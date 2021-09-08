# Lidar 2D to 3D
Projekt polega na stworzeniu i oprogramowaniu urządzenia zdolnego do skanowania otaczającej go przestrzeni w 3D. Do tego celu wykorzystany jest m.in. lidar skanujący płaszczyznę 2D, głowica własnego projektu oraz inne pomocnicze elementy.

# Spis treści

- [Galeria]()
  - [2D]()
  - [3D]()
- [Spis submodułów]()
  - [lidar-tools*]()
    - [sync*]()
    - [servoctl]()
    - [receiver/transmitter]()
    - [scan-dummy]()
  - [lidar-avr*]()
  - [lidar-scan*]()
  - [lidar-vis]()
  - [lidar-visualization]()
  - [lidar-stm32]()

- [Spis elementów]()
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

# Galeria

## 3D

## 2D

# Spis submodułów

W tym repozytorium pod jednym dachem zebrane są repozytoria z przedrostkiem *lidar-* rozwijane w ramach [KNEI](https://github.com/knei-knurow), które mają mniejszy lub większy związek ze skanowaniem 3D. Więcej informacji na każdy z projektów można znaleźć w ich wnętrzu w plikach README.

**Gwiazdka * oznacza repozytoria, które są wymagane do skanowania 3D.** Pozostałe projekty mogą się przydać podczas zabawy ze skanowaniem 2D.

## lidar-tools*

Zbiór *narzędzi* przydatnych podczas pracy z lidarem. 

### sync*

Najważniejsze z *narzędzi*. Do jego zadań należy:

- Ustanowienie połączenia z mikrokontrolerem (który steruje serwem i akcelerometrem) oraz lidarem.
- Synchronizacja danych/pomiarów z dostępnych źródeł.
- Obliczanie punktów chmury 3D.
- Wypisywanie punkt po punkcie (x, y, z) na standardowe wyjście (stdout).

### servoctl

Skrypt pozwalający na wysłanie do mikrokontrolera ramki danych ustawiających serwo na zadanej pozycji.

### transmitter/receiver

Umożliwiają transmisję danych lidaru 2D (uzyskane np. za pomocą *lidar-scan*) poprzez UDP.

### scan-dummy 

Program udający lidar-scan generujący przykładowe dane.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

## lidar-avr*

Oprogramowanie przeznaczone do kompilacji na mikrokontroler AVR Atmega328p, którego zadaniem jest obsługa serwa i akcelerometru oraz komunikacja poprzez USART z urządzeniem operatora. 

Więcej o dokładnej konfiguracji i działaniu w odpowiedniej sekcji tego dokumentu.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

## lidar-scan*

Projekt wywodzący się z *lidar-visualizations.* Pomysł polegał na stworzeniu programu, który specjalizuje się w jednym konkretnym zastosowaniu i robi je dobrze ([Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)).

Zadaniem programu jest ustanowienie połączenia z lidarem oraz wypisywanie na standardowe wyjście (stdout) odebranych danych w formie tekstowej. Docelowo dane mogą być przekazane dowolnemu innemu programowi, który rozumie wejściowy format danych (*lidar-vis, lidar-stream).*

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

Projekt wywodzący się z *lidar-visualizations*. Jest to "siostrzany" program do *lidar-scan –* robi jedną rzecz i robi ją dobrze ([Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)). 

Zadaniem programu jest wyświetlanie danych otrzymanych z lidaru (za pomocą *lidar-scan*) i wyświetlanie ich graficznie.

Zgodny z systemami Linux, macOS, Windows.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy) [Bartek Pacia](https://github.com/bartekpacia)

## lidar-visualizations

Program umożliwia odczyt i wizualizację danych z lidaru w czasie rzeczywistym.

Oprogramowanie kilkukrotnie zmieniło prawie całkowicie swoją formę. Stworzone zostało na potrzeby artykułu do "Elektroniki Praktycznej" w zamian za wypożyczenie od KAMAMI lidaru. Na chwilę obecną nie jest aktywnie rozwijane. Kod składa się z kilku interfejsów, które teoretycznie umożliwiają tworzenie dodatkowych funkcjonalności. Program korzysta z oficjalnego RPLIDAR SDK oraz wysokopoziomowej biblioteki graficznej SFML.

Zgodny z systemami Linux, macOS, Windows.

Więcej informacji można przeczytać w artykule: [Elektronika Praktyczna "Wizualizacja pomiarów skanera LIDAR" (marzec 2021)](https://ep.com.pl/kursy/notatnik-konstruktora/14763-wizualizacja-pomiarow-skanera-lidar)

**Autor:** [Szymon Bednorz](https://github.com/github.com/dsonyy)

## lidar-stm32

Ciekawy projekt, który podobnie jak *lidar-visualizations*, stworzony został na potrzeby "Elektroniki Praktycznej". Uruchamiany jest na płytce STM32, która za pomocą UART wysyła/odbiera dane do/z lidaru, a następnie je wizualizuje. W przeciwieństwie do *lidar-visualizations* nie korzysta z RPLIDAR SDK, które nie jest przystosowane do tego typu urządzeń, tylko z własnych funkcji stworzonych z wzór tych z SDK.

Więcej informacji można przeczytać w artykule: [Elektronika Praktyczna "Wizualizacja pomiarów skanera LIDAR" (marzec 2021)](https://ep.com.pl/kursy/notatnik-konstruktora/14763-wizualizacja-pomiarow-skanera-lidar)

**Autor:** [Bartek Dudek](https://github.com/github.com/doodek)

# Spis elementów

## Lidar

Wykorzystywany w projekcie lidar to [Slamtec RPLIDAR A3](https://www.slamtec.com/en/Lidar/A3Spec). Producent dostarcza także [RPLIDAR SDK](https://github.com/Slamtec/rplidar_sdk) wspierające systemy Windows i macOS, które pozwala na sprawne rozpoczęcie pracy ze sprzętem.

Lidar posiada swoje własne zasilanie, oraz własny przewód USB (do transmisji danych) do urządzenia operatora.

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

| ID   | Scan mode                         | Sample time [us] | Frequency |
| ---- | --------------------------------- | ---------------- | --------- |
| 0    | Standard                          | 252              | 0.484406  |
| 1    | Express                           | 126              | 0.968812  |
| 2    | Boost                             | 63               | 1.93762   |
| 3    | **Sensitivity/Indoor (domyślny)** | 63               | 1.93762   |
| 4    | **Stability/Outdoor**             | 100              | 1.2207    |

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

Podstawową funkcjonalnością urządzenia jest wykorzystywanie 3-osiowego akcelerometru i żyroskopu. W ten sposób otrzymujemy strumień *surowych* pomiarów składających się z sześciu 2-bajtowych liczb zmiennoprzecinkowych w opisanej w dokumentacji skali. Moduł komunikuje się interfejsem I2C.

[MPU-6050 w bazie i2cdevlib](https://www.i2cdevlib.com/devices/mpu6050#links)

### MPU-9250

Moduł całkowicie kompatybilny z MPU-6050. Różnicą jest posiadanie dodatkowo 3-osiowego magnetometru, który wymaga specjalnej kalibracji. Magnetometr aktualnie nie jest wykorzystywany w projekcie.

### Kalibracja

Kalibracja MPU-6050 polega na ustawieniu go na możliwie płaskiej powierzchni, wykonanie serii pomiarów (po 6 wartości na pomiar), obliczenie ich średniej i zapisanie wyników. Należy też uwzględnić przyspieszenie grawitacyjne, które powinno być wyraźnie widoczne na jednej z osi.

Program *lidar-tools/sync* wykonuje kalibrację automatycznie przed rozpoczęciem skanowania (jeżeli korzystamy z IMU).

### DMP

Ciekawą częścią MPU jest moduł DMP (Digital Motion Processor), którym chwali się producent, ale jednocześnie oficjalne dokumentacje całkowicie pomijają jego istnienie. W internecie znaleźć można liczne nieoficjalne dyskusje i biblioteki próbujące wykorzystywać jego funkcjonalności. Do jednej z wielu (w tym dalej nieodkrytych) funkcjonalności należy szacowanie obrotu na podstawie *surowych* danych (obliczanie kwaternionu)

## Mikrokontroler

Wykorzystywany w projekcie mikrokontroler to Atmega328p. Oprogramowanie, które powinno się na nim znaleźć znajduje się w repozytorium *lidar-avr*. Odpowiada ono za:

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

### Dalsza obróbka danych

MPU-6050 dostarcza sześć 2-bajtowych zmiennoprzecinkowych wartości w każdym *surowym* pomiarze. Dane mogą być zwizualizowane na wykresie i odpowiadają ruchom i obrotom urządzenia - [film z wizualizacją](https://youtu.be/J4pH3LHojVM).

<img height=300 src="https://raw.githubusercontent.com/dsonyy/python-stuff/master/accelerometer-live-plot/example.png">

*Surowe* dane następnie są przekazywane estymatora pozycji (ang. attitude estimator), który aktualizowany jest o kolejne wartości. Jako wynik estymator zwraca kwaternion - obiekt matematyczny składającą się z 4 liczb zmiennoprzecinkowych (w, x, y, z), które mogą zostać zinterpretowane jako obrót.

Następnie, płaszczyzny 2D zawierające pomiary (x, y) uzyskane z lidaru są obracane w trzecim wymiarze o obliczony kwaternion. Pomiary lidaru przekształcone względem pomiarów IMU są wtedy gotowe.  

## Hardware - konfiguracja

## Software - konfiguracja

## Parametry skanowania

## Skanowanie

# Materiały 

## Oprogramowanie pomocnicze

Oprogramowanie, które powstało jako pomoc podczas pracy nad projektami. Są to proste programy/skrypty realizujące jedno zadanie.

### accel-read

### accel-plot

### angle-visualization

### pipeline

### [attestimator](https://github.com/knei-knurow/attestimator)

## Chmury punktów

### 3D

### 2D

