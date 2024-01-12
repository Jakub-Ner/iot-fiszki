#iot
## Wprowadzenie do IoT - 01

Czym jest internet Rzeczy?
?
Infrastruktura umożliwiająca łączenie rzeczy (obiektów fizycznych i wirtualnych) w oparciu o technologie informacyjne i komunikacyjne.

Czym jest urządzenie?
?
Sprzęt z obowiązkową możliwością komunikacji i opcjonalnymi czujnikami, elementami wykonawczymi, analizowaniem danych

Wymień rodzaje sieci wchodzące w skład IoT.
?
- Sieci o zasięgu lokalnym:
	- **BAN** - Body Area Network
	- **CAN** - Car Area Network
	- **PAN** - Personal Area Network
- Sieci dalekiego zasięgu:
	- **CAN** - Campus Area Network
	- **HAN** - Home Area Network
	- **LAN** - Local Area Network
	- **MAN** - Metropolitan Area Network
	- **WAN** - Wide Area Network
*UWAGA: Linia podziału nie jest sztywna*

Gdzie można zarządzać danymi?
?
![[Pasted image 20240106173823.png|400]]
- Chmura (**Cloud**) - chmura lub centralne centrum danych, 
- Mgła (**Fog**) - bramy i sieć tranzytowa,
- Krawędź (**Edge**) - w czujnikach.

Jakie urządzenia wyróżniamy w IoT?
?
- Przetworniki
- Czujniki
- Elementy wykonawcze (Actuators) - wpływa na środowisko
- Moduł komunikacyjny
- mikrokontroler
- źródło zasilania

Rozwiń skrót ADC.
?
Analog-Digital-Converter

Wymień podstawowe parametry ADC:
?
- Resolution - liczba bitów
- Precision - stabilność pomiarów
- $V_{REF}$ (napięcie odniesienia - maksymalne) - wewnętrzne / zewnętrzne
- Input scaling - zakres napięcia, jedno-, dwubiegunowość, 
- Prędkość - czas konwersji, opóźnienie

Wymień podstawowe parametry DAC:
?
- Rozdzielczość (Resolution) - liczba bitów.
- Precyzja (Accuracy) - monotoniczność, liniowość, stabilność stałoprądowa.
- Napięcie odniesienia (Reference voltage - VREF) - wewnętrzne lub zewnętrzne.
- Skalowanie wyjścia (Output scaling) - jednobiegunowość lub dwubiegunowość, zakres napięcia.
- Typ wyjścia (Output type) - wyjście napięciowe lub wyjście prądowe.
- Prędkość (SPeed) - czas ustawiania (wyjścia), częstotliwość aktualizacji (wyjścia).

Jak przebiega input scaling dla jedno-wejściowego ADC?
?
Liniowo między GND i $V_{REF}$ w $2^n$ krokach. $Min=0$, $Max=2^n -1$

Jeżeli wartość błędu pomiaru ADC wynosi 1 **LSB**, oznacza to, że:
?
Błąd wynosi $\frac{V_{REF}}{2^n}$

Co jeśli mierzone napięcie jest wyższe od napięcia referencyjnego, to:
?
Zawsze odczytamy maksymalną wartość, którą może podać przetwornik (wartość napięcia zasilania przetwornika musi być większa od referencyjnego)

Zbyt duża różnica między napięciem referencyjnym a mierzonym może spowodować:
?
Ograniczenie dostępnej rozdzielczości.

Wymień źródła pomiaru czujnika.
?
- sygnał cyfrowy, jeśli czujnik jest wyposażony w ADC
- sygnał analogowy, zwykle w postaci napięcia lub prądu odpowiadającego zmierzonej wartości.

Czym jest system wbudowany (Embedded)?
? 
Połączenie sprzętu i oprogramowania (w tym systemu operacyjnego)

## Wprowadzenie do programowania mikrokontrolerów 02

Co zawiera w sobie MCU (microcontroller unit)?
?
- przynajmniej jeden rdzeń procesora 
- pamięć 
- programowalne urządzenia I/O

Jakie wyróżniamy architektury mikrokontrolerów?
?
- **Harvardzka** - osobna pamięć i magistrale dla programu i danych
- **von Neumanna** - wspólna przestrzeń, jest popularniejsza

Rozwiń skrót DSP.
?
Digital signal processing

<span style="color:#ff0000">Czym są endianness?</span>
*Na przykładzie liczby szesnastkowej: 4F 52*
?
Dotyczą one kolejności liczb wielobajtowych w pamięci. Wyróżniamy:
- **big-endian** - najbardziej znaczący bajt (MSB) znajduje się pod najniższym adresem, czyli 4F jest przechowywany w pamięci o indeksie $i$, a 52 na $i+1$
- **little-endian** - najmniej znaczący bajt (LSB)  znajduje się pod najniższym adresem, czyli 4F przechowany w pamięci o indeksie $i+1$, a 52 na $i$

Wymień możliwe w C operacje bitowe.
?
- `~` - operator negacji bitowej, 
- `&` - operator koniunkcji bitowej AND,
- `|` - operator alternatywy bitowej OR, 
- `^` - operator alternatywy rozłącznej XOR, 
- `<<` - operatory przesunięcia bitowego w lewo, 
- `>>` - operatory przesunięcia bitowego w prawo,


Zakładając pozycje cyfr binarnych w bajcie: [7, 6, 5, 4, 3, 2, 1, 0].
Jak ustawić bit na pozycji 5 na wartość 1?
?
```cpp
x |= 32;               // not informative - do not use
x |= 0x20;             // not convenient
x |= 0b00100000;       // not always implemented
x |= (1 << 5);         // use this
```


Zakładając pozycje cyfr binarnych w bajcie: [7, 6, 5, 4, 3, 2, 1, 0].
Jak wyczyścić bit na pozycji 5 do wartości 0?
?
```cpp
x &= 223;              // not informative - do not use
x &= 0xdf;             // not convenient
x &= 0b11011111;       // not always implemented
x &= ~(1 << 5);        // use this
```


Do czego służy `volatile`?
?
Zapewnia, że odczyt danych nie będzie optymalizowany, a wartość zmiennej będzie zawsze odczytywana z adresu pamięci zmiennej lub z rejestru.

## Wprowadzenie do programowania mikrokontrolerów 03

Czym jest **ISP** (In-System-Programming)?
?
Programowanie urządzenia w ramach instalacji całego systemu, a nie osobno każdego komponentu mikrokontrolera. 

Co umożliwia **JTAG** (Joint Test Action Group)?
?
Programowanie wielu urządzeń
![[Pasted image 20231223185029.png|700]]


Inne interface'y: PDI, TPI, UPDI.
?
Nwm czy jest sens


Rozwiń skrót **ALU**.
?
Jednostka Arytmetyczna Logiczna

Czym jest pamięć **Flash**?
?
- Nieulotna, 
- programowalna, reprogramowalna i elektrycznie czyszczona, może zawierać Boot Loader i sekcję programu. Nie da się wyczyścić mniej niż określony blok (kilka) bajtów

Czym jest **SRAM**?
?
Static Random-Access Memory, pamięć ulotna

Czym jest **EEPROM**?
![[Pasted image 20240111224938.png|400]]
?
Electrically Erasable Programmable Read-Only Memory. Podobny do pamięci Flash ale można w nim czyścić pojedynczy bajt. Wolniejszy ale prostszy w użyciu 


Do czego służą **Fusebity**?
?
Pozwalają skonfigurować wybrane funkcje (np watchdog'a) lub parametry pracy mikrokontrolera jeszcze przed uruchomieniem programu z jego pamięci. Trzymane są w pamięci EEPROM. 

Do czego służą **Lockbity**?
?
Pozwalają kontrolować dostęp do obszarów pamięci mikrokontrolera i chronią przed nieautoryzowanym odczytem za pomocą programatora.

Jakiego mikrokontrolera używaliśmy na labach?
?
ATmega328, Arduino Uno

Wymień źródła sygnału zegara.
?
- wewnętrzny oscylator RC (rezystancyjno-pojemnościowy)
	- średnia częstotliwość
	- bardzo niska precyzja
	- często skonfigurowany jako domyślny
- oscylator kwarcowy:
	- najwyższa częstotliwość
	- najwyższa precyzja
- kwarcowy oscylator niskiej częstotliwości
- zewnętrzny sygnał zegara, np z innego mikrokontrolera

Do czego wykorzystuje się **preskaler**?
?
Do zmniejszenia podstawowej częstotliwości zegara, np w celu zmniejszenia zużycia energii

Wymień tryby uśpienia ATmega328.
?
- **Idle** - wyłączenie zegarów dla CPU, RAM, Flash; mikrokontroler budzi się z przerwaniem zewnętrznym lub wewnętrznym (generowanym przez timery, moduły komunikacyjne itp.)
- **ADC Noise Reduction** - wyłącznie zegarów dla CPU, RAM, Flash, modułów komunikacyjnych na czas zbierania pomiaru ADC
- **Power-Down** - wszystkie generowane sygnały zegarowe są wyłączone; wybudzić mogą przerwania zewnętrzne, reset z systemów watchdog i brown-out, przerwanie sygnalizujące zmianę na pinie
- **Power-Save** - jak Power-Down ale z działającym timerem/licznikiem. Wybudzany przez wybrane zdarzenia timer'a
- **Standby** - jak Power-Down ale z działającym oscylatorem
- **Extended Standby** - jak Power-Save ale z działającym oscylatorem

Czym jest reset?
?
Ustawienie początkowych wartości rejestrów I/O. Nie wymaga zegara.

Jakie są źródła resetu?
?
- **Power-on Reset**:
	- po włączeniu zasilania
	- po spadnięciu poniżej poziomu detekcji
- **Brown-out Reset**:
	- gdy niespełniona jest histereza np. $V_{BOT-}$ < $V_{BOT+}$, która eliminuje migotanie sygnału resetowania
	- konfigurowane przez fusebity
**- External Reset**:
	- po przytrzymaniu niskiego poziomu na pinie $\overline{RESET}$  
	- może zostać wyłączony poprzez ustawienie fusebit RSTDISBL.
**- Watchdog System Reset**:
	- po wykryciu blokady (nikt nie kopnął psa od zbyt dawna)
	- włączany i ustawiany za pomocą fusebitów
	- szczególnie zalecany, gdy urządzenie działa przez dłuższy czas bez nadzoru
	- działa również we wszystkich trybach uśpienia

Czym jest oznaczenie $V_{cc}$?
?
System wykrywania napięcia zasilania.

Jak zbyt niskie napięcie może wpłynąć na zapis do EEPROM i co może być rozwiązaniem problemu?
?
Zbyt niskie napięcie może powodować problemy z zapisem i uszkodzić zawartość pamięci. Prawidłowo skonfigurowany BOD (Brown-Out-Detection) eliminuje ten problem.

Czym jest przerwanie?
?
Zasygnalizowana zmiana lub osiągnięcie stanu opisanego przez warunek (np. zmiana stanu na pinie) przerwania. Cechują się priorytetami. Na ich podstawie kontroler CPUINT decyduje, które przerwanie należy obsłużyć, a które musi poczekać. CPUINT ustawia licznik programu, tak aby wskazywał skok do procedury obsługi przerwania (tzw. wektor przerwania). Po zakończeniu procedury, wykonanie programu wznawiane jest od miejsca gdzie zostało przerwane.

Czym jest system zdarzeń (**EVSYS**) i do czego służy?
![[Pasted image 20240111224741.png|700]]
?
Pozwala podsystemom (urządzeniom peryferyjnym) lub programowi komunikować się bezpośrednio (z pominięciem CPU) poprzez konfigurowalną sieć routingu zdarzeń. 

## Wprowadzenie do programowania mikrokontrolerów 04

Czym jest **Timer**?
?
Licznik zliczający od 0 wzwyż, do momentu "przekręcenia" się licznika. Zliczanie jest niezależne od uruchomionego programu. Szybkość zliczania określa się wybierając źródło sygnału taktującego. Oznaczany jako **CNT**

Do czego służy Pulse Width Modulation (**PWM**)?
?
Służy do regulacji urządzenia (np. jasność świecenia diody, prędkość obrotu silnika) poprzez modulację prądu lub napięcia (tzw. zmiana wypełnienia sygnału)
![[Pasted image 20231229142738.png|700]]

Czym charakteryzuje się modulacja PWM z **wykorzystaniem jednego zbocza**?
?
CMPn - Compare register
W0n - Waveform
![[Pasted image 20231229142425.png|700]]

Czym charakteryzuje się PWM w trybie pojedynczego narastania?
?
![[Pasted image 20231229142532.png|700]]


Jak działa **RTC** (Real Time Counter)?
?
RTC zlicza cykle zegarowe w **CNT** (counter register) i porównuje to z period register i **CMP** (compare register). Może generować przerwania i zdarzenia przy porównywaniu lub przepełnieniu. Zazwyczaj działa ciągle - może wybudzać urządzenie


Do czego służy komparator?
?
Do porównania dwóch sygnałów analogowych (napięć)
![[Pasted image 20231229144127.png|400]]

Wymień parametry odchyleń pomiarów - rodzaje błędów:
?
- Błąd przesunięcia (Oﬀset Error),
- Błąd wzmocnienia (Gain Error),
- Nieliniowość skumulowana (Integral Non-Linearity (INL)),
- Nieliniowość różnicowa (Diﬀerential Non-Linearity (DNL)),
- Błąd kwantyzacji (Quantization Error),
- Dokładność bezwzględna (Absolute Accuracy).

Jak wygląda błąd przesunięcia?
?
![[Pasted image 20231229160515.png|400]]

Jak wygląda błąd wzmocnienia?
?
![[Pasted image 20231229160656.png|400]]

Jak wygląda Nieliniowość skumulowana?
?
![[Pasted image 20231229160636.png|400]]

Jak wygląda błąd Nieliniowość różnicowa?
?
![[Pasted image 20231229160722.png|400]]

Na czym polega błąd Błąd kwantyzacji?
?
Każdy pomiar ADC jest obarczony błędem ±0.5 LSB

Czym jest Dokładność bezwzględna?
?
Jest to maksymalne odchylenie od rzeczywistego pomiaru. Idealna wartość to ±0.5 LSB

Rozwiń skrót **AVR**.
?
Automatic Voltage Regulator - utrzymuje wartości na stałym poziomie dla konkretnych wartości prądu

Jaka jest zależność między napięciem a temperaturą?
?
liniowa.

Do czego służy **CRC** (Cyclic Redundancy Check)?
?
Do weryfikacji danych w nieulotnej pamięci mikrokontrolera. Jeśli suma kontrolna obliczona przez CRCSCAN z CRC się nie zgadzają może zostać wygenerowane przerwanie.

Dodatkowe elementy mikrokontrolera:
?
- **RNG** (Random Number Generator)
- akcelerator sprzętowy AES


## Wyświetlacze LED i LCD, programowalne diody LED RGB 05

Co jest rolą przełącznika?
?
Zamykanie / otwieranie obwodu.

Jakie są rodzaje przełączników?
?
- single-pole single-throw
- single-pole double-throw
- double-pole double-throw
- normally open
- normally close
  ![[Pasted image 20231229163820.png|400]] ![[Pasted image 20231229165423.png|400]]

Czym jest potencjometr?
?
Trójwyprowadzeniowym rezystorem - dzielnikiem napięcia. Położenie trzeciej elektrody reguluje się przez obrót osi lub przesunięcie suwaka. Dostarcza sygnału analogowego
![[Pasted image 20231229170404.png|700]]

Jaka jest przewaga enkodera nad potencjometrem?
?
Enkoder dostarcza sygnału, który może być traktowany jako cyfrowy, dzięki temu nie wymaga przetwornika ADC. Jednak programista musi obsłużyć zdarzenia związane ze zmianą stanów wyjść enkodera.
![[Pasted image 20231229171020.png|500]]
*Enkoder Kwadraturowy*

Czym jest buzzer?
?
Płytka piezoelektryczna (buzzer pasywny) z ewentualną obudową i elektroniką do jego obsługi (aktywny)


Czym jest LED?
?
To dioda elektroluminescencyjna, półprzewodnik, który emituje światło, gdy przepływa przez nie prąd (~1.5V - kolor czerwony, ~3.5V niebieski lub biały)

Porównaj diodę matową i przeźroczystą.
?
W matowej światło jest rozproszone - jednakowo świeci pod różnymi kątami widzenia, ale za cenę jasności.
![[Pasted image 20231229175917.png|200]]


Jak zamontować diodę LED do mikrokontrolera?
?
Nie można podłączyć bezpośrednio. Mogłoby to spowodować uszkodzenie urządzenia, przez nadmierny prąd płynący przez diodę. Należy użyć odpowiednio dobranego rezystora. W przypadku diod LED dużej mocy powinny być montowane na radiatorze - zapewni on rozpraszanie ciepła.

Czym jest współczynnik wypełnienia przebiegu elektrycznego?
?
Pozwala regulować średnie natężenie prądu. Jest to cykl PWM (?)



Opisz zasadę działania wyświetlacza LCD.
?
![[Pasted image 20231230123015.png]]


## Sensory, elementy sygnalizacyjne i wykonawcze 06

Czym jest przetwornik?
?
Urządzenie przetwarzające energię (elektryczną lub nie) w inną (elektryczną lub nie) 

Jak dzielimy czujniki (taksonomia)?
?
- aktywne / pasywne - Czy emitują energię i wymagają zewnętrznego źródła?
- inwazyjne / nieinwazyjne - Czy jest częścią środowiska, które mierzy? Jeśli tak, to inwazyjny
- kontaktowe / niekontaktowe - Czy wymagają kontaktu fizycznego?
- bezwzględne / względne - Czy mierzą w skali absolutnej?
- obszar zastosowań - Gdzie są używane?
- mechanizm pomiaru, np termoelektryczny, elektromechaniczny
- mierzone zmienne


Wymień rodzaje czujników temperatury.
?
- oporowe czujniki temperatury,
- termistory NTC i PTC,
- termopary,
- termostaty,
- czujniki w postaci układów scalonych z wyjściem analogowym i cyfrowym,

Czujniki ciśnienia, wilgotności, optyczne, odległości (ultradźwiękowy), położenie (enkoder absolutny + kody Gray'a) i inne :: wykład 6


Podaj przykłady elementów sygnalizacyjnych.
?
- dźwiękowe:
	- syrena
	- buczek
	- dzwonek
- świetlne:
	- lampa sygnalizacyjna
	- wieża świetlna


Do czego służą elementy załączające (element wykonawczy)?
?
Umożliwiają mikrokontrolerom sterowanie urządzeniami pobierającymi większą moc od nich samych.


Do czego służy tranzystor?
?
Do wzmacniania i przełączania sygnałów elektronicznych i energii elektrycznej
![[Pasted image 20240102143312.png|400]]


Do czego służy tyrystor?
?
Do kontroli przepływu prądu. Jako przełącznik - małym prądem może kontrolować znacznie większe napięcie i prąd
![[Pasted image 20240102143653.png|400]]


Jak działa podstawowy silnik elektryczny?
?
pole magnetyczne silnika wchodzi w interakcję z prądem elektrycznym, generując siłę w postaci momentu obrotowego przykładanego na wał silnika

Jak mogą być zasilane silniki?
?
- prądem stałym (AC): 
	- akumulatory
	- prostowniki
	- pojazdy silnikowe
- prądem przemiennym (AC):
	- sieć energetyczna
	- falowniki
	- generatory elektryczne
![[Pasted image 20240102145244.png|700]]


Jaka właściwość silnika krokowego powoduje, że jest wykorzystywany tam gdzie wymagana jest precyzja (np druk 3d)?
?
Silnik krokowy dzieli pełny obrót na kilka kroków. Pozwala to wymusić i przytrzymać pozycję silnika bez czujników położenia i sprzężenia zwrotnego
![[Pasted image 20240102150234.png|400]]



Czym jest Serwomechanizm?
?
Mały, tani siłownik używany do sterowania radiowego i robotyki na małą skalę
![[Pasted image 20240102150643.png|400]]


## Interfejsy komunikacji lokalnej i magistrale urządzeń Internetu Rzeczy 07


Czym jest **GPIO** (General Purpose Input Output)?
?
Pin, którego zachowanie jest kontrolowane przez użytkownika w czasie wykonywania programu.



W jaki sposób dane są przesyłane przez post szeregowy (**Serial**)?
?
Po jednym bicie na raz.

Co jest charakterystyczne dla komunikacji szeregowej na poziomie TTL?
?
Napięcie jest między GND (0) a $V_{CC}$ (1), które wynosi zazwyczaj 5 V lub 3.3 V.

<span style="color:#ff0000">Opisz istotniejsze linie elektryczne portu szeregowego (<strong>TxD</strong>, <strong>RxD</strong>, <strong>GND</strong>).</span>
?
- **TxD** (Transmitted Data) - przenosi dane z **DTE** (Data Terminal Equipment) do **DCE** (Data Communication Equipment)
- **RxD** (Received Data) - przenosi dane z **DCE** do **DTE**
- **GND** - Wspólna masa elektryczna

Jakie wyróżniamy parametry portu szeregowego?
?
- **prędkość**:
	- prędkość portu i urządzenia muszą być zgodne
	- niektóre systemy automatycznie wykrywają prędkość
- **bity danych** - endianness (LSB lub MSB) muszą być zgodne
- **parzystość** - do wykrywania błędów transmisji, do znaku danych wysyłany jest dodatkowy bit, tak aby suma bitów była zawsze parzysta (**E**ven) lub nieparzysta (**O**dd)
- **bity stopu** - do synchronizacji, na końcu znaku umieszczają 
![[Pasted image 20240104002532.png|800]]



Czym jest magistrala **UART**?
![[Pasted image 20240109112411.png|400]]
?
Universal Asynchronous Receiver-Transmitter - serial asynchroniczny, czyli taki, który nie musi współdzielić sygnału zegarowego do synchronizacji nadajnika i odbiornika. Synchronizacja polega na identyfikacji początku transmisji każdego bajtu w przewodzie. Gdy nie ma transmisji, magistrala jest w stanie bezczynności. Jest to przykład pełnego dupleksu.
![[Pasted image 20240104143133.png|700]]


Rozszyfruj poniższe ustawienia:
1. 115200-8-N-1
2. 38400-8-O-2
?
1. szybkość 115,2 Kb/s bez parzystości z jednym bitem stopu
2. szybkość 38400 z ustawieniem parzystości na Odd (O) z dwoma bitami stopu

Opisz magistralę SPI.
![[Pasted image 20240109112618.png|400]]
?
Serial Peripheral Interface - serial w którym (master) współdzieli magistralę z niewolnikami. Wybiera do kogo będzie inicjował komunikację poprzez protokół Select-Slave (SS ![[Pasted image 20240104144447.png|28]]). Niewolnicy nie mogą wysyłać danych jeśli pan/i nie spyta. Jest to przykład pełnego dupleksu.

Opisz rolę portów Serial Peripheral Interface (SPI):
![[Pasted image 20240104144601.png|700]]
?
- GPIO - inicjacja i kończenie komunikacji
- MOSI - Master Output Slave Input
- MISO - Master Input Slave Output
- CLK - sygnał zegarowy, może być podtrzymany przez wysyłanie fałszywych bajtów przez MOSI, które są ignorowane przez niewolnika



Do czego służy magistrala Inter-Integrated Circut?
![[Pasted image 20240104152124.png]]
?
Do połączenia wielu mikrokontrolerów i urządzeń podrzędnych na tej samej magistrali. Jest to magistrala półdupleksowa - dwa kierunki przepływu współdzielą ten sam sygnał, innymi słowy może być kilka urządzeń nadrzędnych (pań/panów).
- **SDA** - Serial Data
- **SCL** - Serial Clock

Czym jest **USB**?
?
Universal Serial Bus - protokół działający w trybie host-device, z jednym kierunkiem komunikacji (host -> device). Transceiver (odbiornik/nadajnik) może pracować w obu trybach - on-the-go (**OTG**).


Co jest wyjątkowe w magistrali Dallas-Maxim 1 Wire?
?
Pozwala na komunikację (single-master, multi slave) ze zdalnym urządzeniem za pomocą tylko jednego przewodu! W praktyce wykorzystuje się dwa lub trzy xd
![[Pasted image 20240104155959.png|700]]


czym magistrala **CAN** (jest Controller Area Network)
![[Pasted image 20240104160042.png|700]]
?
Półdupleksowa, multi-master, multi-slave, asynchroniczna szeregowa magistrala


Wymień warstwy sieci (modele ISO/OSI i TCP/IP)
![[Pasted image 20240104162126.png|700]]


## Technologie bezprzewodowe dla Internetu Rzeczy 08


Czym jest Sensor and Actuators Network (SANETs)?
?
Sieć czujników i urządzeń wykonawczych komunikujących się ze sobą, np inteligentne domy. 
- Zalety:
	▶ Łatwość wdrożenia
	▶ Skalowalne
	▶ Elastyczne projektowanie/dynamiczna topologia
- Wady:
	▶ Ograniczone bezpieczeństwo
	▶ Ograniczone prędkości i zakresy transmisji
	▶ Środowisko ma wpływ


Podaj wzór na długość fali.
?
#### $\lambda = \frac{v}{f}$
gdzie:
- $\lambda$ - długość fali
- $v$ - prędkość
- $f$- częstotliwość


Większe anteny 
-> niższe częstotliwości 
	-> większe długości fal 
		-> większy zasięg

Czym cechują się praca na wyższych częstotliwościach?
?
- krótszymi falami
- większą ilością transmitowanych danych
- mniejszymi antenami
- krótszym zasięgiem działania (szczególnie w terenach zurbanizowanych)

Czym się charakteryzują dłuższe fale elektromagnetyczne?
?
- transmitują mniej danych
- lepiej penetrują ściany
- spory zasięg przy niewielkiej mocy nadajnika





Wymień parametry komunikacyjne transmisji bezprzewodowej.
?
- zasięg:
	- krótki (< 100 m) np.:
		- IEEE 802.15.1 Bluetooth
		- IEEE 802.15.7 Visible Light Communications (pilot do TV)
	- średni (< 1 km):
		- IEEE 802.11 WiFi
		- IEEE 802.15.4
		- IEEE 802.15.4g WPAN
		- *technologie przewodowe takie jak Ethernet i Narowband Power Line Communications (PLC) też się klasyfikuje jako średniego zasięgu*
	- daleki (1 km):
		- 2G, 3G, 4G
		- niektóre zastosowania WiFi oraz Low-Power Wide-Area
- pasma częstotliwości:
	- regulowane przez International Telecommunication Union (ITU)
	- nielicencjonowane
	- licencjonowane
- Rodzaj zasilania:
	- zasilane bezpośrednio
	- zasilane bateryjnie (większa mobilność, ale problematyczna wymiana baterii lub jej niemożność)
- topologia:
	- gwiazda (star), np telefon i słuchawki, głośnik
	- peer-to-peer (P2P)- każdy z każdym (w określonym zasięgu) się komunikuje
	- siatka (mesh) - specjalny rodzaj P2P 
- ograniczone węzły:
	- klasa 0:
		- prymitywne urządzenia, podobne do czujników (niezabezpieczone, przesyłają dane do proxy lub bram)
	- klasa 1:
		-  dość ograniczone pamięciowo i obliczeniowo, ale są w stanie korzystać z prostych protokołów np CoAP, IP
	- Klasa 2:
		- ograniczone ale są w stanie obsługiwać większość serwerowych protokołów
![[Pasted image 20240104230910.png]]


Opisz protokół IEEE 802.**15.4.**
?
To technologia dostępu bezprzewodowego do urządzeń o niskiej przepustowości, zasilanych lub zasilanych bateryjnie. Dane są odbierane i przesyłane przez warstwę fizyczną MAC. Wykorzystuje AES. 
Przykłady użycia:
- automatyka domowa i budowlana
- sieci w przemyśle samochodowym
- zabawki interaktywne i zdalnie sterowane

Wymień stosy protokołów bazujące na 802.**15.4**.
?
- ZigBee 
- 6LoWPAN
- WirelessHart
![[Pasted image 20240112142245.png|400]]

Opisz IEEE 1901.2a.
?
Jest to technologia przewodowa wąskopasmowa w linii zasilającej NB-PLC (Narrowband Power Line Communication). Ma duży zasięg i odporność na zakłócenia na tych samych przewodach, które przewodzą energię elektryczną. 
Przykłady użycia:
- automatyzacja dystrybucji
- oświetlenie publiczne
- stacje ładowania pojazdów elektrycznych
- energia odnawialna


Opisz IEEE 802.**11ah**.
![[Pasted image 20240112141600.png|400]]
?
Wykorzystywana w sieciach bez ograniczeń. Służy do podłączania punktów końcowych (np węzłów obliczeniowych (mgły)), czujników o dużej szybkości transmisji danych oraz urządzenia do analizy audio i wideo. Przykłady użycia:
- czujniki i mierniki obejmujące inteligentną siatkę
- agregacja przez sieć dosyłową (backhaul)
- Wi-Fi o zwiększonym zasięgu


Czy WiFi obsługuje pasma poniżej 1 GHz?
?
Nie


Modulacja LoRa opiera się na modulacji rozproszonego widma. W wyniku tego prędkość transmisji jest niska. Gdzie tu korzyść?
?
Znaczne zwiększenie odległości komunikacji. Bo $\lambda = \frac{v}{f}$, a: 
`niższe częstotliwości` -> `większe długości fal` -> `większy zasięg`
LoRaWAN osiąga częstotliwości sub-GHz (poniżej 1 GHz)

Do czego służy algorytm **ADR** (Adaptive Data Rate)?
?
Do zarządzania szybkością transmisji danych i sygnału radiowego. Zapewnia, że wydajność sieci jest obtymalna.


Opisz topologię LoRaWAN
?
![[Pasted image 20240105000801.png]]


## Protokół IP w warstwie sieciowej Internetu Rzeczy 09


Wymień zalety protokołu IP (jest ich 8).
![[Pasted image 20240111234301.png|400]]
?
1. Otwarty i oparty na standardach
2. Wszechstronny
3. Wszechobecny, bo *'Warstwowa architektura IP jest dobrze przygotowana, aby poradzić sobie z każdym rodzajem warstw ﬁzycznych i łącza danych'*
4. Skalowalny
5. Zarządzalny i bezpieczny
6. Stabilny i odporny, istnieje już 30 lat i jest zajebisty (również w sektorach finansowych i obronnych)
7. Przyjęty na rynku konsumenckim
8. Jest czynnikiem zwiększającym innowacyjność

Czym są adaptacja 🤡 i adopcja 🐶 w kontekście IP?
![](https://www.youtube.com/watch?v=nvSKfN6_6eM)
?
- **adaptacja** - implementacja bramy warstwy aplikacji, aby zapewnić translację między warstwami innymi niż IP oraz IP
- **adopcja** - zastąpienie wszystkich warstw innych niż IP ich odpowiednikami IP, upraszczając model wdrażania i operacje

Kiedy adoptować a kiedy adaptować?
?
W przypadku bardzo ograniczonych zasobowo urządzeń adaptacja. W pozostałych adopcja.

Jakie nowości wprowadza IPv6?
![[Pasted image 20240112000938.png|400]]
?
![[Pasted image 20240112003842.png]]

| cecha                                                                                                                                       | IPv4                                 | IPv6      |
| ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | --------- |
| adresowanie                                                                                                                                 | 32 bity                              | 128 bitów |
| nagłówek zoptymalizowany do przetwarzania                                                                                                   | 32 b                                 | 64 b      |
| rozmiar nagłówka                                                                                                                            | 20 B                                 | 40 B      |
| nagłówek Internet Header Length (**IHL**)                                                                                                   | <span style="color:#ff0000">X</span> | ✔️        |
| flow label - pakiety które są częścią tego samego strumienia, mają tę samą etykietę i są łatwo rozpoznawalne bez wchodzenia w ich zawartość | <span style="color:#ff0000">X</span> | ✔️        |
| ...                                                                                                                                         | TTL                                  | Hop limit |
| długość source Address i destination adress                                                                                                 | 32 b                                 | 128 b     |
| wymagana wielkość obsługi pakietu                                                                                                           | 68 B                                 | 1280 B    |
| optymalizacja nagłówka                                                                                                                                            | <span style="color:#ff0000">X</span>                                     | ✔️          |


Gdzie umieszczana jest warstwa adaptacyjna (między którymi warstwami)?
?
![[Pasted image 20240112130337.png|400]]
Jaki protokół opisuje w jaki sposób enkapsulowany jest IPv4 w ramce Ethernet? A jaki mówi o IPv6?
- RFC 894
- RFC 2464
?
- RFC 894 - IPv4
- RFC 2464 - IPv6

Czym jest 6LoWPAN?
?
Warstwa adaptacyjna zoptymalizowana pod kątem transmisji IPv6 stworzona dla ograniczonych węzłów.
![[Pasted image 20240112130947.png|400]]

Czym jest opcja ustalania osiągalności i przesyłania pakietów "mesh-under"?
?
W niej routing jest obsługiwany w warstwie adaptacyjnej 6LoWPAN

Czym jest opcja ustalania osiągalności i przesyłania pakietów "mesh-over" ("route-over")?
?
W niej routing IP dostarcza pakiety do miejsca docelowego

Jak działa IPv6 routing Protocol for Low Power and Lossy Network (**RPL**)?
?
Każdy węzeł działa jak router i staje się częścią sieci (mesh). Routing odbywa się w warstwie IP. Każdy węzeł sprawdza odebrany pakiet i określa miejsce docelowe następnego przeskoku. żadne informacje z warstwy MAC nie są potrzebne, dlatego nazwa mesh-over-routing.
Aby poradzić sobie z ograniczeniami pamięciowymi i obliczeniowymi stosowane są dwa tryby:
- **z przechowywaniem** - wszystkie węzły zawierają pełną tablice routingu RPL, każdy wie, jak bezpośrednio dotrzeć do każdego węzła
- **bez przechowywania** - tylko graniczne routery zawierają pełną tablicę routingu. Pozostałe posiadają tylko adresy rodziców 


Na czym polega acykliczność RPL?
?
RPL opiera się na skierowanym grafie acyklicznym zorientowanym na miejsce docelowe (DODAG) - z dowolnego wierzchołka nie można podążać wzdłuż łuków z powrotem do tego samego punktu. Dodatkowo miejsce docelowe występuje na routerze granicznym jako root DODAG . 
![[Pasted image 20240112132707.png|400]]


Ilu rodziców ma węzeł w DODAG?
?
Trzech. Zapewniają oni ścieżkę do korzenia. Zazwyczaj jeden z rodziców jest preferowany.

Jak są konfigurowane trasy w IPv6 routing Protocol for Low Power and Lossy Network (RPL)?
![[Pasted image 20240112133500.png|400]]
?
Trasy w górę są wykrywane i konfigurowane za pomocą DAG Information Object (**DIO**). Mówią one węzłom, kto jest ich rodzicem i określają najlepszą ścieżkę do katalogu głównego DODAG. Węzły ustalają trasy w dół ogłaszając swoich rodziców za pomocą Destination Advertising Object (**DAO**) - komunikaty te informują rodziców o obecności dzieci
![[Pasted image 20240112133636.png|400]]

Jak działa funkcja celu (**OF**) RFC 6719 minimalnej oczekiwanej liczby transakcji (**METX**)?
?
Rodzice pakują wartość **METX** do DIO i dziecko wybiera minimalną wartość (najlepszego rodzica)

Czym jest ranga w DODAG?
![[Pasted image 20240112133636.png|400]]
?
Jest przybliżeniem tego jak blisko węzeł jest od roota i pomaga uniknąć problemu zliczania w nieskończoność. Węzły mogą:
- zwiększyć swoją rangę tylko po otrzymaniu **DIO** z większym numerem wersji. 
- obniżyć rangę, o ile ustaliły tańszą trasę

Jakie są dostępne metryki dla RPL (jest ich 8)?
?
1. **Expected Transmission Count (ETX)**: Przypisuje wartość dyskretną liczbie transmisji, których wykonania oczekuje węzeł w celu dostarczenia pakietu.
2. **Hop Count**: Śledzi liczbę węzłów przechodzących w ścieżkę. Zazwyczaj ścieżka o niższej liczbie przeskoków jest bardziej preferowana od ścieżki o wyższej liczbie przeskoków.
3. Latency: Różni się w zależności od oszczędzania energii. Preferowane są ścieżki o niższym opóźnieniu.
4. **Link Quality Level**: Mierzy niezawodność łącza, biorąc pod uwagę poziomy błędów pakietów spowodowane czynnikami takimi jak tłumienie sygnału i interferencje.
5. **Link Color**: Umożliwia ręczny wpływ przez administracyjne na routing poprzez ustawienie wartości, aby łącze było mniej lub bardziej pożądane. Wartości te można dostosować statycznie lub dynamicznie do określonych rodzajów ruchu.
6. **Node State and Attribute**: Identyﬁkuje węzły, które działają jako agregatory ruchu i węzły, na które wpływ mają duże obciążenia. Wysokie obciążenia mogą wskazywać na węzły, które miały wysoki stan obciążania procesora lub pamięci. Oczywiście węzły będące agregatorami są preferowane w porównaniu z węzłami mocno obciążonymi.
7. **Node Energy**: Pozwala unikać węzłów o niskiej mocy, więc można uniknąć węzła zasilanego bateryjnie, w którym brakuje energii, i żywotność tego węzła i sieci można wydłużyć.
8. **Throughput**: Podaje wielkość przepustowości łącza węzła. Często węzły oszczędzające energię wykorzystują mniejszą przepustowość. Ta metryka umożliwia ustalanie priorytetów ścieżek o wyższej przepustowości.

## Protokoły aplikacyjne w Internecie Rzeczy 10

UWAGA :: W Wykładzie 10 określenie sensor odnosi się również do elementów wykonawczych

Wymień podobieństwa między sensorem a elementem wykonawczym.
?
- oba odbierają i wysyłają dane
- mają pewien stopień autonomii
- mogą przyjmować polecenia dot. aktualizacji firmware'u

Czy sensory mogą się komunikować z serwerem?
?
Szyfrowana implementacja protokółu TCP/IP lub UDP jest ciężka (objętościowo i obliczeniowo). Dodatkowo byłoby to raczej bez sensu, głupie pytanie.  
![[Pasted image 20240105010104.png|700]]
![[Pasted image 20240112003542.png]]

| Transmission Control Protocol                                                                                     | User Datagram Protocol                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| wymaga nawiązania i utrzymania sesji (analogiczne do rozmowy telefonicznej)                                       | nie ma gwarancji dostawy (wysłanie listu)                                                                                 |
| dodaje 20 bajtów ramki                                                                                            | dodaje tylko 8 bajtów ramki                                                                                               |
| sieci o niskiej mocy i stratne (Low-Power and Lossy-Network) mogą sobie nie radzić w przypadku dużej liczby sesji | większość protokołów aplikacji przemysłowych było wdrażane gdy łącza były zawodne, dlatego TCP/IP jest tam popularniejszy |
|                                                                                                                   | transmisja mutlicast wykorzystuje UDP                                                                                                                           |
`
Wymień metody transportu aplikacji IoT.
?
- **UDP**
- **TCP/IP**
- Brak protokołu - transport przebiega na niższych warstwach
- Supervisory Control and Data Acquisition (**SCADA**) - najpopularniejszy protokół przemysłowy, bardzo stary, ale przystosowany do sieci IP
- Protokoły internetowe - Ethernet, WiFi, 4G/LTE
- Constrained Application Protocol (**CoAP**)
- **MQTT**


Czy sensor może być serwerem?
?
Jeszcze jak, oczywiście w uproszczonej formie, bez HTTP

Jakie protokoły znajdują w stosie pod CoAP i MQTT?
?
![[Pasted image 20240105012752.png|700]]



Opisz **CoAP** (Constrained Application Protocol).
?
Umożliwia komunikacje punkt-punkt *(nie mylić z peer-to-peer)* za pośrednictwem UDP. Taki niskoenergetyczny i odporniejszy na straty HTTP - umożliwia przesyłanie dokumentów i jest kompatybilny z RESTful. Standardy dojrzewają.
![[Pasted image 20240105014416.png|400]]



Opisz Message Queueue Telemetry Transmission.
?
Jest to pewnego rodzaju kolejka* w której pośredniczy broker - do niego publisher wysyła nowe wiadomości, by ten przesłał je do subskrybentów.
W tradycyjnej kolejce dodawane są nowe elementy, w MQTT dla danego tematu nowe elementy zastępują stare. Nowe tematy można tworzyć na bieżąco.
![[Pasted image 20240105014557.png|400]]


Tematy w MQTT są hierarchiczne. W jaki sposób?
?
Są podobne do systemu plików np `id-pojazdu/silnik/olej/temperatura
Subskrybent może łatwo subskrybować temat z jego wszystkimi pod-tematami (używając `#`) lub użyć `+`, żeby subskrybować temat dla dla wszystkich pod-tematów np `id-pojazdu/+/olej/temperatura`


Dla komunikacji MQTT można określić Quality of Services (**QoS**). Opisz je.
?
- QoS-0 - niepotwierdzona transmisja
- QoS-1 - potwierdzona przez odbiorcę (domyślny tryb)
- QoS-2 - potwierdzona przez nadawcę i odbiorcę 


Do czego służy Last Will and Testament (**LWT**)
![[Pasted image 20240106164738.png|400]]
?
Jest to komunikat o stanie i celu (w tym opublikowanych poleceniach i subskrypcjach) przechowywany przez brokera. 
Po utracie połączenia z publisherem, broker powiadamia wszystkich subskrybentów wysyłając LWT


Wymień zalety i wady MQTT.
?
- zalety:
	- dowolny typ danych
	- niezawodność (QoS-1 i QoS-2)
	- skalowalność - publisher nic nie wie o subskrybentach, zna tylko brokera
	- niezależność czasowa (asynchroniczność) - publisher wysyła nie przejmując się subskrybentami, broker podmienia stare wiadomości na nowe, subskrybenci przeglądają nowe wiadomości, kiedy chcą
	- bezpieczeństwo (o ile włączone TLS/SSL)
	- dwukierunkowość - urządzenie może być zarówno publisherem jak i subskrybentem
	- dojrzałość - pierwsza wersja wyszła w 1999
- wady
	- protokół TCP
	- obciążony broker
	- broker jako bottleneck - bez niego nie ma komunikacji
	- bezpieczeństwo - domyślnie TLS/SSL jest wyłączone 

Podsumowanie CoAP vs MQTT.
?
![[Pasted image 20240106170045.png|700]]

## Architektura i projektowanie IoT 11

Opisz architekturę oneM2M (machine-to-machine).
?
![[Pasted image 20240106172529.png|700]]


Sieć FAN?
?
F** Area Network

Opisz warstwy ustandaryzowanej architektury IoT World Forum (IoTWF).
![[Pasted image 20240106173010.png|700]]
?
![[Pasted image 20240106173020.png|700]]


Czym są Edge (mist), Fog, Cloud w kontekście przetwarzania danych?
?
![[Pasted image 20240106175615.png]]


## Pozyskiwanie, gromadzenie i analiza dużych ilości danych 12


Czym są dane ustrukturyzowane?
?
Są to dane zgodne z określonym modelem (np bazodanowym lub formatem (temperatura, wilgotność, ciśnienie, itd.))

Czym są dane nieustrukturyzowane?
?
Nie posiadające logicznego schematu: mowa, obrazy, wideo. Te dane stanowią ok 80% danych biznesowych. Wymagają bardziej wyrafinowanych narzędzi analizy (ML/DL/AI)

Czym są dane w spoczynku a czym w ruchu?
?
- W spoczynku  - dane zapisywane na dysku twardym, a jeśli są przetwarzane to mówimy o przetwarzaniu wsadowym
- w  ruchu - dane przechodzące do miejsca docelowego (np mail lub dane z czujników), a jeśli są przetwarzane - transmisja strumieniowa


Istnieją 4 rodzaje wyników analizy danych. Opowiedz o nich.
?
- opisowa - co się *w silniku*? - np termometr w samochodzie co sekundę podaje wartość
- diagnostyczna - Dlaczego *silnik się zepsuł*? 
- predykcyjna - Jaka szansa ponownego wystąpienia?
- preskryptywna - Jak rozwiązać problem?

Czym różni się supervised od unsupervised learning?
![[Pasted image 20240108230646.png|700]]
?
- supervised - jabłka i banany są oznaczone, model tylko musi zauważyć różnicę by być w stanie je rozróżnić i powiedzieć co jest czym
- unsupervised - model musi zauważyć, że są obiekty podobne i znacząco różne od siebie. Z tego można wywnioskować, że coś jest A a coś B  

Które warstwy IoT są zaangażowane w uczenie lokalne a które w uczenie zdalne?
?
- lokalne - krawędź, brama (węzeł mgły)
- zdalne - chmura

Jakie są 4 główne domeny ML (w IoT)?
?
▶ monitorowanie,
▶ sterowanie zachowaniem,
▶ optymalizacja operacji,
▶ samoregulacja, samooptymalizacja

Wymień 3 V Big Data.
?
- Velocity - szybkość napływania / analizy danych
- Variety - różnorodność danych
- Volume - ilość danych

Jakie bazy danych się wykorzystuje w IoT?
?
- Massively Parallel Processing (**MPP**) - dane są przetwarzane równolegle w wielu procesorach i węzłach, ponadto często mają wbudowane funkcje analityczne.Jeden węzeł (tzw. główny) jest odpowiedzialny za koordynację przechowywania i przetwarzania danych. Dane są przechowywane w formacie ala SQL
- Not only SQL (**NoSQL**)- może przechowywać dane zarówno ustrukturyzowane (w postaci JSON'ów, bazy klucz-wartość, bazy grafowe (wskazanie relacji między danymi)) jak i nieustrukturyzowane
- Hadoop - framework zarządzania i analizy danych. Przykładowe projekty wchodzące w jego ekosystem:
	- KafKa - budowanie potoków danych i aplikacji do streamowania
	- Spark - silnik obliczeniowy dla danych Hadoop
	- Storm - rozproszony system obliczeniowy min. do nieograniczonych strumieni danych
	- Flink - rozproszony silnik do obliczeń stanowych w nieograniczonych i ograniczonych strumieniach danych

Czym jest Lambda?
![[Pasted image 20240110105606.png|700x500]] ![[Pasted image 20240110110126.png|700x500]]
?
Architektura umożliwiająca korzystanie z danych wsadowych (z dysku) i strumieniowych. Poza tym, że jest magazynem danych, jest też mediatorem między tymi danymi a odbiorami danych.

Opisz cykl zarządzania danymi
- pobieranie danych (z czujników)
- przygotowanie danych - normalizacja itd
- analiza (ML)
- raportowanie, wizualizacja, alarmy

## Bezpieczeństwo i prywatność

Opisz Mirai (atak, nie postać z anime)
![[Pasted image 20240109105913.png|400]]
?
DDOS wyprowadzony z botnetu (zainfekowanego sprzętu z Linuxem)
1. Skanowanie: badanie losowych IPv4 w szczególnośći portów 23 i 2323 (telnet TCP). W przypadku sukcesu umieszczanie czarnej listy adresów IP, których należy unikać
2. nawiązanie sesji Telnet z ofiarą: logowanie brute force  
3. infekcja: 
	1. identyfikacja systemu i instalacja malware'u
	2. ubicie pozostałych portów 22 i 23
	3. maskowanie 'niespodzianki'
4. DDOS: powódź SYN, GRE IP, STOMP, DNS

Opisz Stuxnet
![[Pasted image 20240109111517.png|400]]
?
Robak do: niszczenia pomp i wirówek gazowych do wzbogacania uranu, a konkretniej programowalnych sterowników logicznych (**PLC**) Siemens S7-300 obracających się z częstotliwością 807 Hz i 1210 Hz opartych na SCADA 
1. infekcja: wgranie oprogramowania na pierwsze urządzenie przy pomocy USB i skradzionego i odpowiednio podpisanego certyfikatu sterownika Realtek (dzięki temu oprogramowanie antywirusowe nie było w stanie wykryć malware'u)
2. atak i rozprzestrzenianie: skanowanie systemu Windows w poszukiwaniu oprogramowania sterującego PLC Siemens SCADA 

Opisz atak Chain Reaction 
![[Pasted image 20240109115249.png|400]]
?
Atak na sieci o topologi siatki (mesh) PAN, o ile do konfiguracji użyto protokół Zigbee (w tym protokole wiadomości nie są szyfrowane ani podpisywane, jedynie wymiana kluczy była szyfrowana, jednak klucz główny wyciekł). Ataki mogą być wykonane bez internetu
1. Infekcja: Przerwanie szyfrowania i podpisywania, a następnie wprowadzenie "łatki" do pojedynczej żarówki. 
2. Rozprzestrzenianie: Zaatakowana żarówka przyłączy się do sieci na podstawie skradzionego klucza głównego i wykorzysta bezpieczeństwo zbliżeniowe. Po pomyślnym dołączeniu żarówki zaraża ona sąsiednie (w promieniu kilkuset metrów) żarówki

Czym się różnią technologia informacyjna od operacyjnej?
?
- dział IT:
	- odpowiada za infrastrukturę, m.in. połączenia z internetem wraz z powiązanymi systemami danych. 
	- Ponadto za informacyjne systemy firmy np e-maile. 
	- priorytetyzuje ochronę informacji
- dział OT:
	- odpowiada za zarządzanie i stan funkcjonujących systemów, monitoruje i kontroluje urządzenia (np przemysłowe, czy systemy SCADA) i ich procesy
	-  priorytetyzuje ochronę pracowników i sprzętu
Kiedyś były rozdzielne, obecnie ta granica się zaciera, bo OT zaczyna przejmować protokoły sieciowe IT, a IT coraz częściej wspiera wymagania operacyjne stosowane przez OT


Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
1. Głównego celu
?
![[Pasted image 20240111204717.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
2. Priorytetów
?
![[Pasted image 20240111205000.png]]
![[Pasted image 20240111204850.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
3. Typu ruchu sieciowego
?
![[Pasted image 20240111205000.png]]
![[Pasted image 20240111204858.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
4. Kontroli dostępu
?
![[Pasted image 20240111205000.png]]
![[Pasted image 20240111204910.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
5. Implikacji uszkodzonego urządzenia
?
![[Pasted image 20240111205000.png]]
![[Pasted image 20240111204918.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
6. Ochrony przed zagrożeniami
?
![[Pasted image 20240111205000.png]]
![[Pasted image 20240111204927.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
7. Aktualizacjami
![[Pasted image 20240111205000.png]]
?
![[Pasted image 20240111204936.png]]

Wymień różnice między polityką bezpieczeństwa sieci IT oraz OT w kontekście:
1. Głównego celu
2. Priorytetów
3. Typu ruchu sieciowego
4. Kontroli dostępu
5. Implikacji uszkodzonego urządzenia
6. Ochrony przed zagrożeniami
7. Aktualizacjami
?
![[Pasted image 20240111204625.png|700]]

Model Purdue for Control Hierarchy jest frameworkiem pozwalającym pogrupować urządzenia i sprzęt wg. hierarchicznych poziomów funkcji oraz obszarów. Co to za poziomy?
![[Pasted image 20240111221518.png]]
?
**Sieć korporacyjna**
 5. **sieć korporacyjna** - aplikacje korporacyjne CRM, ERP, VPN, HGB, CBA, FBI, itd
 4. **sieć planowania biznesowego i logistyki** - systemy planowania, telefon, poczta e-mail, monitorowanie bezpieczeństwa, drukowania


Model Purdue for Control Hierarchy jest frameworkiem pozwalającym pogrupować urządzenia i sprzęt wg. hierarchicznych poziomów funkcji oraz obszarów. Co to za poziomy?
![[Pasted image 20240111221541.png]]
?
**Przemysłowa Strefa zdemilitaryzowana**
	 **strefa zdemilitaryzowana** - stanowi bufor, w którym dane z sąsiednich poziomów mogę być współużytkowane, ale żaden ruch nie powinien przez nią przechodzić na drugą stronę  

Model Purdue for Control Hierarchy jest frameworkiem pozwalającym pogrupować urządzenia i sprzęt wg. hierarchicznych poziomów funkcji oraz obszarów. Co to za poziomy?
![[Pasted image 20240111221653.png]]
?
**Strefa operacyjna**
3. **operacje i sterowanie** - monitorowanie i kontrolowanie systemu, planowanie produkcji, zapewnienie niezawodności, optymalizacja systemu, zarządzanie siecią w usługami IT z tym związanymi (DHCP, DNS)
2. **Sterowanie nadzorcze** - administracja sieci/aplikacji systemu sterowania (w tym **HMI** (human-machine-interface)) i zbieranie danych 
1. **Podstawowe sterowanie** - komunikacja kontrolerów, urządzeń **IED** (intelligent electronic device), i dedykowanych **HMI**
0. Proces: urządzenia (czujniki, wykonawcze, napędy, roboty) komunikują się ze sterownikami lub terminalami **IED**
*Jeśli się zastanawiasz czemu wszystkie są zaliczone do strefy operacyjnej, a na zdjęciu są rozdzielone to nwm, tak jest na wykładzie*

Model Purdue for Control Hierarchy jest frameworkiem pozwalającym pogrupować urządzenia i sprzęt wg. hierarchicznych poziomów funkcji oraz obszarów. Co to za poziomy (jest ich 5)?
![[Pasted image 20240111222047.png]]
?
**Strefa bezpieczeństwa**
	**Krytyczne dla bezpieczeństwa** - zarządzanie bezpieczeństwem systemu sterowania za pomocą czujników i innego sprzętu


Model Purdue for Control Hierarchy jest frameworkiem pozwalającym pogrupować urządzenia i sprzęt wg. hierarchicznych poziomów funkcji oraz obszarów. Co to za poziomy (jest ich 5)?
![[Pasted image 20240111205427.png|700]]
?
**Sieć korporacyjna**
 5. **sieć korporacyjna** - aplikacje korporacyjne CRM, ERP, VPN, HGB, CBA, FBI, itd
 4. **sieć planowania biznesowego i logistyki** - systemy planowania, telefon, poczta e-mail, monitorowanie bezpieczeństwa, drukowania
**Przemysłowa Strefa zdemilitaryzowana**
	 **strefa zdemilitaryzowana** - stanowi bufor, w którym dane z sąsiednich poziomów mogę być współużytkowane, ale żaden ruch nie powinien przez nią przechodzić na drugą stronę  
**Strefa operacyjna**
3. **operacje i sterowanie** - monitorowanie i kontrolowanie systemu, planowanie produkcji, zapewnienie niezawodności, optymalizacja systemu, zarządzanie siecią w usługami IT z tym związanymi (DHCP, DNS)
2. **Sterowanie nadzorcze** - administracja sieci/aplikacji systemu sterowania (w tym **HMI** (human-machine-interface)) i zbieranie danych 
1. **Podstawowe sterowanie** - komunikacja kontrolerów, urządzeń **IED** (intelligent electronic device), i dedykowanych **HMI**
0. Proces: urządzenia (czujniki, wykonawcze, napędy, roboty) komunikują się ze sterownikami lub terminalami **IED**
**Strefa bezpieczeństwa**
	**Krytyczne dla bezpieczeństwa** - zarządzanie bezpieczeństwem systemu sterowania za pomocą czujników i innego sprzętu



Jakie są dobre praktyki w zakresie bezpieczeństwa IoT? 
![[Pasted image 20240111222729.png|400]]
?
1. Używaj NaJNowszEgo systemu operacyjnego i bibliotek
2. użyj sprzętu, który zawiera funkcje bezpieczeństwa i przestrzenie gdzie nie można wykonywać kodu
3. stosuj kod zaciemniający (nic nieznaczący ale utrudniający reverse engineering)
4. wybieraj hasła losowo (`stud`,`dupa123`, itd.)
5. używaj mechanizmów typu Root of trust i bezpiecznego rozruchu, aby mieć 'złoty' obraz oprogramowania działającego na urządzeniu klienta
6. wyeliminuj zakodowane hasła w obrazach ROM (read-only-memory)
7. zamknij porty IP   
8. używaj losowego układu przestrzeni adresowej, stosuj mechanizmy Stack Canaries oraz Guard bands 
9. Używaj AUtmoMATycznyCH AKtuAliZacji 
10. zaplanuj etap zakończenia eksploatacji (end-of-life) ⚰️✝️
11. premiuj za znalezione błędy
12. bierz udział w US-CERT aby na bieżąco dowiadywać się o exploitach i cyber-zagrożeniach





























