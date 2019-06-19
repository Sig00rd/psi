Eksperyment Affective Computing - Podstawy Sztucznej Inteligencji 2018/2019
---------------------------------------------------------------------------

Zawartość folderu:
* 2019-afcai-spring.zip - folder z danymi (szczegóły niżej)
* IAPS.csv - informacja o nacechowaniu emocjonalnym każdego z obrazków (valence i arousal)
* IADS2.csv - informacja o nacechowaniu emocjonalnym każdego z dźwięków (valence i arousal)
* NEO-FFI.txt - wyniki kwestionariusza osobowości (nie był dostępny dla osób w pierwszym tygodniu badań)
* NAPS_analysis.ipynb - gdyby ktoś nie wiedział jak rozpocząć to tutaj przykładowa wstępna analiza danych z POPRZEDNIEGO eksperymentu (więc inne zbiory, inne urządzenia, ale ogólny workflow synchronizacji danych czy cięcia danych na fragmenty można obejrzeć)
* READINGS - różne dokumenty do OPCJONALNEGO poczytania: instrukcja osoby badanej, raporty dot. IAPS/IADS, artykuły GEIST dot. analizy danych czy gier

Dane z różnych plików synchonizujemy za pomocą:
* ID - 4-cyfrowy numer identyfikujący osobę badaną
* timestamp - do łączenia współwystępowania w czasie (np. bodziec na ekranie i zmiana sygnału EKG)

***************************************************

Wyniki kwestionariusza NEO-FFI:
* jest to tzw. "Wielka Piątka": otwartość (OTW), sumienność (SUM), neurotyczność (NEU), ugodowość (UGD), ekstrawersja (EKST)
* wyniki są podane na skali stenowej (1-10); Wartości 1-3 = niski poziom cechy, 4-6 = średni poziom, 7-10 = wysoki poziom
* W analizach można sprawdzać czy konkretny profil osobowości ma jakieś charakterystyki (układ cech, np. wysoka Neurotyczność + niska Ekstrawersja + ...) ale można też sprawdzać każdy z wymiarów z osobna (czy wysoka/przeciętna/niska Neurotyczność ma wpływ)

***************************************************

Folder z danymi ma 4 podfoldery:
* bitalino: zawiera pliki .txt z zapisanymi danymi z sensorów EKG i EDA/GSR; nazwa pliku rozpoczyna się od 4-cyfrowego ID osoby badanej
  - interesują nas kanały A5 (EKG) i A6 (GSR/EDA) = ostatnie dwie kolumny pliku
  - opis formatu pliku znajduje się w specyfikacji: http://bitalino.com/datasheets/OpenSignals_File_Formats.pdf
* procedura: dla każdej osoby badanej zawiera dwa pliki .txt [ID]_[data].txt oraz [ID]_[data]_info.txt
  - pierwszy zawiera w kolejnych kolumnach:
    i) ID osoby badanej
    ii) numer kolejny bodźca
    iii) warunek badawczy: spójny (con) vs niespójny (inc)
    iv) szczegółowy warunek badawczy: w postaci pXsX, gdzie X to - (negatywny) / 0 (neutralny) / + (pozytywny); p = picture, s = sound
    v) numer dźwięku z bazy IADS2 (charakterystyka dźwięku do pobrania z IADS2.csv)
    vi) numer obrazka z bazy IAPS (charakterystyka obrazka do pobrania z IAPS.csv)
    vii) wykorzystany widżet: emospace1 (wybór w przestrzeni dwuwymiarowej Valence x Arousal) vs emospace1 (wybór jednej z pięciu emotikon)
    viii) odpowiedź wybrana w widżecie: dwie wartości w przedziale [-1, 1] dla emospace1 (pierwsza = Valence; druga = Arousal), wartość ze zbioru {1,2,3,4,5} dla emoscale1
    ix) czas wyboru odpowiedzi w sekundach
    x) timestamp pojawienia się bodźca (do sparowania z danymi z bitalino)
  - drugi zawiera informację o ID (jest również w nazwie pliku), o wieku i płci osoby badanej
* space: logi z pierwszej gry (SpaceShooter 2.0):
  - pierwsza kolumna to czas w milisekundach od rozpoczęcia gry (do synchronizacji danych należy wykorzystać Unix Time dostępny w pierwszym/drugim wierszu w tej kolumnie; oznaczony jako Unix Time)
  - kolejne kolumny to szczegóły zdarzenia
* freud: logi z drugiej gry (Freud 2.0): jak wyżej

Jednostki trzeba przeliczyć z surowych danych zgodnie z Transfer Function w specyfikacjach (wartość zapisana w logach to "ADC - value sampled from the channel"):
* EKG: http://bitalino.com/datasheets/REVOLUTION_ECG_Sensor_Datasheet.pdf
* GSR/EDA: http://bitalino.com/datasheets/REVOLUTION_EDA_Sensor_Datasheet.pdf

***************************************************

CELE PROJEKTU (można obrać różne kierunki; wybrane z poniższych albo jakieś własne pomysły - każdą grupę proszę o kontakt w celu potwierdzenia/ustalenia tematu projektu; nie oznacza to zobowiązania do zrobienia projektu - chcę mieć pewność, że wiedzą Państwo co i jak chcą zrobić i że to ma jakiś sens - w razie problemów w każdej chwili można zrezygnować z projektu i wybrać drugiego Bossa):

Analiza 1: stworzyć model, który na podstawie danych o akcji serca (EKG) i reakcji skórno-galwanicznej (przewodność skóry; EDA/GSR) przewiduje aktualną emocję (poziom valence i arousal)

Analiza 2: j.w. ale sprawdzić czy był wpływ osobowości? (z kwestionariusza NEO-FFI)

Analiza 3: czy był wpływ osobowości na charakterystyki sygnału EKG i GSR? i nawet krok dalej: czy da się stworzyć model predykcji?

Analiza 4: sprawdzić jak w ogóle mają się oceny bodźców raportowane przez użytkowników do ocen bodźców dostarczonych w charakterystykach IADS/IAPS? Czy jest jakiś wpływ osobości?

Analiza 5: co jest silniejsze w niespójnym warunku (inc): dźwięk vs obraz? a może negatywne vs pozytywne? (np. nieważne czy negatywny jest dźwięk czy obraz, ważne że co najmniej jedno jest negatywne i całość też jest negatywna)

Analiza 6: analiza użycia widżetów: czy wartości wybierane mają jakieś charakterystyki? Jakie były rozkłady wybieranych wartości? Jak zależały od osobowości?

Analiza 7: czy istnieją jakieś ciekawe zależności pomiędzy logami z gier, osobowością i danymi sensorycznymi?

Analiza 8: było pięć rodzajów asteroid w SpaceShooter: szare (podczas spawnowania w logach pojawia się typ = -1) oraz kolorowe reprezentujące różne spójne/niespójne warunki (typ = 0,1,2,3). Czy któreś z nich były częściej zestrzeliwane, a której mniej często?

Analiza 9: [miejsce na Twoją reklamę]


Uwagi:
* można próbować przewidywać konkretny poziom valence/arousal, a można podzielić to na jakieś dyskretne wartości (np. wysoki/neutralny/niski jak w przykładowej analizie); wartości valence/arousal są w przedziałach [1,9] dla IAPS/IADS i w przedziale [-1,1] dla widżetu
* emocja to nie tylko konkretny poziom sygnału z sensorów, ale też: (a) zmiana względem poziomu początkowego (więc może jakoś normalizować wartości do jakiegoś poziomu bazowego?), (b) zmiana w czasie (więc możemy brać próbki z kolejnych momentów czasowych jako wejścia)
* najbardziej interesujące będzie około 10-15 sekund od pojawienia się obrazka; w tym czasie coś się może dziać z HR i GSR
* dane mogą nie być kompletne, mogą być poza skalą, etc - warto sprawdzić przed rozpoczęciem analiz
* danych jest DUŻO i raczej nie chcemy wrzucać do sieci WSZYSTKICH próbek, bo to się mija z celem (biorąc pod uwagę też szumy w danych) - warto zrobić jakiś preprocessing (uśrednianie wartości, wyciąganie jakichś charakterystyk sygnałów)

