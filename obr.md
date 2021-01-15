### Język JavaScript w programowaniu interfejsów webowych

*Źródło: moje doświadczenia*

- Javascript to dynamiczny język programowania, który po dodaniu do dokumentu HTML, może dostarczyć dynamiczną zawartość do stron internetowych.

- Javascript działa po stronie klienta

- Podstawowe zastosowanie to manipulacja DOM, czyli programowej reprezentacji zawartości witryny

- W praktyce oznacza to dynamiczne zarządzanie wyglądem i treścią strony
  - Możliwe jest ustawienie odpowiedzi na różne wykryte zdarzenia (eventy) np. naciśnięcie przycisku, lub kliknięcie myszką
  - Możliwa jest wtedy zmiana stylu lub zawartości
- Możliwe wykonywanie jest wykonywanie zapytań HTTP do zewnętrznych API. Podstawowym narzędziem jest XMLHTTPRequest. Nowocześniejszym i wygodniejszym w użyciu narzędziem jest jednak Fetch API lub axios.

### Podstawowe operacje i algorytmy przetwarzania obrazów. Morfologia matematyczna

*Źródło: slajdy Wody: 96-146*

###### Operacja bezkonstekstowe punktowe (bezkontekstowe):

- są funkcją wartości pikseli i nie zależą od lokalizacji i sąsiedztwa (otoczenia, kontekstu) przekształcanego piksela

- zmianie mogą ulec jedynie wartości (jasność) poszczególnych pikseli w obrazie

- najczęstszymi operacjami są operacje liniowe, potęgowe oraz logarytmiczne

- wszystkie piksele o jednakowej intensywności są traktowane identycznie

- służą jako metody poprawy jakości obrazu:
  - poprawa kontrastu lub jasności
  - uwypuklenie pewnych cech
  - zmiana histogramu
  - zmiana kolorów

###### Operacje kontekstowe

- modyfikacja poszczególnych elementów obrazu w zależności od stanu ich samych i ich otoczenia
- mogą zajmować dużo czasu
- algorytmy są proste i regularne a ponadto mogą być wykonywane na wszystkich punktach obrazu jednocześnie

###### Operacje morfologiczne

- pozwalają przeprowadzić zaawansowaną analizę kształtów poszczególnych obiektów poszczególnych obiektów, oraz odległości między nimi
- podstawowe operacje morfologiczne można ze sobą łączyć, co daję podstawę do budowania skomplikowanych systemów analizy obrazu

###### Operacje geometryczne

- pozwalają ujednolicić format obrazów
- mogą być stosowane w celu wyeliminowania zniekształceń (np. zniekształcenia powodowane przez szerokokątne obiektywy)

###### Operacje afiniczne

Definiowane jako przekształcenia macierzy:

- translacja
- skalowanie
- odbicie
- obrót
- pochylenie
- jednokładność
- dowolne złożenie powyższych

---

**Histogram** - wykres obrazujący, ile pikseli o każdej intenesywności jest w obrazie.

- oś X pokazuje wszystkie moźliwe intensywności w obrazie
- wysokość słupka proporcjonalna do liczby pikseli o intensywności x

---

###### Wyrównanie histogramu

- poprawienie kontrastu analizowanego obrazu z wykorzystaniem jego histogramu
- osiąga dobre wyniki, gdy obraz reprezentowany jest przez wartości z niewielkiego zakresu. Wartości zostaną rozciągnięte wtedy na szerszy zakres

###### Filtracja

- operacja matematyczna na pikselach, w której wyniku uzyskiwany jest przekształcony obraz
- jest to przekształcenie kontekstowe
- stosowane w celu wydobycia z oryginalnego obrazu informacji lub usunięcia szumów
- 'przesuwanie okna'
- można wykonać ją w dziedzinie:
  - przestrzennej - operacja splotu
  - częstotliwościowej - mnożenie transformat obrazu i filtru
- problemy:
  - z powodu kontekstowości nie może dotyczyć pikseli na brzegu obrazu
- w praktyce
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

- "wyostzają"  obraz - uwypuklają krawędzie w obrazie
- odpowiedzialne za 'wydobywanie' z obrazu składowych odpowiedzialnych za szybkie zmiany jasności:
  - konturów
  - krawędzi
  - drobnych elementów faktury
- Przykłady:
  - Krzyż Robertsa
  - **operator Prewitta:**
    - detekcja linii pionowych, poziomych i ukośnych
    - wzmocnieniu ulegają linie zbliżone do horyzontalnych i wertykalnych
  - operator Sobela
  - Laplasjan

---



###### Rozmycie Gaussa

- wykres funkcji gęstości rozkładu normalnego - kapelusz Gaussa
- zastosowanie w usuwanie szumów
- liczy średnią ważoną z otoczenia danego piksela

###### Binaryzacja / progowanie

- metoda uzyskiwania obrazu binarnego, na podstawie kolorowego, lub w obszarach szarości
- każdy piksel zapisany na 1 bicie
- wyznaczeniu dla danego obrazu progu jasności, a następnie piksele jaśniejsze od wyznaczonego progu otrzymują jedną wartość (np. 0), a ciemniejsze drugą (np. 255)
- zastosowanie: oddzielanie obiektów pierwszoplanowych od tła

### Techniki tworzenia aplikacji typu Single Page Application.

*Źródło: https://mansfeld.pl/webdesign/projektowanie-spa-single-page-app/*

###### Informacje ogólne

- Single Page Application - strona internetowa, działająca po stronie klienta, która jest w stanie dynamicznie doładowywać treść
- SPA nie przeładowuje strony, przez co obsługa strony jest bardziej płynna, i sprawia wrażenie aplikacji natywnej
- SPA potencjalnie może oszczędzać zasoby serwera, ze względu na pobieranie tylko potrzebnych danych, nie zaś dla całych podstron

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
  - można sskorzystać z Redux do zarządzania stanem

  

### Najważniejsze funkcje realizowane przez silniki gier

*źródło: https://en.wikipedia.org/wiki/Game_engine*

- Silnik to środowisko programistyczne przeznaczone do rozwijania gier
- Ze względu na szybkość działania, najczęściej rozwijane są w języku C/C++
- kluczowe funkcjonalności to:
  -  silnik renderujący dla grafiki 2D/3D
    - najczęściej zbudowany na bazie API Direct3D, OpenGL lub Vulcan
    - zapewnia warstwę abstrakcji nad GPU
    - zapewnia dostęp do systemu okien
    - zapewnia dostęp do urządzeń wejścia, jak mysz i klawiatura 
  - silnik fizyczny
    - symulacja praw fizyki (dynamika, bryła sztywna, płyny, itp)
    - detekcja kolizji
  - silnik audio
    - odpowiedzilany za wczytanie, dekompresje i odtworzenie pliku z dźwiękiem
    - bardziej zaawansowane silniki, potrafią zreprodukować efekt Dopplera, echo, itp
  - dźwięk,
  - sztuczna inteligencja
  - zarządzanie zasobami
  - często zawiera graficzny interfejs
- silniki radykalnie przyśpieszają tworzenie gier komputerowych i redukują koszty
- często możliwa jest także rozwijanie kodu na wiele platform, bez zmieniania kodu źródłowego

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
    - neurony tworzą warstwyneuron z warstwy n jest połączony z każdym z neuronów warstwy n+1
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

###### GAN

Generative Adversarial Network – generatywne sieci współzawodniczące

**Działanie**

- dyskryminator - sieć ucząca się wykrywać obrazy
- generator - sieć ucząca się generować obrazy
- generator próbuje przechytrzyć dyskryminatora, a dyskryminator, posiadając próbki prawdziwych i nieprawdziwych (generowanych) zdjęć, próbuje do tego nie dopuścić.
-  momencie gdy generator zacznie tworzyć tak realistyczne zdjęcia, że dyskryminator nie będzie w stanie odróżnić ich od prawdziwych, model generatywny zostanie w pełni wytrenowany. 

**Zastosowania**

- generacja twarzy
- postarzanie twarzy
- generowanie zdjęć z opisu słownego
- przewidywanie wideo
- generowanie obrazu

### Standardy kompresji obrazów statycznych i sekwencji obrazów, różnice, zalety i wady.

*źródło: slajdy Wody: 232-*240

Kompresja:

- stratna - kompresuje (usuwa 'nadmiar' danych) przez przybliżenie oryginalnych danych
- bezstratna - dekompresuje obraz, przez odtworzenie oryginalnych danych

###### GIF

- 8 bitowe obrazy (256 kolorów)
- obsługuje przeplot
- wspiera prostą animację

###### PNG

- obsługuję truecolor, skalę szarości, kolor
- posiada kanały alfa - zmienna przeźroczystość
- korelacja gamma - wieloplatformowa kontrola jasności obrazu
- dwuwymiarowy przeplot (metoda wyświetlania progresywnego)
- lepsza kompresja w stosunku do GIF (5-25% lepsza)
- nie wspiera animacji

###### JPEG 2000

- bazowany na dyskretnej transformacie falkowej
- możliwe jest przechowywanie różnych części tego samego obrazu przy użyciu innej jakości
  wsparcie dla HDR
- pełna obsługa przezroczystości i płaszczyzn alfa
- Interaktywność z aplikacjami sieciowymi (JPEG Part 9 JPIP protocol)
- duża odporność na błędy w zaszumionych kanałach transmisji
- Transmisja progresywna (progressive transmission) - o otrzymaniu mniejszej części całego pliku, można zobaczyć wersję końcową obrazu o niższej jakości. Następnie jakość stopniowo się poprawia, pobierając więcej bitów danych ze źródła

###### JPEG XR

- wyższe współczynniki kompresji
- kafelkowa (oddzielna kompresja obrazu)
- większa dokładność reprezentacji kolorów
- przeźroczystość  - kanał alfa
- obsługa metadanych (EXIF, XMP)

###### WebP

- wykorzystuje kodowanie predykcyjne
- może zawierać animacje
- przeźroczystość (kanał alfa)
- profil kolorów
- obsługa metadanych - w formatach EXIF lub XMP
- natywne wsparcie w przeglądarkach

###### BPG

- produkuje mniejsze pliki przy tej samej jakości niż JPEG, JPEG XR i WebP
- przeznaczony do zastosowania w IOT
- zaprojektowany z myślą o przenośności
- niskie zapotrzebowanie na pamięć
- wsparcie dla koloru 14bpp (HDR)
- może zawierać animację
- profil kolorów - obraz może mieć osadzony profil ICC
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
- tylko kompresja bezstratna
- wsparcie dla koloru 16bpp
- stopniowe dekodowanie częściowo pobranych plików - pliki z przeplotem można szybko dekodować w niższej jakości / rozdzielczości („Responsive By Design”)
- cobsługa animacji
- złożony obliczeniowo, ale zapewnia bardzo wysokie współczynniki kompresji



### Budowa i zasada działania akceleratora graficznego, przetwarzanie równoległe, przetwarzanie wielowątkowe

*Źródło: slajdy Wody 46 - 78* 

###### Budowa GPU

**Hardware**

**Streaming Multiprocessor**

- wykonuje właściwe obliczenia
- ma własne: jednostki sterujące, rejestry, potoki wykonawcze, pamięci podręczne
- wiele rdzeni (CUDA Cores) w SM (ilość zależna od architektury)
- współpraca wątków - tylko wewnątrz tego samego SM
- zadanie równoległe wykonywane przez kilku bloków wątków (ang. block threads)
- jednostki funkcji specjalnych (SFU) [cos / sin / tan]
- jądra GPU (ang. cores) zorganizowane w grupy wewn. SM
- brak predykcji rozgałęźień

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

- bloki wątków sterowane przez SM, grupowane w WARP'y (po 32 wątki działające synchronicznie)
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
  - operacje na macierzarz
  - Deep Learning Super Sampling

**Wskaźniki wykorzystania GPU**

- Occupancy:
  - stosunek aktywnych CUDA WARPs do maks liczby CUDA WARPs , które każdy SM może wykonywać jednocześnie
  - wysoki współczynnik occupancy - bardziej efektywnego wykorzystania GPU
  - wysokie occupancy może też obniżyć wydajność w związku z powodu zwiększonej rywalizacji o zasoby między wątkami
- Achieved occupancy:
  - rzeczywista liczba współbieżnie wykorzystanych WARPs na procesorze strumieniowym. Można zmierzyć profilerem

###### Przetwarzanie równoległe

- procesy sekwencyjne - rozdzielone zasoby, ograniczona komunikacja (mechanizmy komunikacji międzyprocesowej)
- procesy wielowątkowe - częściowo równoregłe wykonywanie, w wielu wątkach. Łatwa komunikacja między wątkami 

Dystrybucja procesów między procesorami:

- jeśli proces jest typowo sekwencyjny, można przyśpieszyć przez zastosowanie przetwarzania potokowego (pipelining). Polega to na podzieleniu procesu na podzadania i każdy procesor wykonuje swoje podzadanie. Wymaga synchronizacji, gdyż zadanie procesora n zależne jest od wyniku zadania procesora n-1

###### Przetwarzanie wielowątkowe

**Warunki konieczne synchronizacji**

- wzajemne wykluczanie - wątki są zależne od wyników innych wątków. Dopóki jeden nie skończy pewnej czynności, drugi nie może zacząć swojej czynności,
- postęp - wymaga się, aby synchronizacja nie wykluczała wykonania operacji, gdy nie wynika to z pierwszego warunku,
- ograniczone czekanie - każdy wątek w skończonym czasie musi uzyskać procesor, wątek nie może zostać wygłodzony

Sekcja krytyczna:

- może być w niej jeden proces na raz
- rozwiązywana:
  - semaforem (rozwiązanie softwarowe)
  - instrukcją sprzętowa, atomowa TestAndSet
  - instrukcją sprzętowa, atomowa Swap



### Idea programowania i obliczeń ogólnego przeznaczenia na GPU

*Slajdy Wody 3-6*

###### Warunki konieczne, który musi spełniać algorytm

- masowo równoległy - obliczenia można podzielić na setki lub tysiące niezależnych jednostek pracy. Najlepsza wydajność - wszystkie rdzenie GPU zajęte
- intenesywny obliczeniowo - czas poświęcony na obliczenia, jest większy niż poświęcony na komunikację (przesyłanie danych z/i do pamięci GPU).

###### Cele akceleracji obliczeń na GPU:

- maksymalizacja wykonywania równoległego
- minimalizacja dostępu do pamięci globalnej
- poprawa zajętości wątków
- utrzymanie dużej intensywności arytmetycznej obliczeń

###### Przesłanki możliwości akceleracji obliczeń na GPU

- niestandardowe funkcje lub linie kodu zajmujące większość czasu wykonania
- duża ilość prostych typów danych, na przykład tablic z dużą ilością danych

Duża ilość złożonych typów danych, na przykład struktur wielopoziomowych, niewielka ilość danych do przetworzenie jest złym wskaźnikiem dobrego zrównoleglenia algorytmu

###### Przykładowe operacje do zrównoreglenia

- obliczanie całek metodą Monte Carlo
- obliczanie wyznaczników macierzy



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
- Niezależność od sieci

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
- obiekt to instancja klasy
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
  - najstarszy bit =0, to liczba jest dodatnia lub równa 0.
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
- jest zdefiniowany klucz relacji.
- wszystkie atrybuty niekluczowe są w zależności funkcyjnej od klucza.

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
- możliwość łatwiejszego zrozumienie całego procesu komunikacji,
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

- warstwa aplikacji -
  - poziom, na którym pracują aplikacje użyteczne dla człowieka, np. serwer WWW lub przeglądarka internetowa
  -  Obejmuje zestaw protokołów, które aplikacje wykorzystują do przesyłania różnego typu danych w sieci
  - Wykorzystywane protokoły to m.in.: HTTP, FTP, etc
  - Przykładowe porty: ftp: 20, http: 80, https: 443
  - numer portu - 16b liczba całkowika. Zakres: 0-655535
- warstwa transportowa:
  - pakuje dane w pakiety
  - odpowiada za tworzenie połączeń
  - na podstawie numeru portu, wybiera odpowiedni protokół
  - TCP:
    - *Transmission Control Protocol*
    - zestawia połączenie pomiędzy komunikującymi się stronami przez zainicjowanie tzw. sesji
    - jest protokołem niezawodnym
    - odbiorca potwierdza otrzymanie każdej wiadomości
    - wiadomości dostarczane są w takiej samej kolejności, w jakiej zostały wysłane 
    - zeroko wykorzystywane w protokołach i aplikacjach, które wymagają wysokiej niezawodności (HTTP(S), FTP, SMTP)
  - UDP
    -  *User Datagram Protocol* 
    - komunikacja odbywa się bez nawiązywania żadnego stałego połączenia
    - pakiety wysyłane są niezależnie od siebie
    - szybsze niż TCP
    - nie zapewnia takiej niezawodności działania jak TCP
    - nie gwarantuje, że wiadomości rzeczywiście dotarły do odbiorcy.
    - nie dostarcza pakietów w takiej samej kolejności, w jakiej zostały one wysłane.
    - ciężar uporządkowania otrzymywanych wiadomości i sprawdzenia czy nie nastąpiły błędy transmisji spoczywa na otrzymującej je aplikacji
    - preferowane jeśli przesyłane pakiety danych są nieistotne lub komunikacja musi odbywać się z wyjątkowo dużą prędkością (DNS, DHCP, VOIP)
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
  - warstwy ethernetowe
    - **Logic Link Control (LLC)** - przekazanie informacji do docelowej maszyny odnośnie tego jaki protokół powinien być użyty w warstwie transportowej
    - **Media Access Control (MAC)** - zawiera adresy MAC nadawcy i odbiorcy, czyli fizyczne adresy dwóch komunikujących się maszyn, lub MAC routera, jeśli znajdują się w innej sieci
    - warstwa fizyczna

### Ocena złożoności algorytmów

https://pl.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/big-o-notation

https://edu.pjwstk.edu.pl/wyklady/nai/scb/wyklad6/w6.htm

###### Definicje

- Problem obliczeniowy - Jest to zbiór danych wejściwych, ich definicji oraz polecenie do wykonania.
  - problem sortowania liczb w tablicy
  - problem komiwojażera
  - problem plecakowy
- Algorytm - To uporządkowany zbiór kroków jakie należy kolejno wykonać celem znalezienia rozwiązania rozpatrywanego problemu.
- Problem rozstrzygalny – problem dla którego istnieje algorytm znajdujący rozwiązanie w skończonej liczbie kroków
- Problem nierozstrzygalny – problem dla którego udowodniono że nie istnieje algorytm znajdujący rozwiązanie w skończonej liczbie kroków
- Złożoność obliczeniowa - Miara efektywności algorytmu, czyli ilości zasobów potrzebnych do jego wykonania.
- Złożoność czasowa – oszacowuje zależność czasu potrzebnego do wykonania algorytmu od rozmiaru instancji rozwiązywanego problemu.
- Złożoność pamięciowa – oszacowuje ilość wymaganych zasobów pamięciowych do wykonania algorytmu w funkcji rozmiaru instancji problemu.
- Notacja dużego Theta:
  - Kiedy mówimy, że określony czas wykonania wynosi $\Theta(n)$, mówimy, że kiedy n stanie się wystarczające duże, czas wykonania wynosi, co najmniej $k_1\cdot n$ i co najwyżej  $k_2\cdot n$la niektórych stałych $k_1$ oraz $k_2$.
  - Kiedy używamy notacji dużego Theta, mówimy że czas wykonania jest **mocno związany asymptotycznie**
- Notacja dużego O:
  - jeśli czas wykonania jest ograniczony przez O(f(n)), to dla odpowiednio dużych n czas wykonania wynosi co najwyżej $k \cdot f(n)$ dla pewnej zmiennej k*k*k.
  - używamy w celu wyznaczenia **górnych granic asymptotycznych**, ponieważ ogranicza ona wzrost czasu wykonania dla dużych danych wejściowych.
- Notacja dużego Omega
  - algorytm zajmuje *przynajmniej* pewną ilość czasu bez podawania górnej granicy
  - używana do oznaczenia**asymptotycznej granicy dolnej** ponieważ ogranicza wzrost czasu wykonania od dołu dla odpowiedno dużych wartości podanych na wejściu.
- Staramy się określić złożoność jak najdokładniej

###### Klasy złożoności

- O(1) - złożoność stała
- O(log(n)) - złożoność logarytmiczna
- O(n) - złożoność liniowa
- O(nlog(n)) - złożoność liniowo - logarytmiczna
- O($n^k$) - złożoność wielomianowa (k - stała)
- O($k^n$), O(n!) - złożoność wykładnicza

###### Problemy decyzyjne

- Klasa **P** - wszystkie problemy, które można rozwiązać deterministycznym algorytmem o złożoności wielomianowej
- Klasa **NP** - wszystkie problemy, które można rozwiązać niedeterministycznym algorytmem wielomianowym
- Klasa **NP-zupełne** - Problem $P$ jest NP-Zupełny jeśli:
  - $P_0$ należy do klasy NP,
  - każdy problem z klasy NP da się sprowadzić w czasie wielomianowym do problemu $P_0$.
- Klasa **Np-trudne**
  - każdy problem z klasy NP da się sprowadzić w czasie wielomianowym do problemu  $P_0$.
- **PSPACE** - jest zbiorem wszystkich problemów decyzyjnych, które można rozwiązać za pomocą maszyny Turinga wykorzystującej wielomianową przestrzeń.

### Język UML w projektowaniu oprogramowania

*https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B6%5D%20Jezyk%20UML%20w%20projektowaniu%20oprogramowania/tekst/1.pdf*

###### UML 

- formalny opis modelu reprezentującego projekt informatyczny

- stosuje się do zdefiniowania systemu oprogramowania.
- zestaw pojęć, oznaczeń i diagramów
- pozwala jednoznacznie określić znaczenie graficznego obrazu modelu

###### Składowe modelu

- elementy modelu (klasy, interfejsy, przypadki użycia)
- związki (relacje, generalizacje)
- diagramy (klas, przypadku użycia, ...)



###### Diagramy

- diagram pakietów
- **diagram klas**:
  - przedstawia klasy i relacje między nimi
  - prezentowane są atrybuty, operacje i powiązania 
- diagram struktur złożonych
- diagram komponentów
- diagram wdrożenia
-  **diagram przypadków użycia**:
  - technika wyznaczania funkcjonalnych wymagań systemu
  - opisywanie typowych interakcji między użytkownikami systemu a samym systemem
  - przegląd możliwych działań w systemie
- diagram czynności
- **diagram maszyny stanowej**
  - przedstawia zachowania systemu i jego zmiany
  - stany obiektu połączone strzałkami
  - obiekt reagując na zdarzenia zmienia stan, lub pozostaje w obecnym w zależności od spełnienia warunków
- diagram interakcji (sekwencji, komunikacji, przeglądu interakcji)
- diagram uwarunkowań czasowych

### Generowanie realistycznych obrazów scen 3-D za pomocą metody śledzenia promieni

*źródło https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B7%5D%20Generowanie%20realistycznych%20obrazow%20scen%203D%20za%20pomoca%20metody%20sledzenia%20promieni/tekst/2.pdf*

###### Metoda śledzenia promieni:

- symulacja zachowania światła w realnym świecie.
- promień może się odbijać i zmieniać kierunek.
- obiekty są wykonane z różnych materiałów; mogą pochłaniać i odbijać różne barwy składowe światła

###### Działanie:

- promień śledzony jest od oka obserwatora, zatem od końca, czyli od oka obserwatora
- jeśli promień trafi w jakiś obiekt, można obliczyć kolor tego promienia, np. z metody Phonga
- po odbiciu można śledzić 2 promienie - odbity i załamany
- jeśli nie trafi w żaden ogień, jako kolor promienia przyjmowany jest kolor tła 
- śledzenie odbywa się zwykle w sposób rekurencyjny

Końcowo można uzyskać efekt odbijania się przedmiotów w innych przedmiotach, albo efekt załamania światła na granicy ośrodków

###### Charakterystyka

- wysoki koszt obliczneniowy (należy przeprowadzić procudure RT dla każdego piksela)
- możliwe równoregłe obliczenia dla każdego promienia lub piksela

###### Model oświetlenia Phonga

- pozwala obliczyć kolor wybranego obiektu na powierzchni trójwymiarowego obiektu
- zakłada istnienie 3 składowych światła:
  - składowej ambientowej 
    - światło otoczenia
    - stałe natężenie, niezależne od obserwatora, obiektu, ani źródła światła
  - rozproszonej
    - determinuje podstawowy kolor obiektu
    - model światła rozproszonego - model Lamberta
    - natężenie światła rozproszonego jest wprost proporcjonalne do cosinsusa kąta między wektorem normalnym, a promieniem pochodzącym od źródła światła
  - odbitej
    - odpowiada za efekt połysku
    - cosinus kąte między promieniem pochodzącym od obserwatora, a odbitym od powierzchni od powierzchni promieniem światła do potęgi n. n może wynosić od kilkudziesięciu do kilkuset
    - n - stała charakterystyczna dla materiału. Im większe n tym mniejsza średnica połysku
- zsumowanie składowych daje kolor wynikowy



### Mechanizmy systemu operacyjnego wspomagające synchronizację procesów

*źródło https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B8%5D%20Mechanizmy%20systemu%20operacyjnego%20wspomagajace%20synchronizacje%20procesow/tekst/1.pdf*

*https://www.ii.uni.wroc.pl/~wzychla/ra2223/so2.html*

**Synchronizacja procesów** to klasyczny problem z dziedziny informatyki ustalenia kolejności działania procesów ze sobą współpracujących. Problem pojawia się tam, gdzie występują współbierzne procesy. Celem jest ograniczenie dostępu do zasobu tak, aby dopuszczalne były przeploty zgodnie z wolą programisty

**Klasyczne problemy synchronizacji**

- problem producenta i konsumenta
- problem ucztujących filozofów
- problem czytelników i pisarzy
- problem sekcji krytycznej

**Programowe mechanizmy synchronizacji**

- semafory - procesy z nich korzystające mogą blokować wejście do określonych części kodu
- muteksy - mutex może być uwolniony tylko przez wątek, który jest jego właścicielem, licznik semafora może być zwiększony przez dowolny wątek, który z tego semafora korzysta.
- zmienne warunkowe - narzędziem do blokowania wątku wewnątrz sekcji krytycznej aż do momentu gdy pewien warunek zostanie spełniony



### Programowalne scalone układy cyfrowe PLD, CPLD oraz FPGA

*źródło https://lucc.pl/inf/egzamin_inzynierski/kierunkowe/%5BK%5D%5B9%5D%20Programowalne%20scalone%20uklady%20cyfrowe%20PLD%2C%20CPLD%2C%20oraz%20FPGA/tekst/1.pdf*

Programowalne układy cyfrowe to :

- układy scalone, których właściwości funkcjonalne są definiowane nie przez producenta, lecz przez końcowego użytkownika
- najważniejszą cechą tych układów jest możliwość nadawania im (w procesie analogicznym do programowania komputerów) określonych przez użytkownika cech funkcjonalnych, w jego laboratorium, a nie w fabryce.
- są przydatne gdy nie istnieje układ realizujący takie zadanie
- w stosunku do układów nieprogramowalnych są wolniejsze i mają większy pobór mocy
- realizują funkcje logiczne
- programowane za pomocą VHDL lub Veriloga 

Programowalne układy scalone są komponentami przeznaczonymi do budowy rekonfigurowalnych układów cyfrowych. PLD (*Programmable Logic Device*) jest rodziną programowalnych układów cyfrowych:

- SPLD (Simple PLD) - pozwalają na tworzenie nieskomplikowanych układów. 

  - ich budowa obiera się o matryce funkcji AND oraz OR
  - realizują funkcje w postaci (x1 AND x2 AND x3 …) OR (x1 AND x2 AND x3 …)… lub (x1 OR x2 OR x3 …) AND (x1 OR x2 OR x3…)…
  - dostępne jest kilka przerzutników - zwykle tyle ile wejść/wyjść do układu

- CPLD (Complex PLD)

  - większe zasoby i możliwości funkcjonalne
  - budowa hierarchiczna w oparciu o mikrokomórki, które są połączone w <u>bloki funkcyjne</u>
  - pojedyńcza makrokomórka realizuje prostą funkcję logiczną
  - połączone makrokomórki mogą realizować funkcje z większą liczbą zmiennych
  - pomiędzy blokami funkcyjnymi może zachodzić wymiana informacji

- FPGA (Field Programmable Gate Array):

  - brak matryc funkcyjnych
  - wyniki funkcji przechowuje się w tzw. LUT (Look Up Table)
  - składa się z bloków funkcyjnych (CLB)
  - CLB:
    - zawiera kilka LUT, które mogą być łączone w większe funkcje lub pełnić funkcje pamięci rozproszonej
    - zawiera kilka przerzutników
  - programowalne są połączenia między blokami funkcyjnymi

  

### Optyczne nośniki informacji.

**Optyczny nośnik informacji** to ciało fizyczne, na którym możliwe jest zapisanie/odczytanie danego rodzaju informacji przez oświetlenie nośnika promieniem lasera.

###### Płyty:

- CD - *Compact Disc* - 700MB
- DVD - *Digital Video Disc* - od 4.7 do 17GB (dwustronne dwuwarstwowe) 
  - osiągnięte przez krótszą falę lasera. 
  - Musi zawierać system plików - UDF
- Blue Ray Disc - 25 - 400GB (szesnastowarstwowe) 

###### CD - działanie

- Stany logiczne repreentowane przez wgłębienia (pity) i przerwy między wgłębieniami (landy)
- natrafienie na land - rozproszenie, nie powraca do czujnika
- pit - odbicie - powrót do czujnika

###### Rodzaje CD/DVD

- CD powstające na skutek odciśnięcia matryce
- CD-R - możliwy zapis danych
- CD-RW - podobne do CD-R, jednak umożliwiające wielokrotny zapis danych
- +R 
  - muszą być sformatowane przed rozpoczęciem nagrywania czego nie wymaga format –R.
  - zastosowanie systemu kontroli prędkości i zapisu ADIP, który jest mniej podatny na zakłócenia i błędy,

###### Obszary płyty kompaktowej:

- Lead In Aread - spis treści, czyli dane o położeniu i trwaniu każdej ścieżki na dysku
- Program Area - ramki, na które podzielona jest każda ścieżka. Ramka zawiera dane audio, bity parzystości, słowo synchronizujące i bajt kontrolny
- Lead Out Area - strefa ciszy. Pełni rolę bufora na wypadek pominięcia przez odtwarzacz ostatniej ścieżki na płycie

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
  - wykorzystuje lasery zielony i czerwony