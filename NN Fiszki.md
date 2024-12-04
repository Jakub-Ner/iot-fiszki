#nn

# Sieci neuronowe 2024

## Wykład 1

Czym wyróżnia się perceptron prosty (Model Pittsa-Mc Cullocha)
?
Funkcja aktywacji zwraca dwie wartości - neuron jest pobudzony albo nie. Dodatkowo nie ma elementu nauki.

<div style="page-break-before: always;"></div>

## Wykład 2

Czym wyróżnia się ADALINE
?
Podobne do perceptronu prostego ale celem jest znalezienie wag. Może mieć wiele wejść, ma jedno wyjście


Jakiej funkcji kosztu użyjemy dla sieci rozwiązującej problem regresji?
?
Mean Squared Error

Jakiej funkcji kosztu użyjemy dla sieci rozwiązującej problem klasyfikacji?
?
Cross Entropy - $H(p, \hat{p}) = -\frac{1}{N} \sum_{i=1}^N \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]$. 
W przypadku wieloklasowej klasyfikacji gdzie wyjścia są zakodowane jako 0 lub 1 stosuje się $\mathcal{L}_{CE} = -\sum_{k=1}^M y_k \ln(\hat{y}_k)$ (patrz wykład 3).

Jaka jest formuła sigmoidu
?
![[Pasted image 20241203131755.png]]


Czym jest gradient funkcji wielu zmiennych
?
Wektor wskazujący kierunek największego wzrostu. Składa się z pochodnych cząstkowych ∂ funkcji straty po wagach $∂w_{i}$ .

Czym jest softmax
?
![[Pasted image 20241203133046.png]]

<div style="page-break-before: always;"></div>

## Wykład 3

Jak wyglądają funkcje aktywacji i ich pochodne: **sigmoid, tangens hiperboliczny, relu, softplus**.
![[Pasted image 20241203134856.png]]


Czym jest N-Fold Cross-Validation i kiedy warto jej użyć
?
![[Pasted image 20241203135230.png]]

<div style="page-break-before: always;"></div>

## Wykład 4

Jakie są strategie zmiany wag
?
- **Stochastic Gradient Descent**: uaktualnianie wag (parametrów) po każdym wzorcu. Cechuje się dużą wariancją funkcji kosztu :(
- **Minibatch Gradient Descent**: uaktualnianie wag po m wzorca (m rozmiar minibatcha). Redukuje wariancją (lepiej zbiega).
- **Batch Gradient Descent**: uaktualnianie wag po wszystkich wzorcach uczących (po całej epoce, of line training), co zwiększa stabilność treningu (bo liczymy gradient dopiero po przejsciu przez cały zbiór uczący)

Jak za pomocą sigmoidu wyrazić tangens hiperboliczny
?
$\tanh(x) = 2sigm(2x) - 1$


Czym jest problem zanikającego gradientu
?
Bardzo duże lub małe pobudzenie neuronów, powoduje że aktywacja dla sigmoida lub tanh wynosi zawsze 0 lub 1. To prowadzi do niskich wartości gradientu, co przekłada się na wartość zmiany wag (a raczej jej brak). Poza funkcją aktywacji, odpowiedzialne za to zjawisko może być zła inicjalizacja wag - nadanie im zbyt małej lub dużej wartości początkowej. Jeśli mamy do czynienia z zanikającym gradientem, warto zastosować RELU.
![[Pasted image 20241204100032.png]]


Czym jest problem wybuchającego gradientu
?
Korzystanie z RELU może powodować wysokie wartości gradientu, które w wyniku metody łańcuchowej mogą się zbytnio wyskalować. Aby temu zapobiec można zastosowoać obcinanie gradientu powyżej ustalonego progu albo leaky RELU
![[Pasted image 20241203170111.png]]

Bias a wariancja
?
![[Pasted image 20241203170638.png]]

<div style="page-break-before: always;"></div>

## Wykład 5

Jak sobie radzić z przetrenowaniem modelu?
?
1. Regularyzacja wag (L1 lub L2)
2. Dropout
3. Wczesne zatrzymanie uczenia
4. Sztuczne powiększane zbioru uczącego

Na czym polega L2 (Ridge Regression)
?
1. **wzór**: $L(\theta) = L_0(\theta) + \lambda \frac{1}{2} \|\theta\|^2$, gdzie $\|\theta\|_2 = (w_1)^2 + (w_2)^2 + \ldots$, a $\lambda$ to hiperparametr. 
2. **opis**: Na zwiększeniu funkcji straty o kwadraty wag. Im bardziej skomplikowany model, tym większa kara. 
3. **wpływ na aktualizację wag:** zmniejsza wartości proporcjonalnie do ich wartości, ale nie ustawia ich na 0

Na czym polega L1 (Lasso Regression)
?
1. **wzór:** $L(\theta) = L_0(\theta) + \lambda \|\theta\|$, gdzie $\|\theta\| = |w_1| + |w_{2}| + \ldots$, a $\lambda$ to hiperparametr.
2. **opis:** Na zwiększeniu funkcji straty o wartości bezwględne wag. Im bardziej skomplikowany model, tym większa kara. 
3. **wpływ na aktualizację wag:** zmniejsza wagi niezależnie od ich wartości, w szczególności może je zerować - tym samym wyłączać neurony

Na czym polega Dropout
?
Z określonym prawdopodobieństwem na okres batcha wyłączamy losowe neurony w warstwie ukrytej. Przy każdej paczce wyłączamy inną część sieci. Możemy postrzegać tak wytrenowany model jako rodzina klasyfikatorów (wiele sieci złączone w jedną). Dropout wykorzystywany jest tylko przy treningu
![[Pasted image 20241204002559.png]]


Czym jest macierz pomyłek (confusion matrix)
?
![[Pasted image 20241204003242.png]]

Metryki
?
![[Pasted image 20241204003750.png]]

Czym jest F1 score
?
Średnia harmoniczna precyzji i recall

Czym jest krzywa AUC-ROC (Area Under Curve - Receiver Operating Characteristics)
?
Wykres True-Positive-Rave (**Specifity**) od False-Positive-Rate (Sensitivity). Pożądane jest aby pole pod wykresem było 1.
![[Pasted image 20241204003925.png]]

Wymień dobre praktyki w projektowaniu sieci MLP
?
- sprawdzenie czy zbiór jest zrównoważony
- kodowanie wartości nominalnych (kategorycznych)
- skalowanie i normalizacja cech o wartościach rzeczywistych
- liczba neuronów w warstwie ukrytej to $n_h = \frac{n_{in} + n_{out}}{2}$ lub $n_h = \sqrt{n_{in} n_{out}}$
- Po trenowaniu zwizualizuj gradienty w każdej warstwie sieci , jeśli większość z nich jest bliska 0 =>większość neuronów przestała się uczyć albo nie działa propagacja wsteczna.

<div style="page-break-before: always;"></div>

## Wykład 6

Na czym polega **Momentum** - metoda optymalizująca Gradient Descent
?
Pomaga radzić sobie z "wąwozami" poprzez nadanie "pędu". Do obecnego gradientu dodaje momentum (zakumulowany gradient z poprzednich kroków).
![[Pasted image 20241203171708.png]]



Na czym polega Nesterov Accelerated Gradient (NAG)
?
Bazuje na momentum, jednak najpierw robi krok wynikający z momentum, dopiero potem liczy gradient i robi kolejny krok.
![[Pasted image 20241203172200.png]]
![[Pasted image 20241203172413.png]]

Czym jest ADAGRAD
?
Jest to adaptacyjny współczynnik uczenia, który w z czasem maleje, przez kumulowanie gradientów w mianowniku, a to może powodować, że współczynnik uczenia będzie nieskończenie mały
![[Pasted image 20241203174453.png]]

Czym jest ADADELTA
?
Taki ulepszony ADAGRAD, tylko, że do wyliczenia współczynnika uczenia, bierzemy pod uwagę kilka ostatnich gradientów.


Czym jest Adam (Adaptive Moment Estimation)
?
Najczęściej wykorzystywany optymalizator. Estymuje średnią i wariancję gradientów i wykorzystuje je do aktualizacji wag. Bywa łączony z **NAG** (NAdam).

Co powoduje inicjalizacja wag na jednakową wartość (np. 0)
?
Prowadzi do jednakowego wpływu każdego neuronu na funkcję kosztu, a to powoduje, że każdy neuron uczy się tej samej cechy

Jak zainicjalizować wagi (najprostsza metoda)
?
1. $w \in \left[-\frac{a}{\sqrt{n_{\text{in}}}}, \frac{a}{\sqrt{n_{\text{in}}}}\right]$, gdzie $n_{in}$ to liczba wejść i $a$ zależy od funkcji aktywacji, 
- dla sigmoida $a=2.38$, 
- dla ReLU $a=\sqrt{ 2 }$,
- dla Tanh $a=1$. 
2. Można też brać pod uwagę ilość neuronów ukrytych $\left[-n_{\text{in}}\sqrt{N_h}, \, n_{\text{in}}\sqrt{N_h}\right]$. 
3. Neurony wyjściowe losuje się z przedziału $[-0.5, 0.5]$.

Jak zainicjalizować wagi korzystając z Xaviera
?
Dla każdej warstwy z osobna wylosuj z przedziału $\pm \frac{\sqrt{6}}{\sqrt{n_i + n_{i+1}}}$, gdzie $n_{i}$ to wejściowe a  $n_{i+1}$ wyjściowe. Biasy ustaw na 0.

Jak zainicjalizować wagi korzystając z He
?
TODO

Czym jest normalizacja batch'a
?
TODO

Czym jest Autokoder i jak się go trenuje
?
Jest to sieć wykorzystująca uczenie nienadzorowane. Składa się z enkodera i dekodera. Celem jest skompresowanie reprezentacji i odtworzenie jej.
![[Pasted image 20241203201235.png]]
![[Pasted image 20241203201529.png]]

<div style="page-break-before: always;"></div>

## Wykład 7

Czemu MLP nie radzą sobie za dobrze z obrazami
?
Reprezentacja obrazu w postaci wektora pozbawia sieć reprezentacji przestrzennej i zależności czasowej. Dodatkowo wykorzystanie pełnych połączeń jest wymagające obliczeniowo. 

Czym jest kernel (CNN)
?
Inaczej detektor lub filtr - wykrywacz cech, który w wyniku konwolucji - przesuwania się po obrazie z określonym krokiem, tworzy mape aktywacji. Filtr trzyma w sobie wagi.
![[Pasted image 20241203202801.png]]

Czym jest konwolucja
?
Jest to korelacja wzajemna okolicznych pikseli i filtra odbróconego o 180 stopni. Na zdjęciu wizualizacja kolejnych map aktywacji - niskopoziomowe cechy składają się w rozpoznawalne obiekty.
![[Pasted image 20241203203538.png]]

Czym jest i do czego wykorzystuje się Pooling
?
Pozwala na agregację (avg lub max) sąsiadujących pikseli. Redukuje liczbę parametrów modelu, pozwala na lepszą generalizację map cech. Pooling nie podlega uczeniu - nie ma wag. 
Propagacja wsteczna: 
- jeśli używamy max-pool obliczany jest błąd uzyskiwany przez zwycięską jednostkę (pozostałe błędy są równe 0, dlatego trzeba pamiętać indeks zwycięskiej jednostki). •
- Dla avg-pool błąd jest przypisywany do całego bloku i mnożony przez 1/(NxN)
![[Pasted image 20241203204218.png]]

Jaki sens w stosowaniu konwolucji dla filtra o rozmiarze 1x1
?
TODO

Jak przebiega formuła propagacji błędu w sieciach konwolucyjnych
?
XD, nie będzie takiego pytania

Czym jest VGG
?
Giga dużo warstw przeplatanych poolingiem. Na końcu 3 warstwy tradycyjnych sieci, a po nich softmax do klasyfikacji co jest na obrazku.
![[Pasted image 20241203205922.png]]

Co to GoogleNet
?
Jeszcze więcej warstw. Cała sieć składa się z nastackowanych bloków incepcji, które są jeszcze bardziej zagmatwane i wykorzystują konwolucje 1x1
![[Pasted image 20241203210010.png]]
![[Pasted image 20241203210108.png]]


Czym jest ResNet
?
Podobne do VGG ale wykorzystuje połączenia rezydualne (skrótowe) wyjście z wcześniejszych warstwach jest przekazywane na wyjście następnych warstw.
![[Pasted image 20241203210359.png]]

Gdzie stosuje się konwolucję 1D
?
Do przetwarzania danych czasowych (np cen akcji) lub sygnału.

<div style="page-break-before: always;"></div>

## Wykład 8

Czym cechuje się sieć rekurencyjna (RNN)
?
1. Może przetwarzać dane o dowolnej długości ("ala" i "ala ma kota")
2. Jest oparty na DAG (skierowanym grafie acyklicznym)
3. Cykle działają jako pamięć ($h_{i}$), która jest dodawana do wejścia ($x_{i}$)
4. Mamy tu do czynienia ze współdzieleniem parametrów -każdy $x_{0..n}$ jest przemnażany przez tę samą wagę $A^{i}$, a każdy $h_{0..n}$ jest przemnażany przez tę samą wagę $W^{i}$, gdzie $i$ to index warstwy.
5. Są wolniejsze a pamięć, działa tylko w teorii, chociaż **LSTM** i **GRU** starają się zwiększyć efektywność zapamiętywania
![[Pasted image 20241204094643.png]]

Czym jest Long-Short-Term-Memory (**LSTM**) 
?
Jest to RNN, który składa się z komórek, które poza pobudzeniem Z, mają 3 rodzaje bramek: **forget, input i output**
![[Pasted image 20241204100816.png]]


Czym jest Gated Recurrent Unit (**GRU**)
?
Alternatywa dla LSTM. Zastępuje dwie bramki (**forget** i **input**) bramką **update**. Wprowadza **reset**
![[Pasted image 20241204101116.png]]

Jakie są scenariusze zastosowań RNN?
![[Pasted image 20241204101739.png]]

LSTM w praktyce (to nie jest pytanie xd)
?
![[Pasted image 20241204101702.png]]
