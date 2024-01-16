# 📊 Charger des données avec R

## Voir un fichier importé quelle que soit la source :&#x20;

```
head(data)
```

## Importer un fichier CSV

```r
dataCSV <- read_csv('data/fichier.csv', sep = ",", header = 1)
```

Pour un fichier CSV, il est important de préciser le séparateur afin que les données soient bien reconnues. On peut également préciser la ligne contenant les noms de colonnes avec l'option header.

## Importer un fichier parquet

```r
library(arrow)

dataParquet <- read_parquet('data/fichier.parquet')
```

Pour parquet, il est important d'installer et charger la librairie arrow, qui permet de lire les fichiers parquets.

## Importer un fichier Excel

```r
library(readxl)

dataEXCEL <- read_excel("data/fichier_excel.xlsx", sheet = 1)
```

Pour excel, il est important d'installer et charger la librairie readxl, qui permet de lire les fichiers excels.

## Importer un fichier SAS

```r
library(haven)
 
data <- read_sas('data/fichier_sas.sas7bdat')
```

Pour les fichiers ayant sas pour origine, on peut les ouvrir avec la librairie haven.

## Importer un fichier SPSS

```r
library(haven)
 
data <- read_sav('data/fichier_SPSS.sav')
```

Comme pour sas, haven permet d'ouvrir les fichiers SPSS.

## Importer un fichier stata

```r
library("foreign")

data <- read.dta("data/friendly.dta")
```

Pour stata, la librairie foreign permet de lire les fichiers dta avec R.

## Importer un fichier TXT

```r
dataTXT <- read.delim('data/fichier_texte.txt', header = F)
```

Dans le cadre d'un fichier texte, ce chargement permet d'obtenir une ligne par ligne du fichier texte.
