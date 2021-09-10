# Lidar 2D to 3D

Celem projektu było stworzenie urządzenia zdolnego do skanowania otaczającej go przestrzeni w 3D z użyciem lidaru 2D.

# Spis treści

- [Galeria]()
  - [2D]()
  - [3D]()
- [Submoduły]()
  - [lidar-tools\*]()
    - [sync\*]()
    - [servoctl]()
    - [receiver/transmitter]()
    - [scan-dummy]()
  - [lidar-avr\*]()
  - [lidar-scan\*]()
  - [lidar-vis]()
  - [lidar-visualization]()
  - [lidar-stm32]()
- [Elementy]()
  - [Lidar]()
    - [Specyfikacja]()
    - [Źródła]()
    - [Tryby skanowania]()
    - [Dane]()
    - [Pomiary szybkości silnika lidaru]()
    - [Ogólne pomiary rezultatów lidaru]()
  - [Serwomechanizm]()
  - [IMU]()
    - [MPU-6050]()
    - [MPU-9250]()
    - [Kalibracja]()
    - [DMP]()
  - [Mikrokontroler]()
  - [Głowica]()
    - [Prototyp]()
    - [Wersja finalna]()
- [Skanowanie 3D]()
  - [Obróbka surowych pomiarów IMU]()
- [Konfiguracja]()
  - [Hardware]()
  - [Software]()
    - [Parametry _lidar-tools/sync_]()
- [Materiały dodatkowe]()
  - [Oprogramowanie pomocnicze]()
  - [Przykłady chmur punktów]()

# Galeria

## 3D

## 2D

# Submoduły

W tym repozytorium pod jednym dachem zebrane są repozytoria z przedrostkiem \*lidar-\*\* rozwijane w ramach [KNEI](https://github.com/knei-knurow), które mają mniejszy lub większy związek ze skanowaniem 3D. Więcej informacji o każdym z tych projektów można znaleźć w ich plikach README.

**Gwiazdka \* oznacza repozytoria, które są wymagane do skanowania 3D.** Pozostałe projekty mogą się przydać podczas zabawy ze skanowaniem 2D.

## lidar-tools\*

Zbiór programów _narzędzi_ przydatnych podczas pracy z lidarem.

### sync\*

Najważniejsze z _narzędzi_. Do jego zadań należy:

- Ustanowienie połączenia z mikrokontrolerem (który steruje serwem i akcelerometrem) oraz lidarem.
- Synchronizacja danych/pomiarów z dostępnych źródeł.
- Obliczanie punktów chmury 3D.
- Wypisywanie punkt po punkcie (x, y, z) na standardowe wyjście (stdout).

### servoctl

Wysyła do mikrokontrolera ramkę danych ustawiającą serwo na zadanej pozycji.

### transmitter/receiver

Wysyła/odbiera dane lidaru 2D (uzyskane np. za pomocą _lidar-scan_) przez UDP.

### scan-dummy

Udaje _lidar-scan_. Generuje przykładowe dane.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

## lidar-avr\*

Oprogramowanie przeznaczone do kompilacji na mikrokontroler AVR Atmega328p, którego zadaniem jest obsługa serwa i akcelerometru oraz komunikacja poprzez USART z urządzeniem operatora.

Więcej o dokładnej konfiguracji i działaniu w odpowiedniej sekcji tego dokumentu.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

## lidar-scan\*

Projekt wywodzący się z _lidar-visualizations._ Pomysł polegał na stworzeniu programu, który [specjalizuje się w jednym konkretnym zastosowaniu i robi je dobrze]https://en.wikipedia.org/wiki/Unix_philosophy).

Zadaniem programu jest ustanowienie połączenia z lidarem oraz wypisywanie na standardowe wyjście (stdout) odebranych danych w formie tekstowej. Docelowo dane mogą być przekazane dowolnemu innemu programowi, który rozumie wejściowy format danych (_lidar-vis, lidar-stream)._

Zgodny z systemami Linux, macOS, Windows.

**Przykładowe wyjście:**

```
# A comment
# ! ID Number   Elapsed time [ms]
# Angle [°]   Distance [mm]
! 0 0
120  100
240  100
360  100
! 1 500
120  200
240  200
360  200
! 2 500
```

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

## lidar-vis

Graficzie wyświetla dane otrzymane z lidaru za pomocą _lidar-scan_.

Projekt wywodzący się z _lidar-visualizations_. Jest to "siostrzany" program do \_lidar-scan – [robi jedną rzecz i robi ją dobrze](https://en.wikipedia.org/wiki/Unix_philosophy).

Zgodny z systemami Linux, macOS, Windows.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy) [Bartek Pacia](https://github.com/bartekpacia)

## lidar-visualizations

Wyświetla dane z lidaru w postaci tekstowej lub graficznej w czasie rzeczywistym.

Oprogramowanie kilkukrotnie zmieniło prawie całkowicie swoją formę. Stworzone zostało na potrzeby artykułu do "Elektroniki Praktycznej" w zamian za wypożyczenie od KAMAMI lidaru. Na chwilę obecną nie jest aktywnie rozwijane. Kod składa się z kilku interfejsów, które teoretycznie umożliwiają tworzenie dodatkowych funkcjonalności. Program korzysta z oficjalnego RPLIDAR SDK oraz wysokopoziomowej biblioteki graficznej SFML.

Zgodny z systemami Linux, macOS, Windows.

Więcej informacji można przeczytać w artykule ["Wizualizacja pomiarów skanera LIDAR"](https://ep.com.pl/kursy/notatnik-konstruktora/14763-wizualizacja-pomiarow-skanera-lidar) w ["Elektronice Praktycznej"](https://ep.com.pl) z marca 2021.

**Autor:** [Szymon Bednorz](https://github.com/github.com/dsonyy)

## lidar-stm32

Ciekawy projekt, który podobnie jak _lidar-visualizations_, stworzony został na potrzeby "Elektroniki Praktycznej". Uruchamiany jest na płytce STM32, która za pomocą UART wysyła/odbiera dane do/z lidaru, a następnie je wizualizuje.

RPLIDAR SDK nie jest przystosowany do urządzeń _embeddeed_, więc stworzony został własny kod (na podstawie tego z RPLIDAR SDK) specjalnie dla platformy STM32.

Więcej informacji można przeczytać w artykule ["Wizualizacja pomiarów skanera LIDAR"](https://ep.com.pl/kursy/notatnik-konstruktora/14763-wizualizacja-pomiarow-skanera-lidar) w ["Elektronice Praktycznej"](https://ep.com.pl) z marca 2021.

**Autor:** [Bartek Dudek](https://github.com/github.com/doodek)

# Elementy

## Lidar

Wykorzystywany w projekcie lidar to [Slamtec RPLIDAR A3](https://www.slamtec.com/en/Lidar/A3Spec). Producent dostarcza także [RPLIDAR SDK](https://github.com/Slamtec/rplidar_sdk) wspierające systemy Linux, macOS i Windows, które pozwala na pracę ze sprzętem.

Lidar posiada swoje własne zasilanie. Dysponuje również przewodem USB, aby przesyłać dane do urządzenia operatora.

### Specyfikacja

| Wielkość                        | A3         |
| ------------------------------- | ---------- |
| Zakres pomiarów                 | do 25m     |
| Częstotliwość pomiarów          | do 16kHz   |
| Częstotliwość wykonywania chmur | 5Hz - 20Hz |
| Rozdzielczość kątowa            | do 0.225°  |
| Interfejs komunikacji           | TTL UART   |
| Prędkość komunikacji            | 256000bps  |

### Źródła

- [RPLIDAR A3](https://www.slamtec.com/en/Lidar/A3)
- [SDK GitHub](https://github.com/Slamtec/rplidar_sdk)
- [RPLIDAR A3 User Manual](https://download.kamami.pl/p573426-LM310_SLAMTEC_rplidarkit_usermanual_A3M1_v1.0_en.pdf)
- [RPLIDAR A3 Introduction and Datasheet](https://download.kamami.pl/p573426-LD310_SLAMTEC_rplidar_datasheet_A3M1_v1.3_en.pdf)

### Tryby skanowania

RPLIDAR oferuje kilka trybów skanowania. Godne uwagi są tylko dwa: domyślny sensitivity (indoor) i stability (outdoor). Podczas pracy na zewnątrz, szczególnie w bardzo słoneczne dni, wyraźnie widać różnicę w ilości poprawnie wykonanych pomiarów. Pozostałe tryby istnieją dla kompatybilności wstecznej z poprzednimi generacjami urządzenia i/lub wymagają niższego baudrate'u podczas transmisji danych.

| ID  | Scan mode                         | Sample time [us] | Frequency |
| --- | --------------------------------- | ---------------- | --------- |
| 0   | Standard                          | 252              | 0.484406  |
| 1   | Express                           | 126              | 0.968812  |
| 2   | Boost                             | 63               | 1.93762   |
| 3   | **Sensitivity/Indoor (domyślny)** | 63               | 1.93762   |
| 4   | **Stability/Outdoor**             | 100              | 1.2207    |

### Dane

- Domyślnym formatem danych lidaru są pary (kąt, odległość) w jednostkach [stopnie, milimetry].
- Pary pomiarów są pogrupowane po 360 stopni - jedna chmura punktów.
- Jeżeli pomiar dla danego kąta się nie powiódł, wartość odległości jest równa 0.
- Maksymalna ilość punktów w jednej chmurze to 8192, jest to narzucone przez producenta ograniczenie.
- Ilość punktów w chmurze - 360 stopniach - zależy od trybu skanowania oraz od ilości obrotów na minutę (ang. RPM, revolutions per minute). Im wolniejsza prędkość obrotu, tym więcej punktów w chmurze. Zalecany przez autora zakres pracy to od 200 do 1023 rpm. Przy mniejszych wartościach niż 200 istnieje ryzyko przekroczenia wartości 8192 punktów na chmurę przez co SDK broni się. Domyśla wartość to 660rpm.

### Pomiary szybkości silnika lidaru

| Software RPM | Measured RPM | Software RPS | Measured RPS | Error  |
| ------------ | ------------ | ------------ | ------------ | ------ |
| 200          | 196.62       | 3.33         | 3.28         | ~1.7%  |
| 400          | 432.02       | 6.67         | 7.20         | ~8.0%  |
| 600          | 684.52       | 10.00        | 11.41        | ~14.0% |
| 800          | 965.14       | 13.33        | 16.09        | ~20.6% |
| 1000         | 1268.98      | 16.67        | 21.15        | ~26.8% |

### Ogólne pomiary rezultatów lidaru

Tryb skanowania: **Sensitivity**

| zadany RPM | całk. czas [s] | punktów | punktów na chmurę | chmur | śr. czas na chmurę [s] | zmierzony RPM |
| ---------- | -------------- | ------- | ----------------- | ----- | ---------------------- | ------------- |
| 200        | 28.369         | 447133  | 4860.14           | 92    | 0.31                   | 194.58        |
| 400        | 28.187         | 444097  | 2198.50           | 202   | 0.14                   | 429.99        |
| 600        | 28.308         | 446794  | 1387.56           | 322   | 0.09                   | 682.49        |
| **660\***  | 28.378         | 448529  | 1274.23           | 352   | 0.08                   | 744.24        |
| 800        | 26.792         | 423121  | 984.00            | 430   | 0.06                   | 962.97        |
| 1000       | 27.327         | 432130  | 748.93            | 577   | 0.05                   | 1266.88       |

\* domyślny

## Serwomechanizm

Serwomechanizm odpowiada za obrót płaszczyzny, która jest skanowana przez lidar. Sterowane jest ono sygnałem PWM za pomocą mikrokontrolera.

Wymaga własnego zasilania. Sygnał PWM nadawany jest przez mikrokontroler.

## IMU

IMU (ang. inertial measurement unit) to urządzenie służące do nawigacji inercyjnej wyposażone w akcelerometr i żyroskop. Układ wykorzystywany przez nas to **MPU-6050** o 6 stopniach swobody (akcelerometr X, Y, Z i żyroskop X, Y, Z). W początkowej fazie rozwoju projektu zauważono, że konstrukcja składająca się z samego lidaru i serwa może być podatna na niedokładności spowodowane tym, że:

- konstrukcja podczas ruchu mogłaby być mniej lub bardziej przechylana w każdą ze stron podczas skanowania,
- wykorzystywany przez nas serwomechanizm ma ograniczoną dokładność.

Oba problemy miały zostać rozwiązane przez IMU, które dostarczałoby w czasie rzeczywistym danych dotyczących aktualnego przechylenia/obrotu płaszczyzny skanowania.

Niestety wyniki z wykorzystujące opisane IMU i metody szacowania obrotu płaszczyzny okazują się jeszcze bardziej niedokładne, niż wykorzystywanie samego lidaru i serwa. Powodów należy szukać w szacowaniu pozycji, które polega na ciągłym aktualizowaniu stanu, opierającego się na poprzednich pomiarach. W ten sposób bardzo szybko rośnie błąd, który sprawia, że dwa skany tej samej sceny mogą mocno różnić się od siebie.

Projekt w wersji finalnej przygotowany jest do pracy **z** jak i **bez** IMU. Dla lepszych rezultatów zalecane jest niekorzystanie z IMU. Jeżeli zamierza się ruszać konstrukcją podczas skanowania, można zdecydować się jego wykorzystanie, chociaż ma się wtedy do czynienia z rosnącym błędem.

### MPU-6050

Podstawową funkcjonalnością urządzenia jest wykorzystywanie 3-osiowego akcelerometru i żyroskopu. W ten sposób otrzymujemy strumień _surowych_ pomiarów składających się z sześciu 2-bajtowych liczb zmiennoprzecinkowych w opisanej w dokumentacji skali. Moduł komunikuje się interfejsem I2C.

[MPU-6050 w bazie i2cdevlib](https://www.i2cdevlib.com/devices/mpu6050#links)

### MPU-9250

Moduł całkowicie kompatybilny z MPU-6050. Różnicą jest posiadanie dodatkowo 3-osiowego magnetometru, który wymaga specjalnej kalibracji. Magnetometr aktualnie nie jest wykorzystywany w projekcie.

### Kalibracja

Kalibracja MPU-6050 polega na ustawieniu go na możliwie płaskiej powierzchni, wykonanie serii pomiarów (po 6 wartości na pomiar), obliczenie ich średniej i zapisanie wyników. Należy też uwzględnić przyspieszenie grawitacyjne, które powinno być wyraźnie widoczne na jednej z osi.

Program _lidar-tools/sync_ wykonuje kalibrację automatycznie przed rozpoczęciem skanowania (jeżeli korzystamy z IMU).

### DMP

Ciekawą częścią MPU jest moduł DMP (Digital Motion Processor), którym chwali się producent, ale jednocześnie oficjalne dokumentacje całkowicie pomijają jego istnienie. W internecie znaleźć można liczne nieoficjalne dyskusje i biblioteki próbujące wykorzystywać jego funkcjonalności. Do jednej z wielu (w tym dalej nieodkrytych) funkcjonalności należy szacowanie obrotu na podstawie _surowych_ danych (obliczanie kwaternionu)

## Mikrokontroler

Wykorzystywany w projekcie mikrokontroler to ATmega328p. Oprogramowanie, które musi się na nim znaleźć znajduje się w repozytorium _lidar-avr_. Odpowiada ono za:

- sterowanie sygnałem PWM w celu kontroli serwomechanizmu,
- komunikacja poprzez I2C z MPU-6050 (lub MPU-9250),
- komunikacja z komputerem operatora (odbieranie/wysyłanie ramek danych).

Na poniższym schemacie znajduje się domyślne połączenie przewodów i elementów projektu (wykorzystana została płytka Arduino UNO, ale mikrokontroler jest programowany bezpośrednio):

TODO

## Głowica

Mechaniczna konstrukcja na której zamontowane są poszczególne elementy projektu.

### Prototyp

### Wersja finalna

Konstrukcja zaprojektowana w programie Autodesk Fusion 360 i wydrukowana w technologii 3D.

# Skanowanie 3D

Skanowania 3D polega na zbieraniu danych z kilku źródeł nie-3D i łączeniu ich w taki sposób, aby otrzymać informację 3D o otoczeniu.

Najważniejszym urządzeniem jest lidar, który po uruchomieniu jest w stanie generować kilka chmur punktów na sekundę. Punkty reprezentowane są w postaci par (kąt, odległość) w jednostkach [stopnie, milimetry].

Kolejnym istotnym elementem jest serwomechanizm. Znana jest zadana przez nas pozycja na jaką ma się ustawić. W tym celu wykorzystywana jest wewnętrzna jednostka, która może zostać przeliczona na stopnie.

Ostatnim (ale opcjonalnym) elementem jest IMU, który dostarczać może pomiary w postaci 3 wartości (x, y, z) akcelerometru, 3 wartości (x, y, z) żyroskopu.

Program **lidar-tools/sync** po uruchomieniu na urządzeniu operatora:

1. tworzy subproces i uruchamia program **lidar-scan**, który łączy się z podłączonym do urządzenia operatora lidarem;
   uruchamia pętlę odbierająca od lidar-scan pomiary **lidaru**,
2. łączy się z mikrokontrolerem, na którym powinien znajdować się program **lidar-avr**.
3. uruchamia pętlę wysyłającą rozkazy do mikrokontrolera sterującą **serwomechanizmem**.
4. uruchamia (opcjonalnie) pętlę odbierająca od mikrokontrolera pomiary **IMU**.

Pomiary IMU i zadane pozycje serwomechanizmu są gromadzone wraz z czasem, w którym miały miejsce. Do każdej odebranej chmury punktów lidaru dobierany jest najlepiej pasujący czasowo pomiar IMU lub zadana pozycja serwomechanizmu. Metoda jaka zostanie obrana zależy od użytkownika (innymi słowy, to użytkownik decyduje, czy wykorzystywać IMU).

Następnie dokonywane są obliczenia, w efekcie których powstaje grupa gotowych punktów. Wypisywane są one na standardowe wyjście (stdout).

### Obróbka surowych pomiarów IMU

MPU-6050 dostarcza sześć 2-bajtowych zmiennoprzecinkowych wartości w każdym _surowym_ pomiarze. Aby zrozumieć dane, można je łatwo zwizualizować na wykresie. Będą one odpowiadały ruchom i obrotom urządzenia.

Ffilm z wizualizacją](https://youtu.be/J4pH3LHojVM)

**Przykładowy wykres:**

<img height=300 src="https://raw.githubusercontent.com/dsonyy/python-stuff/master/accelerometer-live-plot/example.png">

_Surowe_ dane po odebraniu przez _lidar-tools/sync_ są przekazywane estymatora pozycji (ang. attitude estimator), który aktualizowany jest o kolejne wartości. Jako wynik estymator zwraca [kwaternion](https://pl.wikipedia.org/wiki/Kwaterniony) - obiekt matematyczny składającą się z 4 liczb zmiennoprzecinkowych (w, x, y, z), które mogą zostać zinterpretowane jako obrót obiektu.

# Konfiguracja

## Hardware

1. Mikrokontroler musoi być podłączony do urządzenia operatora, aby umożliwić komunikację USART.
2. Serwomechanim musi być połączony do zasilania oraz mikrokontrolera w sposób przedstawiony na schemacie (TODO).
3. IMU (MPU-6050 lub kompatybilne MPU-9250) może być podłączone do mikrokontrolera w sposób przedstawiony na schemacie (TODO - patrz skanowanie 3D).
4. Lidar musi być podłączony do stabilnego źródła zasilania i do urządzenia operatora.

## Software

**Na mikrokontrolerze** musi być zaflashowany program _lidar-avr_.

**Na urządzeniu operatora** musi znaleźć się:

- _lidar-tools/sync_
- _lidar-scan_

Następnie można przystąpić do konfiguracji _lidar-tools/sync_. Wszystkie dostępne parametry programu należy dostrajać korzystając z argumentów wiersza poleceń. Ich liczba może być spora, dlatego wygodnie jest przygotować skrypt, który uruchomi _lidar-tools/sync_ przekazując mu odpowiednie parametry (jak np. _sync.ps1_ znajdujący się w głównym repozytorium projektu _lidar-tools_).

### Parametry _lidar-tools/sync_

| Parametr      | Opis                                                                                                                                               | Uwagi                                   |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| avrport       | port, przez który odbywa się komunikacja z mikrokontrolerem                                                                                        |                                         |
| avrbaud       | baudrate, z którego korzysta mikrokontroler do komunikacji                                                                                         | domyślnie 19200                         |
| lidarexe      | ścieżka do pliku wykonywalnego _lidar-sync_                                                                                                        |                                         |
| lidarport     | port, przez który odbywa się komunikacja z lidarem                                                                                                 |                                         |
| lidarmode     | tryb pracy lidaru                                                                                                                                  | 3 (indoor, domyślnie) lub 4 (outdoor)   |
| lidarpm       | ilość obrotów na minutę lidaru (RPM)                                                                                                               | 200-1023, domyślnie 660                 |
| servostep     | pojedynczy krok serwomechanizmu w jego jednostkach                                                                                                 |                                         |
| servodelay    | odstęp czasowy serwomechanizmu pomiędzy krokami w milisekundach                                                                                    |                                         |
| servomin      | minimalna pozycja serwomechanizmu w jego jednostkach                                                                                               | domyślnie 1000                          |
| servomax      | maksymalna pozycja serwomechanizmu w jego jednostkach                                                                                              | domyślnie 3000                          |
| servocalib    | pozycja serwomechanizmu, dla której płaszczyzna lidaru będzie w możliwie równoległej do ziemi pozycji                                              | domyślnie 2500                          |
| servostart    | pozycja startowa serwomechanizmu do skanowania                                                                                                     | domyślnie 3000                          |
| servounit     | ważna wartość wyznaczona eksperymentalnie, która służy do przeliczenia jednostki serwomechanizmu na stopnie: **1 jednostka serwa = _servounit_ °** | domyślnie około -0.047                  |
| cloudrotation | wszystkie punkty leżące na płaszczyźnie zeskanowanej przez lidar zostaną obrócone o _cloudrotation_ radianów                                       | dla głowicy prototyp: -π/4, (-0.785398) |
| acceluse      | jeżeli prawda to bierze pod uwagę IMU, jeśli fałsz to tylko zadane pozycje serwomechanizmu                                                         | _true_ lub _false_                      |

# Materiały

## Oprogramowanie pomocnicze

Oprogramowanie, które powstało jako pomoc podczas pracy nad projektami. Są to proste programy/skrypty realizujące jedno zadanie.

### accel-read

### accel-plot

### angle-visualization

### pipeline

### [attestimator](https://github.com/knei-knurow/attestimator)

## Przykłady chmur punktów

- [3D (Google Drive)](https://drive.google.com/drive/folders/1JSF53_TLBTgeE407KCZTTn-GNv1g_iZ-?usp=sharing)
- [2D (Google Drive)](https://drive.google.com/drive/folders/1GGNDYH1F7mPqHnHaxzhhpN3W45uAHUO9?usp=sharing)
