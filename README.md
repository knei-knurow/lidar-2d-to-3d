# Lidar 2D to 3D
Projekt polega na stworzeniu i oprogramowaniu urządzenia zdolnego do skanowania otaczającej go przestrzeni w 3D. Do tego celu wykorzystany jest m.in. lidar skanujący płaszczyznę 2D, głowica własnego projektu oraz pomocnicze elementy.

## Spis treści

## Spis submodułów

W tym repozytorium pod jednym dachem zebrane są repozytoria z przedrostkiem *lidar-* rozwijane w ramach [KNEI](https://github.com/knei-knurow), które mają mniejszy lub większy związek ze skanowaniem 3D.

**Gwiazdka (*) oznacza repozytoria, które są wymagane do skanowania 3D.**

### lidar-tools*

Zbiór *narzędzi* przydatnych podczas pracy z lidarem. 

#### sync*

Najważniejsze z *narzędzi*. Do jego zadań należy:

- Ustanowienie połączenia z mikrokontrolerem (który steruje serwem i akcelerometrem) oraz lidarem.
- Synchronizacja danych/pomiarów z dostępnych źródeł.
- Obliczanie punktów chmury 3D.
- Wypisywanie punkt po punkcie (x, y, z) na standardowe wyjście (stdout).

#### servoctl

Skrypt pozwalający na wysłanie do mikrokontrolera ramki danych ustawiających serwo na zadanej pozycji.

#### receiver/transmitter

Umożliwiają transmisję danych lidaru 2D (uzyskane np. za pomocą *lidar-scan*) poprzez UDP.

#### scan-dummy 

Program udający lidar-scan generujący przykładowe dane.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

### lidar-avr*

Oprogramowanie przeznaczone do kompilacji na mikrokontroler AVR Atmega328p, którego zadaniem jest obsługa serwa i akcelerometru oraz komunikacja poprzez USART z urządzeniem operatora. 

Więcej o dokładnej konfiguracji i działaniu w odpowiedniej sekcji tego dokumentu.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)

### lidar-scan*

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

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy), [Bartek Pacia](https://github.com/github.com/bartekpacia)https://github.com/github.com/bartekpacia)

### lidar-vis

Projekt wywodzący się z *lidar-visualizations*. Jest to "siostrzany" program do *lidar-scan –* robi jedną rzecz i robi ją dobrze ([Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)). 

Zadaniem programu jest wyświetlanie danych otrzymanych z lidaru (za pomocą *lidar-scan*) i wyświetlanie ich graficznie.

Zgodny z systemami Linux, macOS, Windows.

**Autorzy:** [Szymon Bednorz](https://github.com/github.com/dsonyy) [Bartek Pacia](https://github.com/bartekpacia)

### lidar-visualizations

Program umożliwia odczyt i wizualizację danych z lidaru w czasie rzeczywistym.

Oprogramowanie kilkukrotnie zmieniło prawie całkowicie swoją formę. Stworzone zostało na potrzeby artykułu do "Elektroniki Praktycznej" w zamian za wypożyczenie od KAMAMI lidaru. Na chwilę obecną nie jest aktywnie rozwijane. Kod składa się z kilku interfejsów, które teoretycznie umożliwiają tworzenie dodatkowych funkcjonalności. Program korzysta z oficjalnego RPLIDAR SDK oraz wysokopoziomowej biblioteki graficznej SFML.

Zgodny z systemami Linux, macOS, Windows.

Więcej informacji można przeczytać w artykule: [Elektronika Praktyczna "Wizualizacja pomiarów skanera LIDAR" (marzec 2021)](https://ep.com.pl/kursy/notatnik-konstruktora/14763-wizualizacja-pomiarow-skanera-lidar)

**Autor:** [Szymon Bednorz](https://github.com/github.com/dsonyy)

### lidar-stm32

Ciekawy projekt, który podobnie jak *lidar-visualizations*, stworzony został na potrzeby "Elektroniki Praktycznej". Uruchamiany jest na płytce STM32, która za pomocą UART wysyła/odbiera dane do/z lidaru, a następnie je wizualizuje. W przeciwieństwie do *lidar-visualizations* nie korzysta z RPLIDAR SDK, które nie jest przystosowane do tego typu urządzeń, tylko z własnych funkcji stworzonych z wzór tych z SDK.

Więcej informacji można przeczytać w artykule: [Elektronika Praktyczna "Wizualizacja pomiarów skanera LIDAR" (marzec 2021)](https://ep.com.pl/kursy/notatnik-konstruktora/14763-wizualizacja-pomiarow-skanera-lidar)

**Autor:** [Bartek Dudek](https://github.com/github.com/doodek)

