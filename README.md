# 🧠 Health Analysis
***
## 👤 Projektinformationen

| **Autor** | thedawid999 |
| :--- | :--- |
| **Studiengang** | Angewandte Künstliche Intelligenz |
| **Projekt/Modul** | Maschinelles Lernen - Unsupervised Learning und Feature Engineering|

***

## 🌟 Projektziel

Ziel dieses Projekts ist die Analyse psychischer Belastungen in der Tech-Branche basierend auf den Daten der OSMI Mental Health in Tech Survey 2016.
Im Mittelpunkt steht die Entwicklung einer strukturierten Datenpipeline bestehend aus:
 * Explorative Datenanalyse (EDA)
 * Datenbereinigung & Feature Engineering
 * Dimensionsreduktion
 * Clustering mittels Gaussian Mixture Models
 * Interpretation der Cluster und Ableitung konkreter HR-Handlungsempfehlungen

Das Projekt zeigt, wie aus heterogenen Umfragedaten psychologisch relevante Muster extrahiert und für betriebliche Anwendungen nutzbar gemacht werden können.

*** 

## 📊 Datensatz

**Quelle**: OSMI Mental Health in Tech Survey 2016

**Anzahl Teilnehmende**: 1433

**Anzahl Variablen**: 63

**Link**: [Kaggle Dataset](https://www.kaggle.com/datasets/osmi/mental-health-in-tech-2016?resource=download)

**Schwerpunkt**: Einstellungen und Erfahrungen im Umgang mit mentaler Gesundheit am Arbeitsplatz.

Der Datensatz enthält zahlreiche Freitexte, fehlende Werte sowie uneinheitliche Kategorien und eignet sich daher ideal zur Demonstration komplexer Datenvorverarbeitung.

***

## 🔍 Explorative Datenanalyse (EDA)

Die Analyse umfasste:
 * Untersuchung der Datentypen
 * Identifikation fehlender Werte
 * Erkennung von Ausreißern (z. B. Alter > 100)
 * Analyse demografischer Variablen (Gender, Alter, Wohn-/Arbeitsland)

Erkenntnisse:

➡️ Hoher Anteil fehlender Werte, besonders bei sensiblen Fragen

➡️ Viele Freitextfelder mit uneinheitlicher Qualität

➡️ Stark variierende Jobrollen und Länderangaben

***

## 🛠️ Datenvorverarbeitung

Umfasste mehrere Schritte:

**🔧 1. Umgang mit fehlenden Werten**
 * Entfernen irrelevanter Freitextfelder
 * Löschen von Zeilen und Spalten mit >40 % Missing Ratio
 * Zielgerichtete Imputation für ausgewählte Fragen

**🧹 2. Vereinheitlichung & Bereinigung**
 * Regex-basiertes Mapping für Gender (male/female/others)
 * Entfernung von Ausreißern (Alter <17 bzw. >67)
 * Bündelung seltener Länder unter Others
 * Kategorisierung von Jobrollen mit Prioritätensystem

**🔄 3. Merkmalskodierung**
 * One-Hot-Encoding für nominale Variablen
 * Ordinal-Encoding für ordinale Variablen
 * Zusammenführung in einen finalen data_preprocessed.csv

***

## 🧩 Feature Engineering

Zwei Ansätze wurden verglichen:

**Ansatz A – PCA**
 * 64 Komponenten für 85 % erklärte Varianz
 * Ergebnis: Schlechte Clustermetriken und geringe Interpretierbarkeit → verworfen

**Ansatz B – Manuelle Feature-Konstruktion (finaler Ansatz)**
Fünf psychologisch interpretierbare Scores wurden gebildet:
 * **employer_support_score** misst, wie stark der derzeitige Arbeitgeber mentale Gesundheit unterstützt (höherer
Wert = stärkerer Support) 
 * **prev_employer_support_score** ist analog zum obigen Score, jedoch für den vorherigen
Arbeitgeber
 * **openness_score** erfasst, wie offen der Befragte gegenüber einem neuen Arbeitgeber in Bezug
auf mentale Gesundheit wäre
 * **perceived_stigma_score** misst, wie stark der Befragte die Meinung vertritt,
dass Offenheit über mentale Gesundheit der Karriere oder dem Team schaden könnte (höherer Wert = stärker
wahrgenommenes Stigma)
 * **mh_status_score** bewertet den subjektiven mentalen Gesundheitsstatus der
Person

➡️ Ergebnis: Reduktion auf 35 Merkmale, interpretierbare Struktur, verbesserte Clustermetriken (Silhouetten-Score und BIC/AIC)

***

## 🤖 Clustering

als Modell wurde **Gaussian Mixture Model** und als Clusteranzahl K = 3 gewählt

Die Cluster unterscheiden sich deutlich hinsichtlich:

 * Mentaler Gesundheitsstatus
 * Arbeitgeberunterstützung
 * Wahrgenommenem Stigma
 * Offenheit über mentale Probleme
 * Jobrollen
 * Remote Work
 * Ländern

Eine klare Segmentierung in drei Gruppen wurde erreicht.

***

## 📌 Interpretierbare Clusterprofile

**Cluster 0 – Belastete, wenig offene Mitarbeitende**
 * Niedriger Mental-Health-Status
 * Geringe Offenheit
 * Tätigkeit v. a. in HR, Design, Administration
 * Selten remote
 * Hoher Unterstützungsbedarf

**Cluster 1 – Stabile, durchschnittliche Vergleichsgruppe**
 * Leicht überdurchschnittliche Werte
 * Ausgewogene Rollenverteilung 
 * Keine akuten Belastungen
 * Grundlage für Best Practices

**Cluster 2 – Offene, mental stabile Personen bei gleichzeitig hohem Stigma**
 * Hohe Offenheit & Resilienz
 * Kaum Arbeitgeberunterstützung
 * Stark ausgeprägtes Stigmaerleben
 * Fast ausschließlich Brasilien
 * Systemische bzw. kulturelle Faktoren relevant

## 🎯 Ergebnisse

### Fünf selbst-generierte Features pro Cluster
<img width="1374" height="966" alt="Screenshot 2026-10-04 165756" src="https://github.com/user-attachments/assets/ae8f6fb3-273f-4355-a513-cf5bd9058d28" />

### Allgemeine Features pro Cluster
| Arbeitsstellen | Arbeitsländer | Geschlecht |
|:---:|:---:|:---:|
| <img width="924" height="832" alt="Screenshot 2026-10-04 170039" src="https://github.com/user-attachments/assets/06b9213f-ffb5-43bf-8619-258950308315" /> | <img width="932" height="831" alt="Screenshot 2026-10-04 170046" src="https://github.com/user-attachments/assets/2d1a6f84-8316-47e0-89c8-2edc94430b58" /> | <img width="950" height="795" alt="Screenshot 2026-10-04 170052" src="https://github.com/user-attachments/assets/4ec22953-21c9-4825-9d83-96d1305e46d0" /> |

| Remote Work | Über MH-Probleme mit Familie teilen |
|:---:|:---:|
| <img width="1271" height="630" alt="Screenshot 2026-10-04 170336" src="https://github.com/user-attachments/assets/c4fc0242-d834-4f3b-a43c-66e7ef867389" /> | <img width="1287" height="662" alt="Screenshot 2026-10-04 170341" src="https://github.com/user-attachments/assets/c003c069-0f6c-4df0-b523-640e25129fbd" /> |

| Schwierigkeiten in der Arbeit bei guter Behandlung | Schwierigkeiten in der Arbeit bei schlechter Behandlung |
|:---:|:---:|
| <img width="1314" height="651" alt="Screenshot 2026-10-04 170347" src="https://github.com/user-attachments/assets/8b9d3d18-657b-4f98-ae4f-1da46bf6d992" /> | <img width="1284" height="642" alt="Screenshot 2026-10-04 170352" src="https://github.com/user-attachments/assets/b8c91289-c2cc-459a-9ea8-7710a599e431" /> |


