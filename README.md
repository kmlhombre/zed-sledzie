-   <a href="#cel-projektu" id="toc-cel-projektu">Cel projektu</a>
-   <a href="#wykorzystane-pakiety"
    id="toc-wykorzystane-pakiety">Wykorzystane pakiety</a>
-   <a href="#informacje-dotyczące-zbioru-danych"
    id="toc-informacje-dotyczące-zbioru-danych">Informacje dotyczące zbioru
    danych</a>
    -   <a href="#podstawowe-informacje"
        id="toc-podstawowe-informacje">Podstawowe informacje</a>
-   <a href="#analiza-danych" id="toc-analiza-danych">Analiza danych</a>
    -   <a
        href="#potwierdzenie-zjawiska-stopniowego-karłowacenia-śledzi-oceanicznych-wyławianych-w-europie"
        id="toc-potwierdzenie-zjawiska-stopniowego-karłowacenia-śledzi-oceanicznych-wyławianych-w-europie">Potwierdzenie
        zjawiska stopniowego karłowacenia śledzi oceanicznych wyławianych w
        Europie</a>
    -   <a href="#wykres-korelacji-zmiennych"
        id="toc-wykres-korelacji-zmiennych">Wykres korelacji zmiennych</a>
-   <a href="#predykcja" id="toc-predykcja">Predykcja</a>
    -   <a href="#linear-regression" id="toc-linear-regression">Linear
        Regression</a>
    -   <a href="#random-forest" id="toc-random-forest">Random Forest</a>
    -   <a href="#k-nn" id="toc-k-nn">k-NN</a>
    -   <a href="#porównanie-modeli" id="toc-porównanie-modeli">Porównanie
        modeli</a>
    -   <a href="#atrybuty-wpływające-na-wynik"
        id="toc-atrybuty-wpływające-na-wynik">Atrybuty wpływające na wynik</a>
-   <a href="#podsumowanie" id="toc-podsumowanie">Podsumowanie</a>

# Cel projektu

Celem projektu jest analiza połowów śledzi oceanicznych wyławianych w
Europie.

# Wykorzystane pakiety

Do wykonania analizy danych zostały wykorzystane następujące pakiety:

|            |
|:-----------|
| plotly     |
| caret      |
| lattice    |
| ggcorrplot |
| tidyr      |
| ggplot2    |
| dplyr      |
| knitr      |

# Informacje dotyczące zbioru danych

## Podstawowe informacje

Zbiór danych został wczytany i oczyszczony z brakujących danych.
Rekordy, które nie miały wartości zostały usunięte z zestawu danych.

    ## [1] "Liczba wierszy:  42488"

    ## [1] "Liczba kolumn:  16"

### Próbka z zestawu danych

|   X | length |   cfin1 |   cfin2 |   chel1 |    chel2 |   lcop1 |    lcop2 |  fbar |   recr |      cumf |   totaln |      sst |      sal | xmonth | nao |
|--:|----:|----:|----:|----:|-----:|----:|-----:|---:|----:|-----:|-----:|-----:|-----:|----:|--:|
|   1 |   22.5 | 0.02778 | 0.27785 | 2.46875 | 21.43548 | 2.54787 | 26.35881 | 0.356 | 482831 | 0.3059879 | 267380.8 | 14.30693 | 35.51234 |      7 | 2.8 |
|   2 |   25.0 | 0.02778 | 0.27785 | 2.46875 | 21.43548 | 2.54787 | 26.35881 | 0.356 | 482831 | 0.3059879 | 267380.8 | 14.30693 | 35.51234 |      7 | 2.8 |
|   3 |   25.5 | 0.02778 | 0.27785 | 2.46875 | 21.43548 | 2.54787 | 26.35881 | 0.356 | 482831 | 0.3059879 | 267380.8 | 14.30693 | 35.51234 |      7 | 2.8 |
|   4 |   24.0 | 0.02778 | 0.27785 | 2.46875 | 21.43548 | 2.54787 | 26.35881 | 0.356 | 482831 | 0.3059879 | 267380.8 | 14.30693 | 35.51234 |      7 | 2.8 |
|   6 |   24.0 | 0.02778 | 0.27785 | 2.46875 | 21.43548 | 2.54787 | 26.35881 | 0.356 | 482831 | 0.3059879 | 267380.8 | 14.30693 | 35.51234 |      7 | 2.8 |
|   7 |   23.5 | 0.02778 | 0.27785 | 2.46875 | 21.43548 | 2.54787 | 26.35881 | 0.356 | 482831 | 0.3059879 | 267380.8 | 14.30693 | 35.51234 |      7 | 2.8 |

### Podsumowanie zestawu danych

|     | X             | length       | cfin1           | cfin2           | chel1          | chel2          | lcop1            | lcop2          | fbar           | recr            | cumf            | totaln          | sst           | sal           | xmonth         | nao              |
|:-|:----|:---|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|
|     | Min. : 1      | Min. :19.0   | Min. : 0.0000   | Min. : 0.0000   | Min. : 0.000   | Min. : 5.238   | Min. : 0.3074    | Min. : 7.849   | Min. :0.0680   | Min. : 140515   | Min. :0.06833   | Min. : 144137   | Min. :12.77   | Min. :35.40   | Min. : 1.000   | Min. :-4.89000   |
|     | 1st Qu.:13233 | 1st Qu.:24.0 | 1st Qu.: 0.0000 | 1st Qu.: 0.2778 | 1st Qu.: 2.469 | 1st Qu.:13.427 | 1st Qu.: 2.5479  | 1st Qu.:17.808 | 1st Qu.:0.2270 | 1st Qu.: 360061 | 1st Qu.:0.14809 | 1st Qu.: 306068 | 1st Qu.:13.60 | 1st Qu.:35.51 | 1st Qu.: 5.000 | 1st Qu.:-1.90000 |
|     | Median :26308 | Median :25.5 | Median : 0.1111 | Median : 0.7012 | Median : 5.750 | Median :21.435 | Median : 7.0000  | Median :24.859 | Median :0.3320 | Median : 421391 | Median :0.23191 | Median : 539558 | Median :13.86 | Median :35.51 | Median : 8.000 | Median : 0.20000 |
|     | Mean :26316   | Mean :25.3   | Mean : 0.4457   | Mean : 2.0269   | Mean :10.016   | Mean :21.197   | Mean : 12.8386   | Mean :28.396   | Mean :0.3306   | Mean : 519877   | Mean :0.22987   | Mean : 515082   | Mean :13.87   | Mean :35.51   | Mean : 7.252   | Mean :-0.09642   |
|     | 3rd Qu.:39447 | 3rd Qu.:26.5 | 3rd Qu.: 0.3333 | 3rd Qu.: 1.7936 | 3rd Qu.:11.500 | 3rd Qu.:27.193 | 3rd Qu.: 21.2315 | 3rd Qu.:37.232 | 3rd Qu.:0.4650 | 3rd Qu.: 724151 | 3rd Qu.:0.29803 | 3rd Qu.: 730351 | 3rd Qu.:14.16 | 3rd Qu.:35.52 | 3rd Qu.: 9.000 | 3rd Qu.: 1.63000 |
|     | Max. :52580   | Max. :32.5   | Max. :37.6667   | Max. :19.3958   | Max. :75.000   | Max. :57.706   | Max. :115.5833   | Max. :68.736   | Max. :0.8490   | Max. :1565890   | Max. :0.39801   | Max. :1015595   | Max. :14.73   | Max. :35.61   | Max. :12.000   | Max. : 5.08000   |

### Długość złowionego śledzia \[cm\]

![](raport_files/figure-markdown_github/unnamed-chunk-6-1.png)

### Zagęszczenie Calanus finmarchicus gat. 1 - cfin1

![](raport_files/figure-markdown_github/unnamed-chunk-7-1.png)

### Zagęszczenie Calanus finmarchicus gat. 2 - cfin2

![](raport_files/figure-markdown_github/unnamed-chunk-8-1.png)

### Zagęszczenie Calanus helgolandicus gat. 1 - chel1

![](raport_files/figure-markdown_github/unnamed-chunk-9-1.png)

### Zagęszczenie Calanus helgolandicus gat. 2 - chel2

![](raport_files/figure-markdown_github/unnamed-chunk-10-1.png)

### Zagęszczenie widłonogów gat. 1 - lcop1

![](raport_files/figure-markdown_github/unnamed-chunk-11-1.png)

### Zagęszczenie widłonogów gat. 2 - lcop2

![](raport_files/figure-markdown_github/unnamed-chunk-12-1.png)

### Natężenie połowów w regionie - fbar

![](raport_files/figure-markdown_github/unnamed-chunk-13-1.png)

### Roczny narybek \[liczba śledzi\] - recr

![](raport_files/figure-markdown_github/unnamed-chunk-14-1.png)

### Łączne roczne natężenie połowów w regionie - cumf

![](raport_files/figure-markdown_github/unnamed-chunk-15-1.png)

### Łączna liczba ryb złowionych w ramach połowu - totaln

![](raport_files/figure-markdown_github/unnamed-chunk-16-1.png)

### Temperatura przy powierzchni wody \[°C\] - sst

![](raport_files/figure-markdown_github/unnamed-chunk-17-1.png)

### Poziom zasolenia wody \[Knudsen ppt\] - sal

![](raport_files/figure-markdown_github/unnamed-chunk-18-1.png)

### Miesiąc połowu - xmonth

![](raport_files/figure-markdown_github/unnamed-chunk-19-1.png)

### Oscylacja północnoatantycka \[mb\] - nao

![](raport_files/figure-markdown_github/unnamed-chunk-20-1.png)

# Analiza danych

## Potwierdzenie zjawiska stopniowego karłowacenia śledzi oceanicznych wyławianych w Europie

Z racji tego że w zestawie danych brakuje jednoznacznych znaczników
czasowych, wykorzystałem liczbę porządkową w kolumne X, aby zachować
chronologię badań.

<div id="htmlwidget-e5885749dd2b7b3ad064" style="width:672px;height:480px;" class="plotly html-widget"></div>

## Wykres korelacji zmiennych

W celu ułatwienia odczytywania danych, ukryłem powtarzające się
macierze.
![](raport_files/figure-markdown_github/unnamed-chunk-22-1.png)

Na powyższym wykresie korelacji należy zwrócić uwagę na atrybuty
korelujące z długością śledzi. Dodatnia korelacja zauważalna jest z
wartościami zagęszczenia Calanus helgolandicus gat. 1 (chel1),
zagęszczenia widłonogów gat. 1 (lcop1) i ułamku pozostawionego narybku
(fbar). Natomiast długość śledzia jest ujemnie, bardzo silnie
skorelowana z temperaturą przy powierzchni wody (sst) oraz, w mniejszym
stopniu, z oscylacją północnoatlantycką (nao).

# Predykcja

## Linear Regression

    ## Linear Regression 
    ## 
    ## 29744 samples
    ##    15 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (2 fold, repeated 5 times) 
    ## Summary of sample sizes: 14873, 14871, 14872, 14872, 14874, 14870, ... 
    ## Resampling results:
    ## 
    ##   RMSE      Rsquared   MAE    
    ##   1.330122  0.3509969  1.04961
    ## 
    ## Tuning parameter 'intercept' was held constant at a value of TRUE

## Random Forest

    ## Random Forest 
    ## 
    ## 29744 samples
    ##    15 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (2 fold, repeated 5 times) 
    ## Summary of sample sizes: 14871, 14873, 14870, 14874, 14870, 14874, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   mtry  RMSE      Rsquared   MAE      
    ##    2    1.143350  0.5207053  0.9035362
    ##    8    1.106012  0.5521849  0.8674326
    ##   15    1.189615  0.5034302  0.9292877
    ## 
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final value used for the model was mtry = 8.

## k-NN

    ## k-Nearest Neighbors 
    ## 
    ## 29744 samples
    ##    15 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (2 fold, repeated 5 times) 
    ## Summary of sample sizes: 14872, 14872, 14872, 14872, 14874, 14870, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   k  RMSE      Rsquared   MAE      
    ##   5  1.149578  0.5246518  0.9009937
    ##   7  1.132480  0.5348631  0.8882642
    ##   9  1.124871  0.5391710  0.8828078
    ## 
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final value used for the model was k = 9.

## Porównanie modeli

    ## 
    ## Call:
    ## summary.resamples(object = resamples_results)
    ## 
    ## Models: LR, RF, KNN 
    ## Number of resamples: 10 
    ## 
    ## MAE 
    ##          Min.   1st Qu.    Median      Mean   3rd Qu.      Max. NA's
    ## LR  1.0425824 1.0477413 1.0492743 1.0496102 1.0505849 1.0567158    0
    ## RF  0.8613752 0.8661555 0.8680242 0.8674326 0.8686959 0.8746337    0
    ## KNN 0.8750379 0.8795502 0.8817268 0.8828078 0.8878530 0.8913671    0
    ## 
    ## RMSE 
    ##         Min.  1st Qu.   Median     Mean  3rd Qu.     Max. NA's
    ## LR  1.322250 1.327729 1.329754 1.330122 1.333169 1.337500    0
    ## RF  1.099842 1.103453 1.106526 1.106012 1.108113 1.111417    0
    ## KNN 1.116023 1.119765 1.123577 1.124871 1.129647 1.137692    0
    ## 
    ## Rsquared 
    ##          Min.   1st Qu.    Median      Mean   3rd Qu.      Max. NA's
    ## LR  0.3442899 0.3478061 0.3516040 0.3509969 0.3538881 0.3579734    0
    ## RF  0.5442893 0.5512907 0.5528719 0.5521849 0.5543610 0.5576485    0
    ## KNN 0.5300661 0.5350623 0.5401146 0.5391710 0.5421190 0.5463918    0

## Atrybuty wpływające na wynik

W celu przedstawienia atrybutów, które, na podstawie dostępnych danych,
są przyczyną karłowacenia śledzi wykorzystany zostanie model
RandomForest. Dane zostały wcześniej wyczyszczone.

![](raport_files/figure-markdown_github/unnamed-chunk-28-1.png)

Na podstawie powyższego wykresu można stwierdzić, że największy wpływ na
długość śledzi ma temperatura wody oraz zagęszczenie widłogonów gat. 1.
Atrybuty takie jak miesiąc oraz X, czyli numer porządkowy, zostały
przeze mnie pominięte celowo, ponieważ nie mają znaczenia dla naszej
analizy danych.

# Podsumowanie

Wykonane badania dowiodły że za procesem karłowacenia śledzi
oceanicznych wyławianych w Europie w ostatnich 60 latach, odpowiadają
wzrost temperatury wody oraz dostępność niektórych planktonów, w głównej
mierze zagęszczenie widłogonów gat. 1.