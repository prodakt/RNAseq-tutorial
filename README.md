<!--
# RNAseq tutorial
## Materiał szkoleniowy do analizy RNA-seq przeprwadzonej w całości w R. 
-->

# RNA-seq in R — szybki tutorial projektowy

## Cel projektu

Celem projektu jest przeprowadzenie uproszczonej analizy danych RNA-seq:
- od danych surowych FASTQ,
- przez preprocessing i mapowanie,
- aż do analizy różnic ekspresji i podstawowej analizy funkcjonalnej.

Projekt został podzielony na 3 etapy odpowiadające typowemu pipeline RNA-seq stosowanemu w analizach biologicznych i biomedycznych.

---

# ETAP 1 — Pozyskanie i przygotowanie danych do analiz

## Dane wejściowe

Dane RNA-seq pochodzą z projektu:

- Bioconductor airway:
  
  https://doi.org/doi:10.18129/B9.bioc.airway

Na potrzeby kursu przygotowano uproszczony zestaw danych:
- odczyty wyekstrahowane wyłącznie dla chromosomu 1,
- mniejsze pliki umożliwiające wykonanie analiz na zwykłym komputerze.

### Dane do pobrania

FASTQ:

https://github.com/prodakt/RNAseq-tutorial/blob/main/data/fastq_airway_Chr1.zip

---

## Zadania do wykonania

### 1. Pobranie i organizacja danych

Przygotuj strukturę katalogów projektu, np.:

```text
RNAseq_project/
├── raw_fastq/
├── trimmed_fastq/
├── qc/
├── reference/
├── bam/
├── counts/
├── results/
└── scripts/
```

---

### 2. Analiza jakości danych FASTQ

Wykonaj analizę jakości danych:
- FastQC,
- MultiQC (opcjonalnie).

Należy:
- sprawdzić jakość odczytów,
- ocenić obecność adapterów,
- sprawdzić rozkład jakości,
- ocenić długości odczytów,
- ocenić poziom duplikacji.

---

### 3. Decyzja o trymowaniu

Na podstawie wyników QC:
- zdecyduj, czy dane wymagają trymowania,
- uzasadnij decyzję biologicznie i technicznie.

Jeżeli wykonujesz trymowanie:
- usuń adaptery,
- usuń końce niskiej jakości,
- wykonaj ponownie analizę jakości po preprocessing.

Możliwe narzędzia:
- fastp,
- Trimmomatic,
- cutadapt.

---

### 4. Pobranie referencji genomowej

Z bazy ENSEMBL pobierz:
- genom referencyjny FASTA,
- plik adnotacyjny GTF/GFF,
- wyłącznie dla chromosomu 1.

Przykład:
- Homo sapiens,
- GRCh38.

---

## Efekt końcowy etapu 1

Student powinien posiadać:
- dane FASTQ po preprocessing,
- raport jakości,
- referencję FASTA,
- plik GTF/GFF,
- opis decyzji dotyczących preprocessing.

---

# ETAP 2 — Mapowanie i quantification

## Cel

Mapowanie odczytów RNA-seq do genomu referencyjnego
oraz wygenerowanie macierzy ekspresji genów.

---

## Zadania do wykonania

### 1. Budowanie indeksu referencyjnego

Wykorzystaj pakiet:

```r
Rsubread
```

Wykonaj:
- budowę indeksu genomowego,
- przygotowanie referencji do mapowania.

---

### 2. Mapowanie odczytów

Dla każdej próbki:
- wykonaj alignment do genomu referencyjnego,
- wygeneruj pliki BAM.

Należy:
- sprawdzić skuteczność mapowania,
- porównać próbki,
- opisać wyniki.

---

### 3. Feature counting

Wykorzystaj:

```r
featureCounts()
```

Do:
- przypisania odczytów do genów,
- wygenerowania wspólnej macierzy countów.

---

### 4. (Opcjonalnie) alternatywne pipeline

Możliwe rozszerzenia:
- StringTie,
- Ballgown,
- Cufflinks.

---

## Efekt końcowy etapu 2

Student powinien posiadać:
- pliki BAM,
- statystyki mapowania,
- macierz ekspresji (counts matrix),
- podstawowe wykresy jakości i mapowania.

---

# ETAP 3 — Analiza różnic ekspresji i analiza funkcjonalna

## Dane

Na tym etapie można:
- wykorzystać własne count matrix z etapu 2,
- lub użyć pełnych danych z pakietów:
  - airway,
  - pasilla.

---

## Zadania do wykonania

### 1. Analiza różnic ekspresji

Wykorzystaj:

```r
DESeq2
```

Należy:
- przygotować metadata,
- zbudować obiekt DESeqDataSet,
- wykonać normalizację,
- przeprowadzić analizę różnic ekspresji,
- wygenerować tabelę wynikową.

---

### 2. Wizualizacja wyników

Wygeneruj:
- MA plot,
- volcano plot,
- PCA,
- heatmap,
- histogramy,
- boxploty.

Wszystkie wykresy powinny posiadać:
- tytuły,
- opisy osi,
- legendy,
- interpretację biologiczną.

---

### 3. Analiza funkcjonalna

Wykorzystaj:

```r
gProfiler
```

lub inne narzędzia:
- clusterProfiler,
- enrichR,
- GO,
- KEGG.

Należy:
- wybrać geny różnicujące się,
- wykonać enrichment analysis,
- opisać znaczenie biologiczne wyników.

---

# Maksymalny zakres wykonanej pracy i punktacja

## Poziom podstawowy — do 30%

Wykonanie kompletnych analiz tutorialowych:
- preprocessing,
- mapowanie,
- DESeq2,
- podstawowe wykresy,
- krótkie opisy wyników.

Dotyczy wyłącznie danych tutorialowych.

---

## Poziom rozszerzony — do 65%

Wykonanie pełnych analiz:
- identycznych jak tutorial,
- ale na danych udostępnionych do ćwiczeń.

Wymagane:
- wykresy,
- tabele,
- opisy wyników,
- interpretacja.

---

## Poziom zaawansowany — do 100%

Wykonanie kompletnego projektu RNA-seq:
- preprocessing,
- mapowanie,
- DE,
- analiza funkcjonalna,
- raport naukowy.

Raport powinien być przygotowany:
- w LaTeX,
- np. w platformie Overleaf,
- w szablonie wybranego czasopisma naukowego.

Raport powinien zawierać:
- kod R,
- opis metod,
- opisy wykresów,
- opisy tabel,
- interpretację biologiczną,
- podsumowanie wyników.

---
