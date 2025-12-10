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
 * **employer_support_score**
 * **prev_employer_support_score**
 * **openness_score**
 * **perceived_stigma_score**
 * **mh_status_score**

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


