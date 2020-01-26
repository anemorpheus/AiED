# Data mining - zastosowania
**Data mining** - proces wyszukiwania wzorców i zależności w dużych i złożonych zbiorach danych. Może być wykorzystane w celu np. analizy ryzyka kredytowego klienta.  
Dotychczasowe techniki (arkusze kalkulacyjne, zapytania do bazy danych) są nieefektywne dla dużych zbiorów, dlatego powstała potrzeba zaprojektowania algorytmów do ich analizy.

`KDD` - proces wyszukiwania przydatnych informacji w zbiorach danych. Obejmuje przygotowanie danych (selekcje, pre-processing, transformacje), `Data mining` oraz interpretacje wyszukanych zależności i wzorów.

`Curse of dimensionality` - wraz ze wzrostem liczby cech / wymiarów, liczba obserwacji / próbek musi rosnąć wykładniczo, aby możliwe było dokładne generalizowanie danych.

## Modelowanie predykcyjne
Przewidywanie dla nowych danych z użyciem zbudowanego modelu na podstawie danych historycznych. Wykorzystują uczenie z nadzorem.

Typy metod modelowania predykcyjnego:
- klasyfikacja - dla zmiennych celu jakościowych, target dyskretny,
- regresja - dla zmiennych celu ilościowych, target ciągły.

Przykładowe metody:
- regresja liniowa,
- analiza dyskryminacyjna `LDA`, `QDA`,
- regresja logistyczna,
- drzewa decyzyjne,
- sieci neuronowe,
- `SVM`,
- klasyfikatory nieparametryczne (`k-NN`).

Przykłady zastosowań:
- wykrywanie spamu - z każdej wiadomości można wyodrębnić pewne cechy, które mogą posłużyć do zbudowania modelu i analizy przyszłych wiadomości e-mail,
- analiza ryzyku nawrotu raka piersi - MammaPrint, wykorzystuje analize mikromacierzy DNA, daje binarny wynik.

## Grupowanie
Polega na szukaniu grup obiektów podobnych do siebie i niepodobnych do innych grup. Nie ma tutaj zmiennej celu, więc grupowanie wykorzystuje uczenie bez nadzoru.

Przykładowe metody:
- hierarchiczne,
- `k-means`
- `Vector Quantization`,
- `SOM`

Problemy grupowania:
- ciężko określić prawdziwą liczbę klastrów w danych - do rozwiązania tego problemu wykorzystuje się metryki oceniające optymalność podziału,
- wyniki zależne od metody klastrowania - nie są deterministyczne.

Przykładowe zastosowania:
- wykrywanie klas w danych mikromacierzowych - wykrywanie zależności między genami, taksomonia choroby,
- profilowanie klientów - klientów można najpierw podzielić na grupy, a dopiero później analizować czym charakteryzuje się dana grupa.

## Analiza asocjacji
Polega na analizowaniu zbioru atrybutów z bazy danych pod kątem wystepowania w nim powtarzających się zależności. Wynikiem analizy są `reguły asocjacyjne` i odpowiadające im parametry. Zadanie polega na znalezieniu wszystkich reguł z `min support` i `min confidence`.

W analizie asocjacji wykorzystuje się następujące parametry:
- `Support` (wsparcie) - częstość występowania reguły,
- `Confidence` (pewność) - stosunek mocy podzbioru `XuY` do mocy zbioru `X` dla reguły `X->Y`
- `Lift`

Przykładowe zastosowania:
- znalezienie grupy produktów często kupowanych razem - np. gdy klient kupił skarpetki to kupił też buty,
- automatyczna klasyfikacja tekstów - słowa występujące często razem mogą oznaczać frazy charakterystyczne dla jakiejś dziedziny,
- wyszukiwanie plagiatów.

## Prognozowanie na podstawie szeregów czasowych
Szeregi czasowe dodają zależności czasowe pomiędzy obserwacjami - liczy się ich kolejność, odległość pomiędzy obserwacjami. Wymaga to zbudowania modeli wykorzystujących te informacje.

Analiza wymaga przyjęcia założeń, iż w szeregu czasowych występuje:
- trend - zależność pomiędzy kolejnymi obserwacjami,
- zmienność sezonowa - okresowe fluktuacje,
- szum.

Prognozowanie polega na ekstrapolowaniu trendu (przewidywanie przyszłych zjawisk) dopasowanego do danych historycznych.

Przykładowe zastosowania:
- przewidywanie zapotrzebowania na energię elektryczną,
- analizowanie giełdy, cen akcji itp.,
- meteorologia,
- analizowanie efektów globalnego ocieplenia w przyszłości.
