# LLM-Fine-Tuning: sieben Techniken im Überblick

Technische Vertiefung zu
[Modul 1, Abschnitt 3](01-grundbegriffe.md#3-fine-tuning-prompting-embeddings--drei-unterschiedliche-wege):
Dort steht, dass Fine-Tuning für die meisten Anwendungsfälle in diesem
Repo nicht nötig ist, weil Prompting oder RAG das Problem meist schon
lösen. Dieser Text erklärt, was hinter dem Begriff technisch steckt — für
den Fall, dass eine Fachperson oder ein Dienstleister ihn vorschlägt und
Sie einschätzen müssen, was das bedeutet und was es voraussetzt. Kein
Bestandteil der sechs Basis-Module. Stand: 2026-09-06.

**Vorab, für alle sieben Techniken gleich:** Fine-Tuning verändert ein
Modell dauerhaft anhand eigener Trainingsdaten. Das braucht — anders als
Prompting — eigene, oft manuell erstellte oder geprüfte Datensätze,
Zugang zu Trainings-Hardware (meist GPU, häufig gemietet) und eine
Person, die das Ergebnis fachlich bewertet und den Vorgang bei einer
neuen Modellversion wiederholt. Für einen Betrieb ohne Data-Science-Team
ist das in der Regel nur mit einem spezialisierten Dienstleister
sinnvoll — siehe [`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md)
für den allgemeinen Rechenrahmen aus Einrichtungsaufwand und Amortisation.

## 1. SFT (Supervised Fine-Tuning)

Das Modell wird mit Beispielpaaren aus Eingabe und gewünschter Ausgabe
weitertrainiert, bis es das gezeigte Antwortverhalten nachahmt —
technische Grundform jedes Fine-Tunings, oft der erste Schritt vor
weiteren Verfahren wie DPO oder RLHF (Abschnitte 4–5).

**Voraussetzung:** eine Menge geprüfter Beispiel-Antwortpaare in der
gewünschten Qualität. Deren Erstellung ist meist der größte Aufwand, nicht
das eigentliche Training.

**Praxisrelevanz:** Sinnvoll, wenn ein sehr spezifisches, wiederkehrendes
Antwortformat oder ein Fachjargon zuverlässiger reproduziert werden soll,
als es mit einem Few-Shot-Prompt
([Modul 2](02-prompting.md#drei-techniken-für-schwierigere-aufgaben))
gelingt — für die meisten Anwendungsfälle in diesem Repo reicht Prompting.

Quelle: [Hugging Face TRL, SFT Trainer](https://huggingface.co/docs/trl/sft_trainer).

## 2. LoRA (Low-Rank Adaptation)

Statt alle Modellparameter zu verändern, werden kleine, zusätzliche
Adapter-Matrizen mit niedrigem Rang trainiert, die auf das unveränderte
Basismodell aufgesetzt werden. Das Ergebnis verhält sich wie ein
feinabgestimmtes Modell, ohne dass die ursprünglichen Milliarden
Parameter neu trainiert werden müssen.

**Vorteil gegenüber vollem Fine-Tuning:** deutlich geringerer
Rechenaufwand und Speicherbedarf; mehrere LoRA-Adapter lassen sich für
unterschiedliche Aufgaben auf demselben Basismodell austauschen.

**Praxisrelevanz:** Der heute übliche Einstieg, wenn ein Betrieb mit
externer Unterstützung tatsächlich fine-tunen lässt — deutlich günstiger
als volles Fine-Tuning, aber weiterhin mit eigenen Trainingsdaten und
Fachwissen zur Bewertung des Ergebnisses verbunden.

Quelle: [Hugging Face PEFT, LoRA](https://huggingface.co/docs/peft/package_reference/lora).

## 3. QLoRA

Kombiniert LoRA mit einem quantisierten, also auf niedrigere
Zahlengenauigkeit komprimierten Basismodell. Die Adapter werden auf dem
komprimierten Modell trainiert, was den Speicherbedarf gegenüber
Standard-LoRA nochmals deutlich senkt.

**Vorteil:** Macht Fine-Tuning größerer Modelle auf einzelnen, günstigeren
GPUs statt auf teurer Mehr-GPU-Infrastruktur praktikabel.

**Praxisrelevanz:** Relevant für einen Dienstleister mit begrenztem
Hardwarebudget — für den Betrieb, der den Auftrag vergibt, ändert sich
dadurch vor allem der Preis, nicht das grundsätzliche Vorgehen gegenüber
LoRA.

Quelle: Dettmers et al. (2023), *"QLoRA: Efficient Finetuning of
Quantized LLMs"*, [arXiv:2305.14314](https://arxiv.org/abs/2305.14314).

## 4. DPO (Direct Preference Optimization)

Das Modell lernt direkt aus Paaren von bevorzugter und abgelehnter
Antwort auf dieselbe Eingabe, welches Verhalten gewünscht ist — ohne den
Zwischenschritt eines separat trainierten Belohnungsmodells, den
klassisches RLHF (Abschnitt 5) braucht.

**Voraussetzung:** Paare von Antworten mit einer klaren
Präferenzentscheidung, erstellt von Menschen oder einem als
Bewertungsmaßstab akzeptierten Modell ("LLM-as-a-judge", siehe
[`evaluation.md`, Abschnitt 3](evaluation.md#3-regressionen-verhindern)).

**Praxisrelevanz:** Technisch einfacher umzusetzen als volles RLHF, aber
in der Praxis nur relevant, wenn bereits ein per SFT angepasstes Modell
existiert, dessen Tonfall oder Antwortstil noch gezielt nachjustiert
werden soll — für die meisten KMU-Anwendungsfälle in diesem Repo kein
realistisches Szenario.

Quelle: [Hugging Face TRL, DPO Trainer](https://huggingface.co/docs/trl/dpo_trainer).

## 5. RLHF (Reinforcement Learning from Human Feedback)

Ein separates Belohnungsmodell wird darauf trainiert, menschliche
Präferenzurteile über Modellantworten vorherzusagen; das eigentliche
Sprachmodell wird anschließend per Reinforcement Learning so angepasst,
dass es beim Belohnungsmodell höher bewertete Antworten erzeugt. So
wurden die meisten heutigen, für Dialoge optimierten Foundation-Modelle
über ihr Basistraining hinaus verfeinert.

**Voraussetzung:** umfangreiche menschliche Bewertungsdaten, ein
separates Belohnungsmodell und eine
Reinforcement-Learning-Trainingsinfrastruktur — der aufwendigste der
hier beschriebenen Ansätze.

**Praxisrelevanz:** Wird von den großen Modellanbietern selbst
eingesetzt, nicht von einzelnen anwendenden Betrieben — für einen
Mittelstandsbetrieb in diesem Repo praktisch nie eine eigene
Umsetzungsoption, höchstens Hintergrundwissen darüber, wie das
eingesetzte Modell selbst entstanden ist.

Quelle: [Hugging Face, RLHF erklärt](https://huggingface.co/blog/rlhf).

## 6. GRPO (Group Relative Policy Optimization)

Weiterentwicklung RLHF-artiger Verfahren: Statt eines einzelnen
Belohnungsmodells wertet GRPO eine Gruppe gleichzeitig erzeugter
Antworten auf dieselbe Eingabe relativ zueinander aus und verstärkt die
im Vergleich besseren — ohne ein separates, ebenso großes
Belohnungsmodell trainieren zu müssen wie bei klassischem RLHF. Bekannt
geworden durch das Training aktueller Reasoning-Modelle.

**Praxisrelevanz:** Wie RLHF eine Methode der Modellanbieter beim
Training neuer Foundation-Modelle, kein Werkzeug, das ein Betrieb selbst
anwendet — hier aufgeführt, damit der Begriff bei einer Anbieter- oder
Modellbeschreibung eingeordnet werden kann.

Quelle: [Hugging Face TRL, GRPO Trainer](https://huggingface.co/docs/trl/grpo_trainer).

## 7. Distillation (Wissensdestillation)

Ein kleineres "Schüler"-Modell wird darauf trainiert, die Ausgaben eines
größeren, leistungsfähigeren "Lehrer"-Modells nachzuahmen. Ergebnis ist
ein kompakteres, günstigeres und schnelleres Modell, das einen Teil der
Fähigkeiten des großen Modells für eine engere Aufgabe übernimmt.

**Praxisrelevanz:** Relevant, wenn ein Anbieter ein kleines, günstiges
Modell für einen engen, wiederkehrenden Zweck anbietet (z. B. reine
Klassifikation oder Kurzzusammenfassung) — als Erklärung, warum ein
solches Modell für die schmale Aufgabe gut, für offene Fragen aber
schlechter geeignet sein kann als das große Modell, aus dem es
destilliert wurde.

Quelle: [Hugging Face TRL, Distillation](https://huggingface.co/docs/trl/main/distillation_trainer).

## Einordnung für den eigenen Betrieb

Von den sieben Techniken sind SFT, LoRA und QLoRA die einzigen, die ein
Betrieb realistischerweise selbst beauftragen könnte, meist über einen
externen Dienstleister. DPO ist eine mögliche Ergänzung dazu. RLHF, GRPO
und Distillation sind vor allem Hintergrundwissen darüber, wie
Foundation-Modelle von ihren Anbietern selbst trainiert werden. In
keinem Fall ersetzt Fine-Tuning die Prüfpflicht aus
[Modul 3](03-grenzen-und-risiken.md) — ein fine-getuntes Modell kann
weiterhin halluzinieren und muss weiterhin evaluiert werden (siehe
[`evaluation.md`](evaluation.md)).
