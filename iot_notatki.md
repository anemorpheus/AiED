# Wykład 1

Autonomiczny vs automatyczny:
- automatyczny jest przewidywalny, deterministyczny, podczas gdy przewidywalność systemu autonomicznego jest ograniczona
- automatyczny jest mało adaptacyjny, gdzie system autonomiczny zbiera dane na podstawie których adaptuje się do warunków


# Wykład 2

Poziomy autonomiczności:
0. Pojazd nie może jeździć sam, może pokazywać ostrzeżenia albo wykonywać nagłe akcje w krytycznych sytuacjach (awaryjne hamowanie).
1. Pojazd wspomaga kierowcę sterując kierownicą lub przyspieszając / hamując (np. utrzymywanie pojazdu na środku pasa ruchu, utrzymywanie prędkości z adaptacją - Adaptive Cruise Control)
2. Pojazd wspomaga kierowcę sterując kierownicą i przyspieszając / hamując
3. Pojazd może prowadzić samochód, ale tylko w określonych warunkach. Kierowca musi być gotów wkroczyć do akcji w każdej chwili (np. automatyczna jazda w korku)
4. Pojazd może prowadzić samochód, ale tylko w określonych warunkach. Kierowca musi nadzorować automat, ale niekoniecznie musi przejąć stery (automatyczne taxi).
5. Pojazd prowadzi samochód sam w każdych warunkach. Kierowca nie musi (albo nawet nie może) przejąć kontrolę nad pojazdem.

Operated -> Assisted -> Delegated -> Supervised -> Mixed initiative -> Fully automated

Proces systemu autonomicznego:
- obserwacja
  - zbiera informacje
- analiza
  - analiza zebranych danych, ich interpretacja
- decyzja
- akcja

Wyzwania techonologiczne:
- gromadzenie danych
  - jakie dane, z jakich sensorów?
  - jakich sieci komunikacyjnych użyć? 5G?
  - gdzie dane przechowywać?
- przetwarzanie danych
  - z jakich algorytmów korzystać?
  - gdzie przetwarzać?
- autonomiczność pracy
  - problemy z zasilaniem
  - jak zapewnić niezawodność?


# Wykład 3

Porównanie czujników
- radar
  - używa fal radiowych
  - działa w trudniejszych warunkach atmosferycznych
- lidar
  - używa fal świetlnych (LASERYYY)
  - dokładniejszy od radaru
  - drogi
  - czujnik zajmuje dużo przestrzeni
  - działa gorzej w trudniejszych warunkach atmosferycznych
- kamery
  - wykrywanie przechodni, rowerzystów, świateł drogowych
  - największy potencjaly zasięg
  - może rozpoznać kolory
- ultradźwiękowe (sonary)
  - bardzo mały zasięg, więc służy np. do wspomagania parkowania

Potencjalne wyzwania once again:
- ogromna ilość danych
- komunikacja
- przetwarzanie
- przechowywanie
- bezpieczeństwo
- zarządzanie infrastrukturą
- koszt energetyczny
- koszt

## Ogromna ilość danych
Kamery mogą wygenerować 20-40 MB/s. Radar generuje max 100 KB/s podczas gdy lidar generuje ich nawet 700 razy więcej (do 70 MB/s). Samochód może generować dziennie kilka / kilkadziesiąt terabajtów danych sensorycznych!

W jakich bazach danych przechowywać dane?
- relacyjne bazy danych - ustrukturyzowane
- NoSQL - nieustrkturyzowane, lżejsze, lepiej radzą sobie w przetwarzaniu dużej ilości danych
- grafowe - radzi sobie lepiej z danymi bardzo ze sobą powiązanymi
- baza szeregów czasowych - dla czujników, lekka, ma mechanizmy umożliwiające przechowywanie w pamięci, redukcje zapisów do dysku itp.

## Koszty energetyczne
W skrócie - im mniejsze koszty energetyczne (czujników, komputera itp.) tym większy zasięg pojazdu. Samochody autonomiczne zużywają więcej energii (zużywa je subsystem `CAV` - `Connected and Automated Vehicles`), ale jeśli uwzględnimy zalety tych systemów (tworzenie konwojów, ekonomiczna jazda, komunikacja `V2V`) to samochody te mogą zużywać nawet 9% mniej energii w porównaniu ze zwykłymi samochodami elektrycznymi.

# Wykład 4

Internet of Things - system połączonych ze sobą urządzeń przez internet, mogący komunikować sie ze sobą.  
Internet of Everything - nie dotyczy tylko urządzeń, ale też procesów, danych i ludzi.

W IoT urządzenia typowo łączą się przez pewną bramę z serwerem / cloudem (topologia gwiazdy) albo w innym wariancie również same ze sobą (mesh). Do komunikacji może wykorzystać np. pasma radiowe ISM, czyli publicznie dostępne pasma (np. 2.4 GHz).

Im więcej urządzeń, tym potrzebujemy więcej pasma. Mogą wystąpić wtedy problemy z kolizjami. Do rozwiązania problemu możemy wtedy wykorzystać technologie takie jak `random access`, `TDMA` czy `CDMA`.
- `FDMA` - frequency-division multiple access - innnym urządzeniom przypiswane są inne częstotliwości,
- `CDMA` - code-division multiple access - każdemu użytkownikowi przypisywane 'sekwencje rozpraszające', dzięki którym odbiornik jednoznacznie identyfikuje przeznaczoną dla niego transmisję,

Niezawodność transmisji można zwiększyć poprzez dodanie nadmiarowości, wykrywanie błędów, implementacje sprzężenia i korygowanie błędów (kody `FEC`).

`LORA` - Long Range - `WAN` o niskim zapotrzebowaniu energetycznym (`LPWAN` - low-power wide-area network), używa niskich częstotliwości ISM takich jaak 433 MHz czy 868 MHz itp. (zależy od kraju). Wymaga gatewaya.
`NB-IoT` - Narrowband IoT - również `LPWAN`, ma większy zasięg, mniejsze opóźnienia, działa na licencjonowanych pasmach radiowych
`Sigfax` - chuj wie w sumie, podobne do `LORA`, ale ma mniejszą przepustowość
