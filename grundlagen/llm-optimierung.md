# LLM-Optimierung: sieben Techniken für schnelleren, günstigeren Betrieb

Technische Vertiefung für IT-Verantwortliche, die ein Sprachmodell selbst
betreiben (siehe [`werkzeuge/README.md#lokale-eu-gehostete-und-cloud-modelle-getrennt-bewerten`](../werkzeuge/README.md#lokale-eu-gehostete-und-cloud-modelle-getrennt-bewerten))
oder ein Angebot eines Betreibers technisch einordnen wollen. Anders als
[`llm-fine-tuning.md`](llm-fine-tuning.md) geht es hier nicht darum, ein
Modell zu verändern, sondern darum, ein vorhandenes Modell schneller und
günstiger laufen zu lassen. Kein Bestandteil der sechs Basis-Module.
Stand: 2026-09-06.

## 1. Quantisierung (Quantization)

Modellparameter werden mit weniger Bit pro Zahl gespeichert und
gerechnet — etwa mit 8 oder 4 Bit (INT8, INT4, GPTQ, AWQ) statt der beim
Training üblichen 32 Bit. Das Modell wird dadurch kleiner, braucht
weniger Arbeitsspeicher und antwortet schneller — mit einem meist
kleinen, aber realen Qualitätsverlust, der vor Produktivbetrieb mit dem
eigenen Testset gemessen werden sollte (siehe
[`evaluation.md`](evaluation.md)).

Quelle: [Hugging Face, Quantization Concept Guide](https://huggingface.co/docs/transformers/quantization/concept_guide).

## 2. Wissensdestillation (Knowledge Distillation)

Ein kleineres "Schüler"-Modell wird darauf trainiert, die Ausgaben eines
größeren "Lehrer"-Modells nachzuahmen — hier als Weg zu einem insgesamt
kleineren, günstigeren Modell für den Betrieb betrachtet, nicht nur als
Trainingstechnik. Ausführlicher unter dem Trainings-Blickwinkel bereits
in [`llm-fine-tuning.md`, Abschnitt 7](llm-fine-tuning.md#7-distillation-wissensdestillation)
beschrieben — an dieser Stelle die betriebliche Seite: Das destillierte
Modell braucht weniger Rechenleistung im laufenden Betrieb, ist aber auf
den Aufgabenbereich beschränkt, für den es destilliert wurde.

Quelle: [Hugging Face, Distillation in 2026](https://huggingface.co/blog/sergiopaniego/distillation-2026).

## 3. KV-Cache (KV Caching)

Bei der Texterzeugung würde ein Modell ohne diese Technik für jedes neue
Wort die sogenannten Attention-Schlüssel und -Werte für den gesamten
bisherigen Text neu berechnen. Der KV-Cache speichert diese Werte einmalig
und nutzt sie für jedes weitere Wort wieder — eine Grundtechnik heutiger
Inferenz-Server, kein optionales Zusatzfeature.

Quelle: [vLLM, PagedAttention und KV-Cache](https://docs.vllm.ai/en/latest/design/paged_attention.html).

## 4. Continuous Batching

Statt Anfragen mehrerer Nutzender in festen, gleich großen Gruppen
("Batches") nacheinander abzuarbeiten, fügt der Server laufend neue
Anfragen hinzu und entfernt fertige — die GPU bleibt dadurch durchgehend
ausgelastet, statt auf die langsamste Anfrage einer festen Gruppe zu
warten. Relevant, sobald mehrere Personen gleichzeitig ein selbst
gehostetes Modell nutzen, nicht bei Einzelnutzung auf einem Büro-PC.

Quelle: [vLLM-Dokumentation](https://docs.vllm.ai/en/latest/).

## 5. Spekulatives Dekodieren (Speculative Decoding)

Ein kleines, schnelles Modell schlägt mehrere nachfolgende Wörter auf
einmal vor; das eigentliche, größere Zielmodell prüft diese Vorschläge in
einem Durchgang, statt jedes Wort einzeln selbst zu erzeugen. Bei
zutreffenden Vorschlägen beschleunigt das die Antwortzeit spürbar, ohne
die Ausgabequalität des großen Modells zu verändern.

Quelle: [vLLM, Speculative Decoding](https://docs.vllm.ai/en/latest/features/spec_decode.html).

## 6. Tensor-Parallelität (Tensor Parallelism)

Einzelne Rechenschritte innerhalb einer Modellschicht werden auf mehrere
GPUs gleichzeitig aufgeteilt, wenn ein Modell zu groß für eine einzelne
GPU ist. Voraussetzung ist eine schnelle Verbindung zwischen den GPUs,
sonst frisst die Kommunikation den Geschwindigkeitsgewinn wieder auf —
eine Frage der eigenen Hardware, nicht der Softwareauswahl allein.

Quelle: [PyTorch, Tensor Parallel Tutorial](https://pytorch.org/tutorials/intermediate/TP_tutorial.html).

## 7. Pipeline-Parallelität (Pipeline Parallelism)

Statt einer einzelnen Schicht wird das gesamte Modell in aufeinander
folgende Abschnitte ("Stufen") aufgeteilt, die auf unterschiedlichen GPUs
laufen; mehrere Anfragen werden versetzt durch diese Stufen geschleust,
ähnlich einem Fließband. Wird häufig mit Tensor-Parallelität kombiniert,
wenn ein Modell weder auf eine GPU noch mit reiner Tensor-Aufteilung
sinnvoll betrieben werden kann.

Quelle: [PyTorch, Pipeline Parallel Tutorial](https://pytorch.org/tutorials/intermediate/pipelining_tutorial.html).

## Einordnung für den eigenen Betrieb

Diese sieben Techniken betreffen den **Betrieb** eines Modells, nicht die
Entscheidung, ob eines eingesetzt wird. Für einen Betrieb ohne eigenes
GPU-Rechenzentrum sind sie vor allem beim Lesen eines Angebots relevant:
Ein Anbieter, der "quantisiert", "batched" oder "spekulativ dekodiert",
verspricht damit niedrigere Kosten oder Antwortzeit — keine höhere
Genauigkeit. Wer selbst über eigene Hardware nachdenkt (siehe
[`werkzeuge/README.md`](../werkzeuge/README.md)), findet Quantisierung
und Continuous Batching bereits in Werkzeugen wie
[vLLM](https://github.com/vllm-project/vllm) oder
[llama.cpp](https://github.com/ggml-org/llama.cpp) eingebaut, Tensor- und
Pipeline-Parallelität werden erst bei Modellen relevant, die nicht mehr
auf eine einzelne GPU passen.
