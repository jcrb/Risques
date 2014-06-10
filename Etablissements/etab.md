Etablissement classés
========================================================


Analyse du fichier __Etablissements classés sur la CUS.csv__ qui comporte les établissements soumis à autorisation sr la CUS. Le fichier original se trouve dans le dossier __Data source__. Il a été réenregistré au format _.csv_ avec l'option "mettre les champs entre guillements" à cause des pb causés par les apostrophes.

En terme de risques, la directive Seveso II fixe deux niveaux:
- __établissements SEVESO seuil bas__
- __AS__ Avec Servitudes, anciennement __Seveso Seuil Haut__ [INERIS](http://www.ineris.fr/aida/consultation_document/11319)


```r
path <- "../"
file <- paste0(path,"Etablissements classes sur la CUS.csv")
e <- read.table(file, skip=1, header=TRUE, sep=",")
str(e)
```

```
## 'data.frame':	95 obs. of  5 variables:
##  $ Nom.établissement: Factor w/ 75 levels "AGIP avenue d'alsace ( ex BP)",..: 1 21 2 3 4 5 44 6 8 7 ...
##  $ Code.postal      : int  67000 67000 67000 67000 67000 67000 67000 67000 67000 67000 ...
##  $ Commune          : Factor w/ 1 level "STRASBOURG": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Régime           : Factor w/ 2 levels "Autorisation",..: 2 1 1 1 1 1 1 1 2 1 ...
##  $ Régime.Seveso    : Factor w/ 3 levels "Non-Seveso","Régime inconnu : ",..: 1 1 1 1 1 2 1 1 1 1 ...
```

```r
summary(e$Régime)
```

```
##   Autorisation Enregistrement 
##             89              6
```

```r
summary(e$Régime.Seveso)
```

```
##        Non-Seveso Régime inconnu :           Seuil AS 
##                82                 5                 8
```

Pour tout le Bas-Rhin
----------------------


```r
file <- paste0(path,"Etablissements classes 67.csv")
e <- read.table(file, header=TRUE, sep=",")
summary(e$Régime.Seveso)
```

```
##        Non-Seveso Régime inconnu :           Seuil AS         Seuil Bas 
##               529               106                16                 4
```

```r
e[e$Régime.Seveso == "Seuil AS" | e$Régime.Seveso == "Seuil Bas",]
```

```
##                          Nom.établissement Code.postal      Commune
## 20                         ROQUETTE FRERES       67930     BEINHEIM
## 92         DOW AGROSCIENCES SAS Drusenheim       67410   DRUSENHEIM
## 120                 DOW FRANCE SAS Erstein       67150      ERSTEIN
## 195                  RHONE GAZ Herrlisheim       67850  HERRLISHEIM
## 268                LANXESS EMULSION RUBBER       67610 LA WANTZENAU
## 273               EVONIK OIL ADDITIVES SAS       67630  LAUTERBOURG
## 275               ROHM AND HAAS FRANCE SAS       67630  LAUTERBOURG
## 311           COMPTOIR AGRICOLE Marlenheim       67520   MARLENHEIM
## 326                  MESSIER BUGATTI DOWTY       67129     MOLSHEIM
## 397                            BUTAGAZ SAS       67116   REICHSTETT
## 400                    WAGRAM TERMINAL SAS       67116   REICHSTETT
## 408 TOTAL PETROCHEMICALS FRANCE Oberhoffen       67410   ROHRWILLER
## 514             BOLLORE ENERGIE Strasbourg       67000   STRASBOURG
## 536       JOHNSON CONTROLS ROTH Strasbourg       67000   STRASBOURG
## 550              PRODAIR ET CIE Strasbourg       67000   STRASBOURG
## 553                         RUBIS TERMINAL       67000   STRASBOURG
## 575      SOCIETE EUROPEENNE DE STOCKAGE D1       67000   STRASBOURG
## 576      SOCIETE EUROPEENNE DE STOCKAGE D2       67000   STRASBOURG
## 588                       TREDI Strasbourg       67000   STRASBOURG
## 590                    WAGRAM TERMINAL SAS       67000   STRASBOURG
##           Régime Régime.Seveso Dept Date_Saisie
## 20  Autorisation     Seuil Bas   67  2014-06-05
## 92  Autorisation      Seuil AS   67  2014-06-05
## 120 Autorisation     Seuil Bas   67  2014-06-05
## 195 Autorisation      Seuil AS   67  2014-06-05
## 268 Autorisation      Seuil AS   67  2014-06-05
## 273 Autorisation      Seuil AS   67  2014-06-05
## 275 Autorisation      Seuil AS   67  2014-06-05
## 311 Autorisation     Seuil Bas   67  2014-06-05
## 326 Autorisation      Seuil AS   67  2014-06-05
## 397 Autorisation      Seuil AS   67  2014-06-05
## 400 Autorisation      Seuil AS   67  2014-06-05
## 408 Autorisation      Seuil AS   67  2014-06-05
## 514 Autorisation      Seuil AS   67  2014-06-05
## 536 Autorisation     Seuil Bas   67  2014-06-05
## 550 Autorisation      Seuil AS   67  2014-06-05
## 553 Autorisation      Seuil AS   67  2014-06-05
## 575 Autorisation      Seuil AS   67  2014-06-05
## 576 Autorisation      Seuil AS   67  2014-06-05
## 588 Autorisation      Seuil AS   67  2014-06-05
## 590 Autorisation      Seuil AS   67  2014-06-05
```

Risque sismique
---------------


```r
file <- paste0(path,"Seismes recents en Alsace.csv")
s <- read.table(file, header=FALSE, sep=",")
n <- c("Identifiant du séisme", "Heure UTC", "Latitude", "Longitude", "Magnitude","Type de magnitude","Profondeur (en km)", "Type de profondeur", "Catalogue", "Mode d'évaluation", "Nombre de stations utilisées", "Nombre de phases", "Gap azimuthal", "Mode d'évaluation", "Ville significative","Distance de la ville (en km)")
names(s) <- n
```

Période du 9/5/2013 au 9/5/2014
--------------------------------


```r
file <- paste0(path,"seismes.tsv")
seismes <- read.table(file, header=FALSE, sep="\t")
names(seismes) <- n
summary(seismes$"Ville significative")
```

```
##                  Basel      Breisach am Rhein                 Colmar 
##                      9                      3                      4 
##                 Elzach            Emmendingen              Ettenheim 
##                      1                      3                      7 
##               Freiburg              Gérardmer             Guebwiller 
##                     15                      1                      2 
## Illkirch-Graffenstaden                   Lahr                Lörrach 
##                      1                      7                      4 
##               Mulhouse               Müllheim              Offenburg 
##                      2                      5                      3 
##                Rastatt    Rheinfelden (Baden)   Saint-Dié-des-Vosges 
##                      1                      3                      2 
##             Schopfheim               Sélestat             Strasbourg 
##                      2                      3                      4 
##               Teningen       Titisee-Neustadt         Unterkrozingen 
##                      4                      5                     10 
##       Waldshut-Tiengen          Weil am Rhein             Wittenheim 
##                      8                      1                      1 
##      Zell im Wiesental 
##                      1
```

