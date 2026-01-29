<h1 align="center">Analiza i Prognozowanie Treści HBO Max</h1>

<p align="center">
  <b>Projekt analityczny skupiający się na badaniu dynamiki biblioteki filmów i seriali HBO/HBO Max przy użyciu modeli szeregów czasowych.</b>
</p>

<hr>

<h2>O Projekcie</h2>
<p>
  Celem projektu jest analiza historycznych trendów wydawniczych platformy HBO oraz zbudowanie modelu matematycznego <b>ARIMA (AutoRegressive Integrated Moving Average)</b>, który pozwala na prognozowanie liczby nowych tytułów w nadchodzących latach. Projekt łączy w sobie aspekty inżynierii danych, statystyki opisowej oraz uczenia maszynowego w analizie szeregów czasowych.
</p>

<p>
  Zdecydowałam się poszukać danych z platformy do streamowania filmów, ponieważ jest to dla mnie forma spędzania wolnego czasu i byłam ciekawa jakie dane są dostępne na ten temat oraz czy można przewidzieć ile filmów zostanie wydanych w następujących latach. Okazało się, że nie jest zbyt łatwo znaleźć takie dane, które by pasowały do analizy, jednak finalnie stanęło na datasecie z Hbo i Hbo Max.
</p>

<h2>Dataset</h2>
<p>
  Wykorzystany zbiór danych pochodzi z platformy Kaggle (<i>HBO and HBO Max Content Dataset https://www.kaggle.com/datasets/thedevastator/hbo-and-hbo-max-content-dataset/data </i>), stanowi kompleksowe zestawienie biblioteki multimedialnej obu serwisów. Dane zawierają metadane tysięcy produkcji, obejmując zarówno klasyczne tytuły <b>HBO</b>, jak i nowszą ofertę <b>HBO Max</b>. 
</p>
<p>
  Każdy rekord w zbiorze opisany jest szeregiem atrybutów, takich jak:
</p>
<ul>
  <li><b>title:</b> Pełna nazwa filmu lub serialu.</li>
  <li><b>type:</b> Klasyfikacja treści (Movie – film lub TV – serial).</li>
  <li><b>year:</b> Rok wydania produkcji.</li>
  <li><b>imdb_score & imdb_votes:</b> Wskaźniki popularności i oceny społeczności.</li>
  <li><b>genres:</b> Kategorie tematyczne przypisane do tytułów.</li>
  <li><b>rating:</b> Klasyfikacja wiekowa treści.</li>
</ul>

<h2>Wykorzystane Technologie</h2>
<ul>
  <li><b>Python 3.x</b></li>
  <li><b>Pandas & NumPy:</b> Czyszczenie, transformacja i agregacja danych.</li>
  <li><b>Matplotlib & Seaborn:</b> Wizualizacja trendów i wyników prognoz.</li>
  <li><b>Statsmodels:</b> Zaawansowana analiza statystyczna (Test Dickeya-Fullera, ACF/PACF, modelowanie ARIMA).</li>
  <li><b>Scikit-learn:</b> Ewaluacja modelu przy pomocy metryk błędu (MAE, RMSE, MAPE).</li>
</ul>

<h2>Etapy Postępowania</h2>

<h3>1. Przygotowanie i Czyszczenie Danych</h3>
<p>
  Proces rozpoczął się od wczytania danych z plików <code>HBO_Content.csv</code> oraz <code>HBO_MAX_Content.csv</code>. Kluczowe kroki to:
</p>
<ul>
  <li>Uzupełnienie braków w kolumnie <i>type</i> (przypisanie domyślnej wartości "Movie").</li>
  <li>Połączenie zbiorów danych i usunięcie duplikatów (na podstawie tytułów).</li>
  <li>Przekształcenie danych do formatu szeregu czasowego z indeksem rocznym.</li>
</ul>

<h3>2. Analiza Stacjonarności (EDA)</h3>
<p>
  Wizualizacja danych wykazała wyraźny trend wzrostowy po 2010 roku. Aby móc zastosować model ARIMA, przeprowadzono:
</p>
<ul>
  <li><b>Test ADF (Augmented Dickey-Fuller):</b> Wykazał, że oryginalne dane są niestacjonarne.</li>
  <li><b>Transformacje:</b> Zastosowano logarytmizację oraz różnicowanie (pierwszego i drugiego rzędu), aby ustabilizować średnią i wariancję szeregu.</li>
</ul>

<h3>3. Modelowanie ARIMA</h3>
<p>
  Na podstawie wykresów autokorelacji (ACF) i autokorelacji cząstkowej (PACF) oraz optymalizacji pod kątem kryterium <b>AIC (Akaike Information Criterion)</b>, dobrano parametry modelu:
</p>
<ul>
  <li>Dla filmów i seriali wybrano model <b>ARIMA(2, 1, 2)</b>.</li>
  <li>Dane podzielono na zbiór treningowy (80%) i testowy (20%) w celu weryfikacji prognoz.</li>
</ul>

<h3>4. Diagnostyka i Ewaluacja</h3>
<p>
  Ostatnim etapem była analiza jakości modelu:
</p>
<ul>
  <li>Sprawdzenie reszt modelu (czy mają charakter białego szumu i rozkład normalny).</li>
  <li>Obliczenie metryk błędu (np. MAPE), aby ocenić procentową dokładność przewidywań.</li>
</ul>

<h2>Interpretacja Wyników</h2>
<ul>
  <li><b>Dynamika wzrostu:</b> Produkcja treści na HBO Max gwałtownie przyspieszyła w ostatniej dekadzie, co jest widoczne na wykresach historycznych.</li>
  <li><b>Stabilność prognozy:</b> Model ARIMA(2,1,2) poprawnie identyfikuje kierunek zmian. Warto zauważyć, że prognozy długoterminowe dążą do średniej, co jest typową cechą modeli klasy ARIMA (tzw. powrót do średniej).</li>
  <li><b>Wnioski praktyczne:</b> Wyliczone przedziały ufności (95%) pozwalają oszacować pesymistyczny i optymistyczny scenariusz rozwoju biblioteki platformy.</li>
</ul>

<h2>Struktura Plików</h2>
<pre>
├── projekt_analiza_hbomax.py  # Kod źródłowy analizy
├── HBO_Content.csv            # Dane źródłowe HBO
├── HBO_MAX_Content.csv        # Dane źródłowe HBO Max
└── README.md                  # Opis projektu
</pre>

<h2>Jak uruchomić?</h2>
<p>Skopiuj repozytorium i zainstaluj wymagane zależności:</p>
<code>pip install pandas matplotlib seaborn statsmodels scikit-learn</code>
<p>Następnie uruchom skrypt:</p>
<code>python projekt_analiza_hbomax.py</code>
