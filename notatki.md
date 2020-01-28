# Data mining - zastosowania
**Data mining** - proces wyszukiwania wzorców i zależności w dużych i złożonych zbiorach danych. Może być wykorzystane w celu np. analizy ryzyka kredytowego klienta.  
Dotychczasowe techniki (arkusze kalkulacyjne, zapytania do bazy danych) są nieefektywne dla dużych zbiorów, dlatego powstała potrzeba zaprojektowania algorytmów do ich analizy.

`KDD` - proces wyszukiwania przydatnych informacji w zbiorach danych. Obejmuje przygotowanie danych (selekcje, pre-processing, transformacje), `Data mining` oraz interpretacje wyszukanych zależności i wzorów.

`Curse of dimensionality`
- wraz ze wzrostem liczby cech / wymiarów, liczba obserwacji / próbek musi rosnąć wykładniczo, aby możliwe było dokładne generalizowanie danych,
- dostępne dane rzadko wypełniają przestrzeń wielowymiarową,
- przy dużej liczbie parametrów może zajść zjawisko przeuczenia (`overfitting`)
- im więcej przestrzeni, tym punkty są dalej od siebie, ciężej też jest obliczyć ich odległość od siebie (ma mniej sensu)

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

# Data mining - algorytmy
## Modelowanie predykcyjne
Model na podstawie zmiennych wejściowych `X` generuje predykcję `Y`.
Zmienne celu `Y` (target) mogą mieć następujące typy wartości:
- `nominal` - zmienne jakościowe nieporządkowe - wartości oznaczają przynależność do klasy, ale nie można ich uporządkować (ustawić w pewnej kolejności) np. Człowiek, Zwierzę, Przedmiot
- `ordinal` - zmienne jakościowe porządkowe - wartości oznaczają przynależność do klasy i można je uporządkować, ale nie można obliczyć różnic ani ilorazu pomiędzy dwoma wartościami, np. Duży, Średni, Mały
- `interval` - zmienne ilościowe ciągłe albo dyskretne, różnice wartości mają znaczenie

Dla zmiennych celu `nominal` i `ordinal` mówimy o klasyfikacji, dla zmiennych typu `interval` mówimy o regresji.

### Regresja liniowa
Funkcja regresji to wartość oczekiwana zmiennej $Y$ dla danego $X$.
$$
f(x) = E(Y|X = x)
$$

Idea jest prosta: szukamy takiej funkcji $f(x)$, która da odpowiednie wyjście $y$ i jest reprezentowana linią.
$$
f(x) = B_0 + \sum X_j\beta_j
$$
Jako zmienne losowe $X_j$ możemy wziąć:
- zmienne losowe ilościowe,
- nieliniowe transformacje zmiennych ilościowych (np. `log`),
- przekształcenia wielomianowe,
- numerycznie zakodowane wartości zmiennej jakościowej.

Model dopasowywany jest poprzez minimalizację błędu kwadratowego `RSS`, czyli suma błędów kwadratowych dla każdego $(x_n, y_n)$.

Weryfikację dopasowania modelu można przeprowadzić z wykorzystaniem narzędzi takich jak:
- wykresy diagnostycznego (np. `Residual vs predicted values` gdzie `Residual` to różnica pomiędzy wartością przewidzianą a wartością zaobserwowaną - im wartości są bardziej rozproszone wertykalnie, tym gorsza regresja),
- testy hipotez dot. istotności parametrów modelu,
- miary błędu dopasowania.

`Standard Error (SE)` - mierzy średni dystans pomiędzy obserwowanymi wartościami, a linią regresji.  
`t Value` - współczynnik estymaty parametru do `SE`. Im większy, tym cecha jest bardziej znacząca.  
`p Value` (inaczej `Pr > |t|`) - im mniejsze, tym bardziej prawdopodobne, że cecha jest ważna. Zazwyczaj wybiera się cechy z `p Value <= 0.05`.

Ważny jest wybór najlepszych cech, dzięki którym można zbudować lepszy model. Do wyboru cech używa się takich metryk jak np. `p Value` czy `t Value`. Parametry można dodawać do modelu na wiele sposobów, np.:
- `Forward` - parametry są kolejno dodawane do modelu,
- `Backward` - zaczynamy od modelu pełnego, parametry są usuwane,
- `Stepwise` - podobne do forward, ale parametr może być później usunięty z modelu.

Miary jakości dopasowania modelu:
- `Root MSE` - średni błąd regresji,
- `R-Square` - 
- `SST (SSTotal)` - suma kwadratów różnic pomiędzy zaobserwowanymi wartościami i ich średnią,
- `SSR (SSReq)` - suma kwadratów różnic pomiędzy przewidywanymi wartościami a średnią wartości zaobserwowanych,
- `SSE (SSErr, RSS)` - suma kwadratów pomiędzy zaobserwowanymi wartościami a wartościami przewidywanymi

`Non parametric regression` - nie ma parametrycznych funkcji tak jak w normalnej regresji, przykładem mogą być np. drzewa regresyjne.

### Klasyfikacja
W odróżnieniu od regresji, zmienna `Y` należy do zbioru możliwych klas (dyskretnych). Szukamy takiego klasyfikatora $f(X)$ minimalizującego oczekiwany błąd predykcji (`expected prediction error`).

#### Klasyfikator Bayesa
`Klasyfikator Bayesa` - wykorzystuje regułę Bayesa, klasyfikuje obserwację do najbardziej prawdopodobnej klasy wg rozkładu warunkowego $Pr(Y|X=x)$. Klasyfikator Bayesa jest optymalny (da najmniejszy oczekiwany błąd predykcji).  
Dla $Pr(c_1|x) > Pr(c_2|x)$ wybiera $Pr(c_1|x)$ (prawdopodobieństwo należenie do klasy $c$ obserwacji $x$). W praktyce ciężko jest wykorzystać klasyfikator Bayesa, ponieważ zakłada on, że rozkłady prawdopodobieństw są rozkładami normalnymi, a w praktyce nie możemy mieć takiej pewności. Musimy znać również wszystkie prawdziwe parametry populacji, co nie jest możliwe w praktyce. Możemy za to użyć `LDA` albo `QDA` do aproksymacji klasyfikatora Bayesa.
`Błąd Bayesa` - błąd spowodowany "nakładaniem się" cech, można go zredukować poprzez dostarczanie nowych informacji.
Regułę klasyfikatora Bayesa można przedstawić `hiperpłaszczyzną`:
$$
g(x) = Pr(c_1|x) - Pr(c_2|x) = 0
$$

- `variance` (wariancja) - informuje, jak bardzo rozrzucone są liczby od ich średniej
- `funkcja gęstości` - funkcja, której całka = 1 i oznacza prawdopodobieństwo

#### LDA
Próbuje znaleźć taką linię (dla 2 cech) lub płaszczyznę (dla więcej niż 2 cech), na której rzutowanie zwiększy separację pomiędzy klasami (na podstawie średnich i macierzy kowariancji cech w różnych klasach),
- określa klasyfikator optymalny Bayesa dla $p(x|c_j)$ o rozkładzie normalnym, gdzie macierze kowariancji cech są takie same w poszczególnych klasach,
- parametry są obliczane na podstawie średnich i macierzy kowariancji cech.

#### QDA
- również zakłada, że prawdopodobieństwa, że cecha występuje w danej klasie, są przedstawione rozkładami normalnymi,
- każda klasa ma różne macierze kowariancji,
- bardziej elastyczne od `LDA`, ale wolniejsze (wymaga więcej parametrów do wyestymowania),
- bardziej narażone na przeuczenie.

#### Naive Bayes
W przypadku wielowymiarowych danych wyznaczenie gęstości `p(x|c_j)` jest trudne. Klasyfikator obchodzi ten problem obliczając tą gęstość jako iloczyn gęstości cech.
$$
p(x|c_j) = \prod p(x_k|c_j)
$$
Klasyfikator zakłada, że **cechy są niezależne**.

#### Regresja logistyczna
Oblicza parametry tak jak w regresji liniowej, ale ponieważ musi na wyjście dać wartości dyskretne to dodatkowo oblicza prawdopodobieństwo.
$$
logit(p) = log(\frac{p}{1-p}) = \sum \beta_j X_j + \beta_0
$$

#### Algorytm perceptronu
Dla danych uczących liniowo separowalnych można znaleźć taką płaszczyznę separującą klasy:
$$
f(x) = \sum \beta_j X_j + \beta_0 = 0
$$
Tak, żeby klasa była określona przez $c_i = sign(f(x))$, co dosłownie znaczy "po której stronie płaszczyzny jest punkt".

Algorytm perceptronu znajduje rozwiązanie dla tej metody, próbując zminimalizować koszt błędnych decyzji.
$$
J(\beta) = \sum|\langle\beta, x\rangle|
$$

Co jeśli dane są nieseparowalne liniowo? Można transformować te dane tak, aby były separowalne (poprzez wykorzystanie dodatkowych perceptronów). Wtedy mamy do czynienia z wielowarstwowymi perceptronami, czyli sieciami neuronowymi.

#### Klasyfikacja nieparametryczna - K najbliższych sąsiadów
Idea: nowy punkt `x` jest klasyfikowany na podstawie `k` najbliższych sąsiadów w zbiorze uczącym.

#### Drzewa decyzyjno-klasyfikacyjne
W korzeniu drzewa mamy cały zestaw danych. Następnie dzielimy zestaw danych pomiędzy kolejnymi węzłami, patrząc przy każdym kroku na jedną cechę.  
Do zalet można zaliczyć łatwy do zrozumienia proces predykcji, a do wad: złą stabilność (zmiana danych może całkowicie zmienić drzewo). Dlatego wymyślono np. `random forest` (zamiast jednego drzewa model zawiera wiele mniejszych drzew).  
Najczęściej konstruowane są drzewa binarne.

Miary jednorodności (`entropia`, `indeks gini`) mierzą entropię klas. Im więcej klas w węźle, tym większa entropia. Przyjmują wartości 1 dla równolicznych klas i 0 dla jednej klasy.

Jak dzielić węzeł?
1. Maksymalizując kryterium *jakości* podziału (np. redukcja entropii, wariancji itp.). Miara wartości podziału:
$$
W(S, A) = I(S) - \sum p(b) I(S_b)
$$
Załóżmy, że metryką jest entropia. Wtedy miara wartości podziału to różnica pomiędzy entropią węzła, a sumą iloczynu prawdpodobieństw gałęzi `b` i ich entropią.
2. Na podstawie badania zależności zmiennych $X_i$ oraz $Y$ - próbujemy dzielić tak, aby były one zależne od siebie.
- dla każdego atrybutu $X$ liczymy `p-value` względem $Y$ (test niezalożności zmiennych),
- wybieramy ten atrybut dla którego `p-value` jest najmniejsze.

Jak długo dzielić węzły? Gdy koniec węzła jest czysty lub mały (`minimum leaf size`).

Jaki powinien być właściwy rozmiar drzewa?
- zbyt wysokie drzewo grozi przeuczeniem
- oceniamy błąd na danych uczących i testowych
- obcinamy pełne drzewo w celu minimalizacji kosztu

#### SVM
Optymalne hiperpłaszczyzny separujące to hiperpłaszyczyny maksymalizujące odległości od punktów granicznych każdej z klas (leżące jak najdalej od klas).  
SVM znajduje te płaszczyzny, starając się zmniejszyć odległości od wektorów nośnych (`support vectors`, punktów które leżą najbliżej hiperpowierzchni, punkty graniczne klas).

Jeśli klas nie da się separować linią można pozwolić niektórym wektorom nośnym na przekroczenie marginesu lub znalezienie się po złej stronie hiperpłaszczyzny. Zadanie optymalizacje polega wtedy na minimalizacji marginesów oraz kosztów błędów związanymi z obecnością tych punktów.  
SVM radzi sobie z nieseparowalnymi danymi mapując dane do przestrzeni o wyższej wymiarowości z wykorzystaniem kerneli. W tej nowej przestrzeni można wtedy poprowadzić hiperpłaszczyzny.

### Metody wyboru cech
Im bardziej złożony model, tym większa różnica $E_test - E_train$.
Im prostszy klasyfikator, tym większy problem z zamodelowaniem zależności.

Trzeba więc znaleźć złoty środek pomiędzy elastycznością, a zdolnością generalizacji (przykładowo, `QDA` jest bardziej elastyczne od `LDA`, ale gorzej mu wychodzi generalizacja).

#### Univariate (filter)
- wyznaczamy związek każdej cechy ze zmienną celu (np. poprzez test hipotezy, że cechy są niezależne obliczając `p-value`)
- sortujemy cechy wg miary zależności (na górze najbardziej zależne)
- wybieramy `k` cech z góry

#### Multivariate (wrapper)
- oceniamy wartość predykcyjną podzbioru cech, wybieramy podzbiór maksymalizający skuteczność klasyfikatora (inaczej: wybieramy najlepsze cechy do klasyfikacji)
- możemy przeanalizować wszystkie zbiory (przegląd zupełny) albo możemy użyć pewnej heurystyki (np. algorytm genetyczny, metody zachłanne)

#### RFE
Przykład metody `mutlivariate`.
1. Zbuduj klasyfikator liniowy używając `d` cech z ogólną postacią płaszczyzną decyzji
$$
D(x) = wX + b
$$
2. Usuń cechę z najmniejszym $w_i^2$
3. Powtarzaj kroki 1-2 dla d-1, d-2, ..., 1 cech pozostałych z poprzedniej iteracji
4. Oceń wartość informacyjną podzbiorów cech `FS` uzyskanych w kolejnych iteracjach za pomocą wybranego klasyfikatora

Opis spoza wykładu: budujemy model używając wszystkich cech, później iteracyjnie wyrzucamy najsłabsze jednocześnie oceniając wydajność modelu. Jeśli wydajność modelu spada, przestajemy odrzucać wartości.

### Metody regularyzacji
Metoda regularyzacji - ograniczanie wartości współczynników danego modelu.  
Norma - całkowity rozmiar albo długość wszystkich wektorów w danej przestrzeni wektorów lub macierzy.

#### Ridge regression
Model minimalizujący `RSS` (`Residual sum of squares`) poprzez ograniczenie rozmiaru współczynników $\beta$ sformułowane jako norma `L_2`. Proporocjonalnie redukuje wartości współczynników.

#### Lasso
Podobne do `ridge regression`, ale ograniczenie na wektor $\beta$ sformułowane jako norma `L_1`. Prowadzi do wyboru zmiennych, ponieważ redukuje niektóre współczynniki do 0.

#### Elastic net
Tak jakby połączenie `ridge regression` i `lasso`: ograniczenia na parametry na podstawie ważonej normy `L1` i `L2`. W porównaniu do `lasso`, które wybierze jedną cechę z powiązanych cech, `elastic net` wybierze całą grupę.

### Metody redukcji cech
#### PCA
Przekształcamy zbiór cech (które prawdopodobnie zawiera cechy skorelowane) na zbiór cech nieskorelowanych. `PCA` wykorzystujemy w np. wizualizacji danych albo redukcji wymiarowości w modelowaniu predykcyjnym / klasteryzacji.

PCA analizuje korelacje pomiędzy cechami. Te najbardziej skorelowane ze sobą są "łączone" w `principal component`.

### Jakość klasyfikacji
Jakość klasyfikacji można ocenić wykorzystując np. macierz konfuzji (macierz kontyngencji).
   
   
                                   przewidywana  
                                  klasa 1  klasa 0  
rzeczywista  klasa 1      TP         FN  
                    klasa 0      FP        TN  

Czułość - jaki procent klasy został oznaczony poprawnie ($\frac{TP}{TP + FN}$)  
Specyficzność - jaki procent nie klasy został oznaczony poprawnie ($\frac{TN}{TN + FP}$).

Do wizualizacji czułości i specyficzności można użyć krzywej `ROC`. Jest to wykres zależności `czułości` w funkcji `1 - specyficzności` (jaki procent klasy został oznaczony poprawnie w funkcji nie klasy oznaczonej niepoprawnie). Im większe pole pod wykresem, tym lepszy model (tym lepiej jest w stanie rozróżnić klasy).

## Grupowanie
Metody niehierarchiczne:
- `k-means clustering`
- złożoność $O(n)$

Metody hierarchiczne:
- aglomeratywne - na początku kazda obserwacja traktowana jest jako osobny klaster, w kolejnynch krokach łączone są najbliższe siebie klastry,
- podziałowe - na początku wszystkie obserwacje traktowane są jako jeden klaster, w kolejnych krokach następuje podział
- złożoność $O(n^2) - O(n^3)$

Do grupowania dużych zbiorów można użyć `k-means` (bo jest szybki), albo można połączyć metody (najpierw grupować z użyciem `k-means`, później innymi metodami na wynikach `k-means`).

### Metody nierhierachiczne
#### K-means
1. Wybierz `k` punktów (środków klastru)
2. Przypisz wszystkie obserwacji do najbliższych klastrów
3. Dla każdego klastra wyznacz nowy środek (średnia punktów w klastrze)
4. Powtarzaj 2 i 3 dopóki żadna obserwacja nie zmieni przynależności klastra

W wyniku uzyskamy `k` rozłącznych klastrów. Podział zależy od wybranych środków, więc jeśli są one losowane to każde uruchomienie algorytmu może dać nam inne wyniki na tych samych danych.

Algorytm wymaga przyjęcia:
- `k` - liczby klastrów
- pewnej metody liczenia odległości pomiedzy punktami (zwykła odległość, odległość cosinusowa itp.)

### Metody hierarchiczne
Oznaczenia:
- $x_i$ - obserwacje
- $C_k$ - klastry
- $G$ - aktualna liczba klastrów
- $D_{KL}$ - odległość między klastrami $C_K$ i $C_L$  
Hierachiczne algorytmy grupowania wymagają przyjęcia pewnej `linkage function` ($D_{KL}$), a wyniki zależą od przyjętej definicji.  
Algorytmy hierarchiczne są deterministyczne (zawsze dają to same wyjście).

Algorytm (wer. aglomeratywna):
1. $C_k = {x_k}, k = 1..n, G = n$ (kademu klastrowi przyporządkuj jeden punkt)
2. Znajdź $K$, $L$ takie, że $D_{KL} = min D_{IJ}, 1 <= I, J <= G$ (znajdź takie klastry, które są do siebie podobne)
3. Zastąp $C_K$ i $C_L$ przez klaster $C_K \cup C_L$, $G = G - 1$ ()
4. Powtarzaj kroki 2, 3 dopóki G > 1

Wszystkie `linkage function` mają wspólne dla siebie to, że:
- wybierane są te zbiory, dla których `linkage function` jest minimalne,
- wszystkie `linkage function` wybierają zbiory sąsiadujące

Typy `linkage function`:
- `average linkage`
  - suma kwadratu odległości środków i wariancji podzielonych przez liczności poszczególnych zbiorów
  - łączy klastry o małej wariancji
  - w wyniku klastry o podobnej wariancji
- `centroid linkage`
  - minimalna odległość środków
- `complete linkage`
  - maksymalny dystans pomiędzy dwoma klastrami
  - w wyniku klastry o podobnej średnicy
- `simple linkage`
  - minimalny dystans pomiędzy dwoma klastrami
  - w wyniku klastry wydłużone, nieregularne
- `ward's minimum variance method`
  - stosunek kwadratu odległości środków od sumy odwrotnych liczności zbiorów
  - w wyniku klastry z grubsza równoliczne
- `density linkage`
  - klastry nieregularne, wydłużone

Przed analizą skupień warto wykonać `standaryzację` (rodzaj normalizacji zmiennej losowej, w wyniku której zmienna uzyskuje średnią oczekiwaną zero i odchylenie standardowe jeden). Często jest to konieczne, ponieważ zmienne z duża wariancją mogą najbardziej wpływać na wynik grupowania.  
Najczęstszym stosowanym przekształceniem jest standaryzacja `z`:
$$
z_{ij} = \frac{x_{ij} - \mu_j}{s_j}
$$
$x_{ij} - oryginalna wartość zmiennej $j$ dla obserwacji $i$,  
$\mu_j, s_j$ - wartość średnia i odchylenie standardowe zmiennej $j$

### VQ

`Kohonen VQ` (`VQ` - `Vector Quantization`) - podobny do k-means, ale wybór nowych środków zależy od malejącej stałej uczenia, przesuwa się w kierunku grupowanych obserwacji. Stała uczenia $L$ maleje, ponieważ gdyby nie malała, algorytm nie byłby zbieżny.
1. Wybierz k punktów
2. Dla obserwacji $X_i$ znajdź najbliższy centroid $S_n$ (`winning seed`)
3. Zmodyfikuj $S_n$ wg formuły:
$$
S_n = S_n(1 - L) + x_iL
$$
4. Powtarzaj krok 2 i 3 po wszystkich próbkach uczących
5. Powtarzaj kroki 2 - 4 zadaną liczbę iteracji

`Metoda MacQueena` - wariant metody `VQ`, gdzie stała uczenia jest odwrotnie proporcjonalna do liczby obserwacji $N_n$ w klastrze przypisaną uprzednio do `winning seed`.
$$
S_n = S_n\frac{N_n}{N_n + 1} + x_i \frac{1}{N_n + 1}
$$

### SOM
1. Wybierz k punktów
2. Dla obserwacji $X_i$ znajdź najbliższy centroid $S_j$ (`winning seed`)
3. Zmodyfikuj wszystkie centroidy wg formuły
$$
S_n = S_n(1 - K(j, n)L) + x_iK(j, n)L
$$
$K(j,n)$ - funkcja malejąca z odległością centroidów $S_j$ i $S_i$ na mapie 2D, (0: daleko, 1: odległość zerowa)
4. Powtarzaj krok 2 i 3 po wszystkich próbkach uczących

SOM pozwala na stworzenie mapy klastrów (np. mapy demograficznej miasta).

## Reguły asocjacyjne
W analizie asocjacji wykorzystuje się następujące parametry:
- `Support` (wsparcie) - częstość występowania reguły,
- `Confidence` (pewność) - stosunek mocy podzbioru `XuY` do mocy zbioru `X` dla reguły `X->Y`
- `Lift` - "pewność / jaki procent transakcje zawiera Y" - określa ile razy częściej kupowany jest produkty w regule niż normalnie, im wyższa tym znaleziona reguła jest bardziej wartościowsza

Jak znaleźć reguły asocjacyjne?
- przegląd zupełny, analizujemy wszystkie możliwe podzbiory - bardzo wolny i zasobożerny, liczba podzbiorów dramatycznie rośnie wraz z liczbą elementów
- można zauważyć, że jeśli zbiór `X` jest częsty, to każdy podzbiór `X` też jest częsty
  - szukamy obiektów często występujących w koszykach (powyżej pewnego supportu) (zbiór $L_1$)
  - szukamy par obiektów występujących w $L_1$ jako kandydatów do reguły asocjacyjnej (powyżej pewnego supportu) (zbiór $L_2$)
  - dalej tworzymy częste trójki, częste czwórki itp.
- modyfikacja poprzedniego algorytmu polega na tym, że:
  - w pierwszym kroku generujemy duże itemsety patrząc na minimalny support
  - w drugim kroku bierzemy duże itemsety i wyciągamy z nich reguły z wystarczającą pewnością (bierzemy jeden element podzbioru i stawiamy go po lewej stronie implikaji, $x => l - x$ gdzie $l$ to duży podzbiór i $x \in l$)
