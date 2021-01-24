### Język JavaScript w programowaniu interfejsów webowych

*Źródło: moje doświadczenia*

- Javascript to skryptowy, dynamicznie typowany język programowania
- Javascript działa po stronie klienta
- Podstawowe zastosowanie to manipulacja DOM, czyli programowej reprezentacji zawartości witryny
- W praktyce oznacza to dynamiczne zarządzanie wyglądem i treścią strony
  - Możliwe jest ustawienie odpowiedzi na różne wykryte zdarzenia (eventy) np. naciśnięcie przycisku, lub kliknięcie myszką
  - Możliwa jest wtedy zmiana stylu lub zawartości
- Workery:
  - możliwość wykonywania zadań, bez blokowania głównego wątku
  - nie mają dostępu do obiektu window, ani documentu
  - porozumiewają się z głównym wątkiem przez przesyłanie komunikatów
- Możliwe wykonywanie jest wykonywanie zapytań HTTP do zewnętrznych API. Podstawowym narzędziem jest XMLHTTPRequest. Nowocześniejszym i wygodniejszym w użyciu narzędziem jest jednak Fetch API lub axios.
- Oferuje localStorage i sessionStorage:
  - magazyn dla całej domeny
  - większy rozmiar niż Cookie
  - nie jest wysyłane do serwera, jak Cookie
- obsługuje API Canvas i webGL do animacji 2D i 3D
- Typescript:
  - nadzbiór JS, wprowadzający statyczne typy
  - kompilowany do JS
- frameworki służące do SPA
- npm - menadźer pakietów

- NodeJS - Javascript po stronie serwera
  - bazuje na silniku Google - V8
  - brak obiektu window
  - możliwe używanie JS bez przeglądarki, dostępny jest także shell

### Podstawowe operacje i algorytmy przetwarzania obrazów. Morfologia matematyczna

*Źródło: slajdy Wody: 96-146*

###### Operacja bezkonstekstowe:

- są funkcją wartości pikseli i nie zależą od lokalizacji i sąsiedztwa (otoczenia, kontekstu) przekształcanego piksela
- zmianie mogą ulec jedynie wartości poszczególnych pikseli w obrazie
- najczęstszymi operacjami są operacje liniowe, potęgowe oraz logarytmiczne
- służą jako metody poprawy jakości obrazu:
  - poprawa kontrastu lub jasności
  - uwypuklenie pewnych cech
  - zmiana kolorów

**Przykładowe operacje bezkontekstowe**

---

**Histogram** - wykres obrazujący, ile pikseli o każdej intenesywności jest w obrazie.

- oś X pokazuje wszystkie moźliwe intensywności w obrazie
- wysokość słupka proporcjonalna do liczby pikseli o danej intensywności

----



- Wyrównanie histogramu
  - poprawienie kontrastu obrazu
  - osiąga dobre wyniki, gdy obraz reprezentowany jest przez wartości z niewielkiego zakresu. Wartości zostaną rozciągnięte wtedy na szerszy zakres

- Binaryzacja / progowanie
  - metoda uzyskiwania obrazu binarnego, na podstawie kolorowego, lub w obszarach szarości
  - wyznaczenie dla danego obrazu progu jasności, na podstawie którego piksele jaśniejsze od wyznaczonego progu otrzymują jedną wartość, a ciemniejsze drugą
  - każdy piksel zapisany na 1 bicie
  - zastosowanie: oddzielanie obiektów pierwszoplanowych od tła.
  - różne metody (oparte na atrybutach obiektów, przestrzenne, lokalne, OTSU, oparte na histogramie, ...)
- zmiana kontrastu
- zmiana jasności 
- zmiana nasycenia kolorów

###### Operacje kontekstowe

- modyfikacja poszczególnych elementów obrazu w zależności od stanu ich samych i ich otoczenia
- mogą być wykonywane na wszystkich punktach obrazu jednocześnie
- zalicza się operacje morfologiczne oraz filtrację.

**Przykładowe operacje kontekstowe**

- Filtracja
  - realizowane z wykorzystaniem funkcji splotu dla obrazu oraz maski, którą stanowi macierz współczynników
  - stosowane w celu wydobycia z oryginalnego obrazu informacji lub usunięcia szumów
  - problemy:
    - z powodu kontekstowości nie może dotyczyć pikseli na brzegu obrazu
  - zastosowania
    - usuwanie szumu w obrazie
    - wzmocnienie elementów zgodnych ze wzorcem
    - korekta wad obrazu, np. rys kliszy
    - poprawa obrazu (wyostrzanie, poprawa 'poruszownych')

---

**filtr** - tablice współczynników, zapisywane jako macierz:

- im większa maska, tym większe zmiany w obrazie
- im większa maska, tym więcej operacji dodawania i mnożenia
- duże maski służą do usuwania dużych zakłóceń

**filtry dolnoprzepustowe**

- drobne zakłócenia obrazu są rozmazywane
- filtr powoduje rozmycie konturów obiektów i pogorszenie rozpoznawalności ich kształtów
- prosty filtr uśredniający to macierz 3x3 z samymi 1.
- w celu zmniejszenia rozmycia, wzmacnia się punkt centralny obrazu

**filtry górnoprzepustowe**

- "wyostrzają"  obraz - uwypuklają krawędzie w obrazie
- są odpowiedzialne za 'wydobywanie' z obrazu składowych odpowiedzialnych za szybkie zmiany jasności:
  - konturów
  - krawędzi
  - drobnych elementów faktury
- Przykłady:
  - Krzyż Robertsa:
    - charakter kierunkowy
    - wykrywa proste pod kątem 45 stopni
  - operator Prewitta:
    - detekcja linii pionowych, poziomych i ukośnych
    - wzmocnieniu ulegają linie zbliżone do horyzontalnych i wertykalnych

---



- Operacje morfologiczne
  - pozwalają przeprowadzić zaawansowaną analizę kształtów poszczególnych obiektów poszczególnych obiektów, oraz odległości między nimi
  - podstawowe operacje morfologiczne można ze sobą łączyć, co daję podstawę do budowania skomplikowanych systemów analizy obrazu
  - z uwagi na złożoność, zwykle przetwarzane na obrazach binarnych
  - Przykłady:
    - dylatacja - zwiększenie obiektu, zniknięcie detali i wypełnienie „dziur” w niespójnym obszarze
    - erozja - zmniejszenie obiektu, zniknięcie wąskich gałęzi i małych obiektów, likwidacja szumu, rozszerzenie się „dziur” w niespójnym obszarze

###### Operacje afiniczne

- podstawowe przekształcenia geometryczne, jakim może być poddany obraz.
- każdy piksel składowy w macierzy obrazu, może być poddany transformacji polegającej na przeniesieniu jego wartości do piksela o odpowiednio wyliczonym położeniu.
- Obliczenie to jest dokonywane poprzez mnożenie współrzędnych piksela przez macierz transformacji.
- Przykłady:
  - translacja (przesunięcie)
  - skalowanie
  - odbicie
  - obrót
  - pochylenie
  - dowolne złożenie powyższych

---



### Techniki tworzenia aplikacji typu Single Page Application.

*Źródło: https://mansfeld.pl/webdesign/projektowanie-spa-single-page-app/*

###### Informacje ogólne

- Single Page Application - kliencka aplikacja internetowa zawarta w jednym pliku html, która jest w stanie dynamicznie doładowywać treść w taki sposób, aby się nigdy nie przeładowywać.

###### Zalety

- SPA nie przeładowuje strony, przez co obsługa strony jest bardziej płynna, i sprawia wrażenie aplikacji natywnej
- SPA potencjalnie może oszczędzać zasoby serwera, ze względu na pobieranie tylko potrzebnych danych, nie zaś dla całych podstron
- możliwość ponownego wykorzystania kodu w wielu sytuacjach
- możliwość korzystania łatwego z zewnętrznych bibliotek, dzięki npm i automatycznemu skonfigurowania środowiska
- nowe możliwości ciekawej prezentacji treści

###### Wady

- rozwiązanie droższe, bardziej pracochłonne
- problem z pozycjonowaniem
- ciągłe zmiany zachodzące w ekosystemach frameworków SPA

###### Kiedy użyć SPA

- częsta nawigacja
- podobny wygląda podstron

###### Cechy techniczne:

- odejście od bezpośredniego zarządzania DOM,
- zarządzanie stanem strony,
- podział na komponenty wieloktronego użytku,
- użycie HTML5 History API do nawigacji,
- komunikacja z aplikacją serwerową za pomocą protokołu HTTP i najczęściej JSON

###### Przykładowa technologia:

- React:

  - wspierany przez Facebook
  - najpopularniejsze obecnie rozwiązanie
  - duża swoboda w wyborach architektonicznych
  - umożliwia także (wraz z React-Native) tworzenie aplikacji mobilnych
  - można skorzystać z Redux do globalnego zarządzania stanem

  

### Najważniejsze funkcje realizowane przez silniki gier

*źródło: https://en.wikipedia.org/wiki/Game_engine*

- Silnik to środowisko programistyczne przeznaczone do rozwijania gier
- Ze względu na szybkość działania, najczęściej rozwijane są w języku C/C++
- kluczowe funkcjonalności to:
  -  silnik renderujący dla grafiki 2D/3D
    - najczęściej zbudowany na bazie API Direct3D, OpenGL lub Vulcan
    - zapewnia warstwę abstrakcji nad GPU i CPU
    - zapewnia dostęp do systemu okien
    - zapewnia dostęp do urządzeń wejścia, jak mysz i klawiatura 
  - silnik fizyczny
    - symulacja praw fizyki (dynamika, bryła sztywna, płyny, itp)
    - detekcja kolizji
  - silnik audio
    - odpowiedzialny za wczytanie, dekompresje i odtworzenie pliku z dźwiękiem
    - bardziej zaawansowane silniki, potrafią zreprodukować efekt Dopplera, echo, itp
  - sztuczna inteligencja
  - kod sieciowy
  - zarządzanie zasobami
  - często zawiera graficzny interfejs
- silniki radykalnie przyśpieszają tworzenie gier komputerowych i redukują koszty
- często możliwa jest także rozwijanie kodu na wiele platform, bez zmieniania kodu źródłowego
- Przykłady:
  - Unity
  - RAGE
  - Frostbite
  - REDEngine

### Zastosowanie metod inteligentnego przetwarzania danych w rozpoznawaniu obrazów. 

*Źródło: moja prezentacja*

- Podział:
  - **uczenie z nadzorem:**
    - perceptron wielowarstwowy
    - konwolucyjna sieć neuronowa
  - uczenie bez nadzoru
- Zadania
  - klasyfikacja - rozpoznawanie obiektu na obrazie
  - detekcja - rozpoznanie wielu obiektów, ze wskazaniem ich lokalizacji
- Perceptron wielowarstwowy
  - Budowa
    - neuron - struktura przechowująca liczbę (aktywację)
    - neurony tworzą warstwy
    - neuron z warstwy n jest połączony z każdym z neuronów warstwy n+1
    - połączenia między neuronami posiadają wagi
    - aktywacja każdego neuronu z n+1 warstwy liczona jest jako suma każdego z połączeń i aktywacji poprzedniego neuronu
    - aby aktywacja zawierała się w przedziale <0, 1>, stosuje się funkcję aktywacji, np. sigmoid
  - Nauka
    1. wprowadzenie danych
    2. liczenie funkcji kosztu (np. kwadrat błędu)
    3. na podstawie funkcji kosztu liczony jest spadek gradientu
    4. spadek gradientu odejmowany jest od wag
       1. gradient to wektor, który mówi gdzie należy się przesunąć, aby funkcja zmalała
       2. algorytm obliczania gradientu: backpropagation, propagacja wstecz
       3. aby sieć nie była ustawiana pod konkretną liczbę, gradient jest obliczany dla każdego z obrazków i jest uśredniany
       4. spadek gradientu obliczany jest na podstawie małych zbiorów danych (mini-batches) , lub na podstawie wszystkich danych
- Konwolucyjne sieci neuronowe
  - konwolucja  - operacja wykonywana na macierzach, pozwalająca wykrywać kształty:
    - operacja zachodzi na oryginalnej macierzy i filtrze (kernelu). Filtr jest zwykle mniejszy, i jest przesuwany po oryginalnej macierzy
    - istnieją filtry służące do wykrywania krawędzi pionowych i poziomych
    - parametry filtrów dobierane są ustawiane są drogą uczenia
  - padding:
    - zapobiega zmniejszaniu wynikowego obrazu
    - zapobiega zgubieniu informacji o krawędziach
  - sieci konwolucyjne
    - wykrywanie wielu cech jednocześnie, przez stosowanie kilku filtrów na raz
    - warstwa wyjściowa ma tyle kanałów, ile jest filtrów
    - warstwa konwolucyjna stosuje jeszcze funckje aktywacji i dodaje bias
    - **warstwa poolingu** 
      - uwypuklenie wykrytej cechy, oparta o stałe wartości
      - najczęściej - max-pooling
    - **fully connected**:
      - w pełni połączone wektory warstwy
  - generalny kierunek:
    - zmniejszanie wysokości i szerokości, zwiększanie liczby kanałów
    - pooling po każdej konwolucji
    - warstwy fc na koniec
- Problemy:
  - czas przetwarzania
  - ilość danych
  - underfitting (zbyt małe dopasowanie)
  - overfitting (zbyt duże dopasowanie)
- Ulepszanie sieci:
  - liczba danych
  - jakość i rodzaj danych
  - regulacja hiperparametrów:
    - liczba warstw
    - wielkość warstw FC
    - wielkość filtrów do konwolucji i poolingu
    - rodzaj poolingu
    - ‘kroki’ konwolucji i poolingu

### Techniki sztucznej inteligencji w modelowaniu sceny, renderingu i animacji. 

*źródło https://chmurowisko.pl/gan-ai-generujaca-rzeczywistosc/*

https://developers.google.com/machine-learning/gan

###### GAN

Generative Adversarial Network – generatywne sieci współzawodniczące

Dyskryminator - sieć ucząca się wykrywać obrazy

Generator - sieć ucząca się generować obrazy podobne do tych, ze zbioru uczącego

**Działanie**

- generator uczy się generować wiarygodne dane. Wygenerowane instancje stają się negatywnymi przykładami szkoleniowymi dla dyskryminatora.
-  dyskryminator uczy się odróżniać fałszywe dane generatora od rzeczywistych. Dyskryminator karze generator za wytwarzanie nieprawdopodobnych wyników.
-  generator i dyskryminator są sieciami neuronowymi. Wyjście generatora jest połączone z wejściem dyskryminatora
-  przez algorytm propagacji wstecz, dyskryminator dostarcza sygnał do generatora, który pozwala zaktualizować wagi w sieci.

Loss function === cost function

**Dyskryminator**:

- dowolna architektura sieci
- źródła danych treningowych:
  - prawdziwe dane, np. zdjęcia ludzi. Są to pozytywne przykłady
  - fałszywe fane, otrzymywane z generatora. Są to negatywne przykłady
- 2 funkcje straty:
  - funkcja straty od generatora. Ignorowana podczas treningu dyskryminatora.
  - funkcja straty dyskryminatora, używana podczas treningu dyskryminatora.
- Trening:
  - klasyfikacja danych prawdziwych treningowych i fałszywych, z generatora
  - funkcja straty dyskryminatora każe dyskryminator za nieprawidłowe klasyfikacje
  - dyskryminator aktualizuje wagi w sieci o gradient, obliczony w wyniku działania algorytmu propagacji wstecz

**Generator**

- Elementy niezbędne w architekturze generatora:
  - losowe wejście (szum). Rozkład nie ma dużego wpływu
  - sieć generatywna, generująca instancje danych z losowego wejścia
  - sieć dyskryminatora, klasyfikująca dane wygenerowane przez generator
  - wyjście dyskryminatora
  - funkcje straty generatora, która karze generator, jeśli nie udało się oszukać dyskryminatora
- Trening:
  - wytwórz dane z losowego szumu
  - otrzymaj odpowiedź: 'Prawdziwe' lub 'Fałszywe' z dyskryminatora
  - uzyskaj gradienty przez propagacje wstecz (???)
  - użyj gradientów, aby zmienić wagi generatora

**Trening GAN**

1. Przez pewną ilość epok trenowany jest dyskryminator
2. Przez pewną ilość epok trenowany jest generator
3. powtarzane są krotki 1 i 2

- podczas treningu dyskryminatora, generator się nie zmienia
- podczas treningu generatora, dyskryminator sie nie zmienia
- jeśli dyskryminator ma skuteczność 50%, generator działa perfektcyjnie
- gdy generator generuje tak dobre dane, że odpowiedzi dyskryminatora są losowe, z czasem może doprowadzić to do pogorszenia jakości generatora

**Funkcja kosztu**

- minimax loss
- Wasserstein loss

**Rodzaje GAN**

- progresywny
  - tworzy obrazy nieskiej rozdzielczości, i dopiero z czasem dodaje szczegóły
  - szybszy do wytrenowania
- warunkowy
  - pozwala określić co należy wygenerować, np. którą cyfrę z MNIST
- Image-to-Image
  - pozwala wygenerować np. fotorealistyczny obraz ze szkicu
- CycleGan
  - pozwala na nieznaczną konwersję zdjęcia, jak np. lewej ręki na prawą, konia w zebrę, etc
- synteza tekstu w obraz
- Super-Resolution
  - pozwala polepszać jakość (rozdzielczość, szczegółowość) niewyraźnych obrazów
- Face inpainting
  - generacja pełnych twarzy z obrazów z zakrytymi obszarami

### Standardy kompresji obrazów statycznych i sekwencji obrazów, różnice, zalety i wady.

*źródło: slajdy Wody: 232-*240

Kompresja:

- stratna - kompresuje (usuwa 'nadmiar' danych) przez przybliżenie oryginalnych danych
- bezstratna - dekompresuje obraz, przez odtworzenie oryginalnych danych
- ściśle powiązana z formatem pliku - np. ilość kompresowanych kanałów

###### GIF

- 8 bitowe obrazy (256 kolorów)
- bezstratny
- obsługuje przeplot - zmieszanie 2 obrazów w jednym
- wspiera prostą animację

###### PNG

- obsługuje truecolor(16M barw, 24b głębia kolorów)
- posiada kanały alfa - zmienna przeźroczystość
- korelacja gamma - wieloplatformowa kontrola jasności obrazu
- lepsza kompresja w stosunku do GIF (5-25% lepsza)
- nie wspiera animacji

###### JPEG

- bardzo popularny
- obsługiwany przez większość aplikacji użytkowych
- pozwala skompresować obraz nawet to 5% rozmiaru obrazu oryginalnego
- brak kanału alfa

###### JPEG 2000

- wsparcie dla HDR
- pełna obsługa przezroczystości i płaszczyzn alfa
- duża odporność na błędy w zaszumionych kanałach transmisji
- transmisja progresywna (progressive transmission) - po otrzymaniu mniejszej części całego pliku, można zobaczyć wersję końcową obrazu o niższej jakości. Następnie jakość stopniowo się poprawia, pobierając więcej bitów danych ze źródła

###### JPEG XR

- wyższe współczynniki kompresji od JPEG
- możliwość kompresji bezstratnej
- kafelkowa (oddzielna kompresja obrazu) - dane można dekodować regionalnie
- większa dokładność reprezentacji kolorów
- przeźroczystość  - kanał alfa
- obsługa metadanych (EXIF, XMP)

###### WebP

- może zawierać animacje
- przeźroczystość (kanał alfa)
- tryb stratny i bezstatny
- w trybie stratnym: mniejszy rozmiar i porównywalna jakość do JPEG
- w trybie bezstratnym: 26% mniejszy rozmiar od PNG
- obsługa metadanych - w formatach EXIF lub XMP
- natywne wsparcie w przeglądarkach

###### BPG

- zarówno stratny jak i bezstratny
- produkuje mniejsze pliki przy tej samej jakości niż JPEG XR i WebP
- przeznaczony do zastosowania w IOT
- zaprojektowany z myślą o przenośności
- niskie zapotrzebowanie na pamięć
- może zawierać animację
- obsługa metadanych
- do dekodowania w przeglądarce potrzebuje biblioteki JS

###### HEIF

- format kontenera dla pojedynczych zdjęć i sekwencji obrazów
- obsługiwany w iOS 11 / MacOS HighSierra, Windows 10 (1803+), Android Pie
- wysokie współczynniki kompresji
- obsługa animacji, przechowywanie innych mediów, takich jak audio i tekst
- przechowywanie dodatkowych elementów - miniatur, właściwości obrazu
- obsługa metadanych

###### FLIFF

- otwarty format
- tylko kompresja bezstratna, nieco lepsza od webP lossless
- stopniowe dekodowanie częściowo pobranych plików - pliki z przeplotem można szybko dekodować w niższej jakości / rozdzielczości
- obsługa animacji
- złożony obliczeniowo, ale zapewnia bardzo wysokie współczynniki kompresji



### Budowa i zasada działania akceleratora graficznego, przetwarzanie równoległe, przetwarzanie wielowątkowe

*Źródło: slajdy Wody 46 - 78* 

###### Budowa GPU

**Hardware**

**Streaming Multiprocessor**

- wykonuje właściwe obliczenia
- ma własne: jednostki sterujące, rejestry, potoki wykonawcze, pamięci podręczne
- wiele rdzeni (CUDA Cores)
- niewielki cache, niskie taktowanie zegara
- współpraca wątków - tylko wewnątrz tego samego SM
- jednostki funkcji specjalnych (SFU) [cos / sin / tan]
- brak predykcji rozgałęzień

**Rdzeń CUDA**

- zintegrowana jednostka zmiennoprzecinkowa i całkowitoliczbowa
- jednostka logiczna
- jednostka MOVE, COMPARE
- jednostka rozgałęzień (ang. Branch Unit)

**Hardware vs. Software**

- Wątki są wykonywane na procesorach skalarnych np. Cuda Core
- Bloki wątków wykonywane są na procesorach strumieniowych
- kernel (siatka wątków) działa na urządzeniu

**Software**

**Wątki CUDA**

- podstawowa jednostka robocza w programowaniu GPU
- wykonywane na CUDA Core
- organizowane w WARP’y
- zapewniają szybkie przełączanie kontekstu
- sprzętowe harmonogramowanie zadań (SCHEDULER)
- Single Instruction, Multiple Thread (SIMT)
- współpraca - tylko wewnątrz tego samego bloku

**WARP**

- bloki wątków sterowane przez SM, grupowane w WARP'y są 32 wątki działające synchronicznie
- jeden lub wiele WARPów tworzą CUDA Thread block

**Bloki CUDA**

- grupują do 1024 CUDA threads
- są wykonywane na 1 procesorze strumieniowym

**GRID/kernel**

- definiowana funkcja (rozszeżenie CUDA C)
- grupuje CUDA blocks
- wykonywany na urządzeniu (ang. device)

**Jednostki specjalne**

- TMU (Texture Mapping Unit) - jednostka odwzorowania tekstury
- SPU (Shader Processing Units) - równoległy procesor odpowiedzialny za obliczenia graficzne
- ROP (Render Output Unit) - pobiera informacje o pikselach i tekselach, przetwarza je, aby nadać pikselowi ostateczną teksturę i wartość głębi
- rdzenie RT (Ray-tracing):
- rdzenie Tensor (AI):
  - operacje na macierzach
  - Deep Learning Super Sampling

###### Przetwarzanie równoległe

- forma wykonywania obliczeń, w której wiele instrukcji jest wykonywanych jednocześnie
- MIMD wg. taksonomii Flynna
- dominujący wzorzec, ze względu na upowszechnienie procesorów wielordzeniowych
- Występuje na poziomie:
  - instrukcji - w gesti projektantów procesorów
  - zadania - sekwencja rozkazów tworzących zadania, wykonywana równoregle
  - programów - wykonywanie niezależnych programów przez OS
- może być prowadzone na:
  - pojedyńczym procesorze wielordzeniowym
  - systemie wieloprocesorowym
  - na systemie składającym się z wielu maszyn
- konieczne są również odpowiednie algorytmy nazywane równoległymi
- algorytmy trudniejsze w implementacji ze względu na:
  - obsługę komunikacji
  - konieczność synchronizacji niektórych zadań

Dystrybucja procesów między procesorami:

- jeśli proces jest typowo sekwencyjny, można przyśpieszyć przez zastosowanie przetwarzania potokowego (pipelining). Polega to na podzieleniu procesu na podzadania i każdy procesor wykonuje swoje podzadanie. Wymaga synchronizacji, gdyż zadanie procesora n zależne jest od wyniku zadania procesora n-1

###### Przetwarzanie wielowątkowe

- w ramach jednego procesu może być wykonywanych kilka zadań nazywanych wątkami.
- wątki (zadania) w ramach tego samego procesu współdzielą tą samą wirtualną przestrzeń adresową zawierającą kod programu i jego dane.
- wymaga synchronizacji dostępu do wspólnych zasobów

**Warunki konieczne synchronizacji**

- wzajemne wykluczanie - nie dopuszczanie do jednoczesnego korzystania ze wspólnego zasobu przez wiele wątków
- postęp - wymaga się, aby synchronizacja nie wykluczała wykonania operacji, gdy nie wynika to z wzajemnego wykluczania,
- ograniczone czekanie - każdy wątek w skończonym czasie musi uzyskać procesor, wątek nie może zostać wygłodzony



### Idea programowania i obliczeń ogólnego przeznaczenia na GPU

*Slajdy Wody 3-6*

###### Warunki konieczne, który musi spełniać algorytm

- **masowo równoległy** - obliczenia można podzielić na setki lub tysiące niezależnych jednostek pracy. Najlepsza wydajność - wszystkie rdzenie GPU zajęte
- **intenesywny obliczeniowo** - czas poświęcony na obliczenia, jest większy niż poświęcony na komunikację (przesyłanie danych z/i do pamięci GPU).

###### Cele akceleracji obliczeń na GPU:

- maksymalizacja wykonywania równoległego
- minimalizacja dostępu do pamięci globalnej
- poprawa zajętości wątków
- utrzymanie dużej intensywności arytmetycznej obliczeń

###### Przesłanki możliwości akceleracji obliczeń na GPU

- niestandardowe funkcje lub linie kodu zajmujące większość czasu wykonania
- duża ilość prostych typów danych, na przykład tablic z dużą ilością danych

Duża ilość złożonych typów danych, na przykład struktur wielopoziomowych, niewielka ilość danych do przetworzenie jest złym wskaźnikiem dobrego zrównoleglenia algorytmu

###### Wskaźniki wykorzystania GPU

- Occupancy:
  - stosunek aktywnych CUDA WARPs do maks liczby CUDA WARPs , które każdy SM może wykonywać jednocześnie
  - wysoki współczynnik occupancy - bardziej efektywnego wykorzystania GPU
  - wysokie occupancy może też obniżyć wydajność w związku z powodu zwiększonej rywalizacji o zasoby między wątkami
- Achieved occupancy:
  - rzeczywista liczba współbieżnie wykorzystanych WARPs na procesorze strumieniowym. Można zmierzyć profilerem

###### Przykładowe operacje do zrównoreglenia

- obliczanie całek metodą Monte Carlo
- obliczanie wyznaczników macierzy

Prawo Amdahla -  używane w przypadku prowadzenia obliczeń równoległych do przewidzenia teoretycznego maksymalnego wzrostu szybkości obliczeń przy użyciu wielu procesorów.



### Tworzenie aplikacji w systemie Android

*Slajdy wuja*

###### Rozwiązania natywne

Rozwiązanie zaprojektowane specjalnie pod daną platformę

Technologie:

- Java
- Kotlin

Zalety:

- łatwy dostęp do funkcji sprzętowych
- najwydajniejsze rozwiązanie
- użycie natywnych komponentów

Wady:

- zależne platformowo
- wymagane poznanie nowej technologii

###### Aplikacja Przeglądarkowa

Zalety:

- szybka w stworzeniu
- technologie webowe

Wady:

- wolna
- tylko online
- brak komponentów natywnych

###### Rozwiązania hybrydowe

Rozwiązanie bazujące do przeglądarce internetowej

Technologie:

- Cordova
- PhoneGap

Zalety:

- Oparte na przeglądarce

- korzysta z HTML, JS i CSS
- posiada dostęp do sprzętu
- wieloplatformowość
- niezależność od sieci

Wady:

- trudność z dostępem do funkcji sprzętowych
- powolność w stosunku do aplikacji natywnych
- trudno osiągnąć natywny wygląd i styl
- utrudniona dystrybucja w sklepach z aplikacjami

###### Aplikacje hybrydowe – JavaScript + Natywne UI

Technologie:

- React Native
- NativeScript

Zalety:

- szybsze niż rozwiązania hybrydowe (wymaga silnika JS, nie całej przeglądarki)
- natywny wygląd

Wady:

- trudniejsze do nauki

###### Rozwiązania kros-kompilowane

Kod aplikacji pisany jest w danym języku. Język zapewnia dostęp do natywnych interfejsów API. Narzędzie kompiluje kod do języka maszynowego, kodu bajtowego, lub do języka wysokiego poziomu

Techonologie:

- Xamarin

Zalety:

- potencjalnie szybsze niż aplikacje oparte na JS
- natywny wygląd i styl

Wady:

- nie można wykorzystać technologii znanych z tworzenia interfejsów webowych
- zupełnie nowa platforma
- niewielka relacja między kodem dewelopera, a ostatecznym wynikiem

###### Rozwiązania domain-specific

Rozwiązania tworzące aplikacje z ograniczonego spektrum, zoptymalizowany pod to konkretne zastosowanie

Technologie:

- Unity

Zalety:

- dobra wydajność
- szybkie prototypowanie i projektowanie
- czasami możliwe do użycia przez osoby nie będące programistami

Wady:

- przypisane do pewnej domeny



### Paradygmaty programowania obiektowego.

- paradygmaty - zbiór mechanizmów, jakich używa programista, wpływających na to, w jaki sposób wykonywany będzie program
- programowanie obiektowe - podejście rozwiązywania problemów programistycznych z wykorzystaniem obiektów, czyli połączeniu danych i operacji, jakich można na nich wykonać.
- zwolennicy OOP argumentują, że takie podejście dobrze odzwierciedla otaczający świat 

###### Podstawowe paradygmaty OOP

- Abstracja - Każdy obiekt w systemie służy jako model abstrakcyjnego „wykonawcy”, który może wykonywać pracę, opisywać i zmieniać swój stan oraz komunikować się z innymi obiektami w systemie bez ujawniania, w jaki sposób zaimplementowano dane cechy. 
- Hermetyzacja - jest mechanizmem łączącym kod i dane, na których kod operuje, i chroni je przed niepowołanym dostępem i niewłaściwym użyciem. Pewne dane i metody obiektów danej klasy są ukrywane, czyli dostępne jedynie metodom wewnętrznym danej klasy. 
- Dziedziczenie - mechanizm udostępniania wspólnych cech. Polega na stworzeniu nowe klasy, zwanej podklasą na podstawie już istniejącej klasy bazowej, zwanej nadklasą. Wyróżniamy dziedzieczenie pojedyńcze i wieloktrone
- Polimorfizm - mechanizmy pozwalające programiście używać zmiennych i funckji na kilka różnych sposobów. Inaczej mówiąc jest to możliwość wyabstrahowania wyrażeń od konkretnych typów

### Arytmetyka stało- i zmiennoprzecinkowa.

###### Zapis stałoprzecinkowy

**Rodzaje**

- Naturalny kod binarny – cyfry mają wagi wynikające jedynie z ich pozycji względem przecinka,
- Znak - Modół - pierwszy znak oznacza znak liczby, reszta jak w NKB
- U2 
  - najstarszy bit liczby n-cyfrowej ma wagę $-2^{n-1}$.
  - najstarszy bit = 1, to liczba jest ujemna,
  - najstarszy bit = 0, to liczba jest dodatnia lub równa 0.
  - można zwiększyć obszar zajmowany przez liczbę, przez dodanie kolejnych bitów o wartości znaku
  - można wykryć overflow
- kod spolaryzowany:
  - umożlwia zapisanie na danej ilości bitów najszerszego zakresu względem 0
  - aby otrzymać zapisaną wartość należy odjąć $2^{n-1}$
  - zakres możliwy do zapisania: [$-2^{n-1}+1$, $2^{n-1}$]

**Cechy**

- wyniki są dokładne
- im więcej bitów w części ułatmkowej, tym większa precyzja
- dokładność to waga najmniej znaczącego bitu części ułamkowej
- operacje są przemienne, łączne i rozdzielne

###### Zapis zmiennoprzecinkowy

**Informacje**

- Liczba reprezentowana przez trójkę:
  - znak S ∈ {0, 1}, gdzie 0 oznacza znak +, a 1 oznacza znak -; zawsze jest to jeden bit,
  - wykładnik E, o określonym zakresie, zapisywany w kodzie spolaryzowanym
  - mantysa M  o określonej liczbie bitów, fizycznie nie zapisuje się pierwszego bitu:
    - 1, jeśli liczba jest znormalizowana,
    - 0, jeśli liczba nie jest znormalizowana (kiedy występuje niedomiar)
- wzór: $x=S*2^E*M$
- istnieją kody specjalne:
  - nieskończoność, w przypadku nadmiaru
  - NaN
- Wykonywanie działań w arytmetyce zmiennoprzecinkowej wymaga specjalnej jednostki procesora albo programowej implementacji

**Działania**

- Dodawanie i odejmowanie:
  - Jeśli liczby mają różne wykładniki, to podczas dodawania/odejmowania mantysa liczby o mniejszym wykładniku musi zostać zdenormalizowana, tak aby wykładniki były takie same
  - dodawane/odejmowane są mantysy
- Mnożenie i dzielenie:
  - Mnożenie/dzielenie mantys i dodanie/odejmowanie wykładników

**Cechy**

- duży zakres
- często dochodzi do utraty precyzji
- powstał aby ujednolicić obliczenia na różnych platformach sprzętowych
- 2 rodzaje liczb: 32b-pojedyńczej precyzji i 64b-podwójnej precyzji
- operacje NIE są przemienne, łączne i rozdzielne

### Normalizacja schematu bazy danych.

*źródło:*

https://en.wikipedia.org/wiki/Database_normalization#Example_of_a_step_by_step_normalization

- Normalizacja to proces organizowania danych w bazie danych. Obejmuje to tworzenie tabel i ustanawianie relacji między tymi tabelami zgodnie z regułami zaprojektowanymi w celu zapewnienia większej elastyczności bazy danych przez wyeliminowanie nadmiarowości i niespójnych zależności. 
- Chociaż są możliwe inne poziomy normalizacji, trzecia postać normalna jest uważana za najwyższy poziom niezbędny dla większości aplikacji. 

Cele:

- Uniknięcie redundancji
- Wyeliminowanie niewygodnych relacji wieloznacznych.
- Uniknięcie anomalii przy aktualizacji: modyfikacji, wstawianiu i usuwaniu. 
- Unikniecie niespójności. 

###### Pierwsza postać normalna 1NF

Relacja jest w pierwszej postaci normalnej, jeśli:

- opisuje jeden obiekt
- wartości atrybutów są elementarne (niepodzielne) -to nie żadna lista, macierz, czy coś co posiada własną strukturę
- nie zawiera kolekcji, grup informacji (przykład - płeć-imiona)
- kolejność wierszy może być dowolna

###### Druga postać normalna 2NF

- spełnia 1NF
- żadna kolumna niekluczowa nie jest częściowo funkcyjnie zależna od jakiegokolwiek klucza potencjalnego (np. tablela imie-nazwisko-płeć. płeć zależy od imiona, więc nie spełnia 2NF)

**Klucz potencjalny** - minialny zbiór atrybutów, jednoznacznie identyfikujący każdą krotkę relacji

###### Trzecia postać normarna 3NF

- spełnia 2NF
- żaden atrybut niekluczowy nie jest zależny funkcyjnie od innych atrybutów niekluczowych. (np. tabela imie, nazwisko, stanowisko, stawka. Wszystkie zależą od klucza potencjalnego, ale stawka zależy także od stanowiska (zakładając że takie same stanowisko jest tak samo płatne), więc nie spełnia 3NF)

**Wady**

- przy dużej ilości tabel, może dochodzić do wielu kosztownych JOINów



### Model warstwowy TCP/IP

https://pasja-informatyki.pl/sieci-komputerowe/po-co-nam-modele/

http://www.crypto-it.net/pl/teoria/protokoly-tcp-ip.html

###### Korzyści z podziału komunikacji sieciowej na warstwy

- możliwość współdziałania ze sobą urządzeń sieciowych i oprogramowania różnych producentów
- łatwiejsze określanie reguł i zasad komunikacji
- możliwość łatwiejszego zrozumienia całego procesu komunikacji,
- możliwość zarządzania procesem komunikacji.

###### TCP/IP vs ISO/OSI

- TCP/IP:
  - to model protokołów
  - każda z warstw wykonuje konkretne zadania
  - do owych zadań stosowane są odpowiednie protokoły
- ISO/OSI
  - model odniesienia
  - służy raczej do analizy, która pozwala lepiej zrozumieć procesy komunikacyjne
  - stanowi wzór do projektowania rozwiązań sieciowych zarówno sprzętowych jak i programowych.

###### Warstwy TCP/IP

- warstwa aplikacji
  - poziom, na którym pracują aplikacje użyteczne dla człowieka, np. serwer WWW lub przeglądarka internetowa
  -  obejmuje zestaw protokołów, które aplikacje wykorzystują do przesyłania różnego typu danych w sieci
  - wykorzystywane protokoły to m.in.: HTTP, FTP, etc
- warstwa transportowa:
  - pakuje dane w pakiety
  - odpowiada za tworzenie połączeń
  - na podstawie numeru portu, wybiera odpowiedni protokół warstwy aplikacji
  - przykładowe porty: ftp: 20, http: 80, https: 443
  - numer portu - 16b liczba całkowika. Zakres: 0-655535
  - TCP:
    - *Transmission Control Protocol*
    - zestawia połączenie pomiędzy komunikującymi się stronami przez zainicjowanie tzw. sesji
    - jest protokołem niezawodnym
    - odbiorca potwierdza otrzymanie każdej wiadomości
    - brakujące pakiety są retransmitowane
    - wiadomości dostarczane są w takiej samej kolejności, w jakiej zostały wysłane 
    - szeroko wykorzystywane w protokołach i aplikacjach, które wymagają wysokiej niezawodności (HTTP(S), FTP, SMTP)
  - UDP
    -  *User Datagram Protocol* 
    - komunikacja odbywa się bez nawiązywania żadnego stałego połączenia
    - pakiety wysyłane są niezależnie od siebie
    - szybsze niż TCP
    - nie zapewnia takiej niezawodności działania jak TCP
    - nie gwarantuje, że wiadomości rzeczywiście dotarły do odbiorcy.
    - nie dostarcza pakietów w takiej samej kolejności, w jakiej zostały one wysłane.
    - ciężar uporządkowania otrzymywanych wiadomości i sprawdzenia czy nie nastąpiły błędy transmisji spoczywa na otrzymującej je aplikacji
    - preferowane, jeśli przesyłane pakiety danych są nieistotne lub komunikacja musi odbywać się z wyjątkowo dużą prędkością (DNS, DHCP, VOIP)
- warstwa internetu
  - dodaje swój nagłówek do wiadomości otrzymywanych z warstwy transportowej
  - najważniejszymi polami nowego nagłówka są adresy IP nadawcy i obiorcy
  - ustalana jest odpowiednia droga do docelowego komputera w sieci
  - IP:
    - służy do przesyłania pakietów danych przez sieć 
    - wersje IPv4 i IPv6
    - nie zapewnia żadnego systemu potwierdzania dostarczenia wiadomości
    - obowiązek upewniania się, że wszystkie dane zostały dostarczone spoczywa na protokole TCP
    - tak więc TCP/IP jest niezawodne
  - Datagramy IP:
    - pakiety danych otrzymywane z warstwy transportowej są dzielone na mniejsze datagramy
    - każdy datagram zawiera nagłówek IP oraz bajty otrzymane z warstwy transportowej. 
- warstwa dostępu do sieci 
  - umożliwia przesłanie datagramów z warstwy internetowej, przez fizyczną sieć do drugiego komputera
  - protokoły TCP/IP wyższych warstw najczęściej są używane razem z zestawem protokołów ethernetowych
  - warstwy ethernetowe:
    - **Logic Link Control (LLC)** - przekazuje informacje do docelowej maszyny odnośnie tego jaki protokół powinien być użyty w warstwie transportowej. Dopisuje informacje o protokole użytym w warstwie internetowej i o protokole, który powinien otrzymać wiadomość. Pozwala to warstwie LLC na docelowym komputerze poprawnie dostarczyć otrzymane datagramy.
    - **Media Access Control (MAC)** - Odpowiedzialna za tworzenie końcowej wiadomości ethernetowej (*Ethernet frame*), która będzie wysłana przez sieć komputerową. Zawiera adresy MAC nadawcy i odbiorcy, czyli fizyczne adresy dwóch komunikujących się maszyn, lub MAC routera, jeśli znajdują się w innej sieci
    - warstwa fizyczna - odpowiedzialna za przekształcanie wiadomości w (zależności od typu sieci) impulsy elektryczne lub fale elektromagnetyczne oraz za transmitowanie ich przez sieć fizyczna pomiędzy komunikującymi się maszynami.

### Ocena złożoności algorytmów

https://pl.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/big-o-notation

https://edu.pjwstk.edu.pl/wyklady/nai/scb/wyklad6/w6.htm

https://pl.wikipedia.org/wiki/Problem_NP-zupe%C5%82ny

###### Definicje

- Problem obliczeniowy - Jest to zbiór danych wejściowych, ich definicji oraz polecenie do wykonania.
  - problem sortowania liczb w tablicy
  - problem komiwojażera
  - problem plecakowy
- Algorytm - To uporządkowany zbiór kroków jakie należy kolejno wykonać celem znalezienia rozwiązania rozpatrywanego problemu.
- Problem **rozstrzygalny** – problem dla którego istnieje algorytm znajdujący rozwiązanie w skończonej liczbie kroków
- Problem **nierozstrzygalny** – problem dla którego udowodniono że nie istnieje algorytm znajdujący rozwiązanie w skończonej liczbie kroków
- Złożoność **obliczeniowa** - Miara efektywności algorytmu, czyli ilości zasobów potrzebnych do jego wykonania.
- Złożoność **czasowa** – oszacowuje zależność czasu potrzebnego do wykonania algorytmu od rozmiaru instancji rozwiązywanego problemu.
- Złożoność **pamięciowa** – oszacowuje ilość wymaganych zasobów pamięciowych do wykonania algorytmu w funkcji rozmiaru instancji problemu.
- Notacja dużego Theta:
  - kiedy mówimy, że określony czas wykonania wynosi $\Theta(g(n))$, mówimy, że kiedy n stanie się wystarczające duże, czas wykonania wynosi, co najmniej $k_1\cdot g(n)$ i co najwyżej  $k_2\cdot g(n)$ dla stałych $k_1$ oraz $k_2$.
  - kiedy używamy notacji dużego Theta, mówimy że czas wykonania jest **mocno związany asymptotycznie**
- Notacja dużego O:
  - jeśli czas wykonania jest ograniczony przez $O(g(n))$, to dla odpowiednio dużych n czas wykonania wynosi co najwyżej $k \cdot g(n)$ dla pewnej zmiennej *k*.
  - używamy w celu wyznaczenia **górnych granic asymptotycznych**, ponieważ ogranicza ona wzrost czasu wykonania dla dużych danych wejściowych.
- Notacja dużego Omega
  - algorytm zajmuje *przynajmniej* pewną ilość czasu bez podawania górnej granicy
  - używana do oznaczenia **asymptotycznej granicy dolnej** ponieważ ogranicza wzrost czasu wykonania od dołu dla odpowiedno dużych wartości podanych na wejściu.
- staramy się określić złożoność jak najdokładniej

###### Rzędy złożoności obliczeniowej

- $O(1)$ - złożoność stała
- $O(log(n))$ - złożoność logarytmiczna
- $O(n)$ - złożoność liniowa
- $O(nlog(n))$ - złożoność liniowo - logarytmiczna
- $O(n^k)$ - złożoność wielomianowa (k - stała)
- $O(k^n)$ - złożoność wykładnicza

###### Klasa złożoności

- Klasa **P** - problem decyzyjny, dla którego rozwiązanie można znaleźć w czasie wielomianowym.
- Klasa **NP** - problem decyzyjny, dla którego rozwiązanie można zweryfikować w czasie wielomianowym. Równoważna definicja mówi, że problem jest w klasie NP, jeśli może być rozwiązany w wielomianowym czasie na niedeterministycznej maszynie Turinga.
- Klasa **NP-zupełne** - problem należy do klasy NP oraz dowolny problem należący do NP może być do niego zredukowany w czasie wielomianowym.
- Klasa **NP-trudne** - problem obliczeniowy, którego rozwiązanie jest co najmniej tak trudne, jak rozwiązanie każdego problemu z klasy NP
- Klasa **PSPACE** - jest zbiorem wszystkich problemów decyzyjnych, które można rozwiązać za pomocą maszyny Turinga wykorzystującej wielomianową przestrzeń.

### Język UML w projektowaniu oprogramowania

*https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B6%5D%20Jezyk%20UML%20w%20projektowaniu%20oprogramowania/tekst/3.pdf*

###### UML 

- zestaw pojęć, oznaczeń i diagramów
- formalny opis modelu reprezentującego projekt informatyczny
- stosuje się do zdefiniowania systemu oprogramowania
- pozwala jednoznacznie określić znaczenie graficznego obrazu modelu
- pozwala na wygenerowanie kodu

###### Zalety

- oszczędność czasu w fazie produkcji przez możliwość wcześniejszego dokładnego zaprojektowania
- możliwość eliminacji błędów na etapie koncepcyjnym, co zmniejsza koszt projektu
- jest w większośći zrozumiały dla programistów i osób nietechnicznych

###### Składowe UML

- notacja - reprezentacja graficzna
- metamodel - definicje pojęć i powiązań, dla nadania modelom ścisłości

###### Diagramy

- **diagram przypadków użycia**:

  - technika wyznaczania funkcjonalnych wymagań systemu
  - opisywanie typowych interakcji między użytkownikami systemu a samym systemem
  - w terminologii przypadków użycia systemu użytkowników nazywa się aktorami
  - możliwy jest aktor bezosobowy, jak np. zewnętrzny system
  - **przypadek użycia** reprezentuje konkretną funkcjonalność, ale bez prezentowania jej szczegółów.

- **diagram klas**:
  
  - przedstawia klasy i relacje między nimi
  - pokazuje atrybuty i funkcje klas
  - prezentowane są powiązania między klasami
  
- **diagram sekwencji**:

  - prezentuje jak współpracują ze sobą grupy obiektów
  - pokazuje kilka przykładowych obiektów i komunikaty między nimi wymieniane z zachowaniem ich kolejności np:
    - wywołanie procedury
    - wywołanie asynchroniczne
  - może pokazywać tworzenie lub niszczenie obiektu
  - mogą zawierać konstrukcje takie jak pętle, czy instrukcje warunkowe

- **diagram aktywności**

  - technika opisywania logiki działania systemu, procesów biznesowych i przepływów pracy
  - diagram określa najważniejsze zasady dotyczące kolejności wykonywania czynności
  - przydatny przy modelowaniu sytuacji decyzyjnych, operacji czy algorytmów

- **diagram maszyny stanowej**
  
  - pokazuje możliwe stany obiektu oraz przejścia, które powodują zmianę tego stanu
  - można z niego odczytać, jakie dane wejściowe powodują przejście systemu w dany stan
  - składa się ze stanów, oraz reguł, wg których przełączane są stany
  
  

### Generowanie realistycznych obrazów scen 3-D za pomocą metody śledzenia promieni

*źródło https://git.izernet.pl/MKjanek32/PWrEgzaminInz/src/branch/master/W4-INF-kierunkowe.md*

###### Metoda śledzenia promieni:

- służy do generowania fotorealistycznych scen 3D z odwzorowaniem efektów oświetlenia (cienie, odbicia światła od obiektów)
- analizowane są tylko promienie docierające do obserwatora, w kierunku odwrotnym do padania światła – od pozycji obserwatora, przecinając rzutnię (ekran), wgłąb sceny. 
- powyższe działanie zaoszczędza zasoby systemu, gdyż nie liczy promieni, które nie trafiłyby w ekran

###### Działanie:

1. Dla każdego piksela na ekranie z punktu, w którym znajduje się obserwator, wyprowadzany jest promień pierwotny, który przecina ten piksel.

2. Jeżeli:

- promień nie trafi na żaden obiekt na scenie – piksel przyjmuje kolor tła,
- promień trafi w źródło światła – piksel przyjmuje kolor źródła,
- promień trafi w obiekt – wyznaczany jest najbliższy punkt przecięcia z obiektem i dla niego:
  - obliczany jest kolor za pomocą jednego z modeli oświetlenia lokalnego (np. modelu Phonga),
  - ewentualne zacienienie (poprzez poprowadzenie pomocniczych promieni do źródeł światła i przeanalizowanie, czy przecinają inne obiekty),
  - kierunek odbicia promienia wtórnego, który następnie jest śledzony rekruncyjnie w taki sam sposób (jeżeli trafi w kolejny obiekt – jego oświetlenie lokalne jest mnożone przez współczynnik odbicia i dodawane do lokalnego oświetlenia poprzedniego obiektu).

3. Krok 2 jest powtarzany dopóki promień wtórny nie trafi w tło albo w źródło światła, lub dopóki nie zostanie osiągnięta określona głębokość rekurencji.

###### Charakterystyka

- wysoki koszt obliczneniowy (należy przeprowadzić procedurę RT dla każdego piksela)
- możliwe równoregłe obliczenia dla każdego promienia lub piksela

###### Model oświetlenia Phonga

**Model Phonga** pozwala wyliczyć oświetlenie lokalne jako sumę trzech rodzajów światła:

- **światło otaczające (ang. ambient)** – bezkierunkowe światło, równomiernie oświetlające obiekty ze wszystkich stron – w naturze ten rodzaj światła dominuje w środku dnia podczas pochmurnej pogody,
- **światło rozproszone (ang. diffuse)** – światło padające z określonego kierunku i rozpraszane przez obiekty, dając ich równomierne oświetlenie z jednej strony,
- **światło odbite (ang. specular)** – światło padające z określonego kierunku i silnie odbijane przez obiekty, dając efekt połysku ich powierzchni.



### Mechanizmy systemu operacyjnego wspomagające synchronizację procesów

*źródło https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B8%5D%20Mechanizmy%20systemu%20operacyjnego%20wspomagajace%20synchronizacje%20procesow/tekst/1.pdf*

*https://www.ii.uni.wroc.pl/~wzychla/ra2223/so2.html*

https://pl.wikipedia.org/wiki/W%C4%85tek_(informatyka)

https://en.wikipedia.org/wiki/Semaphore_(programming)

###### Wątki a procesy

Różnica między zwykłym procesem a wątkiem polega na współdzieleniu przez wszystkie wątki działające w danym procesie przestrzeni adresowej oraz wszystkich innych struktur systemowych (np. listy otwartych plików, gniazd itp.) – z kolei procesy posiadają niezależne zasoby. Ta cecha ma dwie ważne konsekwencje:

- Wątki wymagają mniej zasobów do działania i też mniejszy jest czas ich tworzenia. 
- Dzięki współdzieleniu przestrzeni adresowej (pamięci) wątki jednego zadania mogą się między sobą komunikować w bardzo łatwy sposób, niewymagający pomocy ze strony systemu operacyjnego.

Jeśli biblioteka pthreads implementuje opcję **TSH** (Thread Process-Shared Synchronization), wówczas możliwa staje się synchronizacja między wątkami różnych procesów.

###### Synchronizacja

**Synchronizacja procesów** to klasyczny problem z dziedziny informatyki ustalenia kolejności działania procesów ze sobą współpracujących. Problem pojawia się tam, gdzie występują współbierzne procesy. Celem jest ograniczenie dostępu do zasobu tak, aby dopuszczalne były przeploty zgodnie z wolą programisty

**Kiedy pojawia się problem synchronizacji**

- procesy współdzielą strukturę danych - sekcja krytyczna
- wyniki działania jednego procesu, są potrzebne do działania innego procesu - producent-konsument
- procesy mogą korzystać z pewnej puli zasobów - Filozofowie

**Klasyczne problemy synchronizacji**

- problem producenta i konsumenta
- problem ucztujących filozofów
- problem czytelników i pisarzy
- problem sekcji krytycznej

###### Mechanizmy synchronizacji

- semafory - procesy z nich korzystające mogą blokować wejście do określonych części kodu
  - binarny
    - może przyjmować wartości całkowite ze zbioru {0, 1}
    - operacja P (wait) - oczekiwanie, dopóki zasób chroniony przez semafor stanie się dostępny, a następnie jest zajmowany. 
    - operacja V (signal) - zwalnianie zasobu
  - zliczający
    - może przyjmować wartości całkowite ze zbioru {0, inf}
- muteksy - mutex może być uwolniony tylko przez **wątek**, który jest jego właścicielem, licznik semafora może być zwiększony przez dowolny wątek, który z tego semafora korzysta. Rodzaj semafora binarnego
- zmienne warunkowe - narzędziem do blokowania **wątku** wewnątrz sekcji krytycznej aż do momentu gdy pewien warunek zostanie spełniony



### Programowalne scalone układy cyfrowe PLD, CPLD oraz FPGA

*źródło https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B9%5D%20Programowalne%20scalone%20uklady%20cyfrowe%20PLD%2C%20CPLD%2C%20oraz%20FPGA/tekst/1.pdf*

https://git.izernet.pl/MKjanek32/PWrEgzaminInz/src/branch/master/W4-INF-kierunkowe.md

Programowalne układy cyfrowe to :

- układy scalone, których właściwości funkcjonalne są definiowane nie przez producenta, lecz przez końcowego użytkownika
- są przydatne gdy nie istnieje układ realizujący takie zadanie
- w stosunku do układów nieprogramowalnych są wolniejsze i mają większy pobór mocy
- realizują funkcje logiczne w sposób równoległy
- języki: VHDL i Verilog
- narzędzia syntezy tworzone przez producentów układów są w stanie przetłumaczyć VHDL na konfigurację konkretnego układu FPGA lub CPLD.
- stosuje się często do sterowania urządzeniami i szybkiego przetwarzania dużych ilości danych – na przykład w kryptografii, w urządzeniach sieciowych (przełączniki), czy też przy cyfrowym przetwarzaniu sygnałów.

###### Kategorie urządzeń

- PLD (*Programmable Logic Device*)

  - najstarszy i najprostszy
  - składają się one z 2 matryc bramek logicznych AND-OR i występują w trzech odmianach:
    - **PAL** – z programowalną matrycą AND (najpowszechniejsze)
    - **PLE** - z programowalną matrycą OR
    - **PLA** - z programowalnymi obydwoma matrycami
  - składają się z małej liczby bramek logicznych (typowo posiadają 8-10 wejść i wyjść oraz kilkadziesiąt bramek)

- CPLD (Complex PLD)

  - wiele układów PLD połączonych szybką globalną matrycą połączeń
  - mogą posiadać już kilka tysięcy bramek logicznych.
  - w układach PLD i CPLD jako pamięć konfiguracji wykorzystuje najczęściej EEPROM (elektrycznie programowalną i kasowalną).
  
- FPGA (Field Programmable Gate Array):

  - to najbardziej skomplikowany rodzaj układów programowalnych o największych możliwościach

  - pojemności dochodzą do kilkuset tysięcy bramek logicznych

  -  tzw. LUT (Look Up Table) tablicuje tabele prawdy funkcji

  - składają się z wielu połączonych globalną matrycą bloków CLB (*Configurable Logic Block*), zawierających LUT, przerzutniki i multipleksery.

  - jako pamięć konfiguracji wykorzystywana jest pamięć statyczna RAM (SRAM) – ponieważ jest to pamięć ulotna, często do układów FPGA dołącza się oddzielne układy pamięci EEPROM, z których FPGA po podłączeniu zasilania automatycznie może odczytać konfigurację połączeń

    

  

### Optyczne nośniki informacji.

**Optyczny nośnik informacji** to ciało fizyczne, na którym możliwe jest zapisanie/odczytanie danego rodzaju informacji przez oświetlenie nośnika promieniem lasera.

###### Płyty:

- CD - *Compact Disc* - 700MB - podczerwień
- DVD - *Digital Video Disc* - od 4.7 do 17GB (dwustronne dwuwarstwowe) 
  - osiągnięte przez krótszą falę lasera. 
  - Musi zawierać system plików - UDF
  - światło czerwone
- Blue Ray Disc - 25 - 400GB (szesnastowarstwowe) - światło niebieskie

###### CD - działanie

- Stany logiczne repreentowane przez wgłębienia (pity) i przerwy między wgłębieniami (landy)
- natrafienie na land - odbicie,  powrót do czujnika
- pit -  rozproszenie, nie powraca do czujnika

Przy użyciu odpowiednich algorytmów stopień odbicia lub rozproszenia tej wiązki konwertowany jest na ciąg jedynek i zer, a ten z kolei pozwala na odtworzenie danych, które wcześniej zostały tam zapisane

###### Rodzaje CD/DVD

- CD powstające na skutek odciśnięcia matryce
- CD-R - możliwy jednokrotny zapis danych
- CD-RW - podobne do CD-R, jednak umożliwiające wielokrotny zapis danych
- +R 
  - muszą być sformatowane przed rozpoczęciem nagrywania czego nie wymaga format –R.
  - zastosowanie systemu kontroli prędkości i zapisu ADIP, który jest mniej podatny na zakłócenia i błędy,

###### Inne:

- kody kreskowe
  - kombinacja jasnych i ciemnych elementów
  - odczytywane przez czytniki elektroniczne
  - Przykłady Code11, POSTNET
- dyski magnetooptyczne
  - krążki z tworzywa, pokryte warstwą materiału magnetycznego, zabezpieczony warstwą ochronną i umieszczony w kasecie
  - wymiar 3.5 cala - 128MB - 2.3GB
  - wymiar 5.25 cala - 650MB - 9GB
  - jedno lub wielokrotny zapis
  - odczyt wykorzystuje efekt Kerra
- HVD - Holographic Versatile Disc:
  - do 6TB
  - zapis w przestrzeni trójwymiarowej dysku
  - wykorzystuje lasery: zielony i czerwony