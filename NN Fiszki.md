#nn

# Sieci neuronowe 2024

## Wykład 2

Czym wyróżnia się perceptron prosty (Model Pittsa-Mc Cullocha)
?
Funkcja aktywacji zwraca dwie wartości - neuron jest pobudzony albo nie. Dodatkowo nie ma elementu nauki.

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


## Wykład 3

Jak wyglądają funkcje aktywacji i ich pochodne: **sigmoid, tangens hiperboliczny, relu, softplus**.
![[Pasted image 20241203134856.png]]


Czym jest N-Fold Cross-Validation i kiedy warto jej użyć
?
![[Pasted image 20241203135230.png]]


## Wykład 4

Jakie są strategie zmiany wag
?
- **Stochastic Gradient Descent**: uaktualnianie wag (parametrów) po każdym wzorcu. Cechuje się dużą wariancją funkcji kosztu :(
- **Minibatch Gradient Descent**: uaktualnianie wag po m wzorca (m rozmiar minibatcha). Redukuje wariancją (lepiej zbiega).
- **Batch Gradient Descent**: uaktualnianie wag po wszystkich wzorcach uczących (po całej epoce, of line training). Gwarantuje zbieżność do globalnego optimum :)

Jak za pomocą sigmoidu wyrazić tangens hiperboliczny
?
$\tanh(x) = 2sigm(2x) - 1$


Czym jest problem zanikającego gradientu
?
Bardzo duże lub małe pobudzenie neuronów, powoduje że aktywacja dla sigmoida lub tanh wynosi zawsze 0 lub 1. To prowadzi do niskich wartości gradientu, co przekłada się na wartość zmiany wag (a raczej jej brak). Poza funkcją aktywacji, odpowiedzialne za to zjawisko może być zła inicjalizacja wag - 
nadanie im zbyt dużej wartości początkowej. Jeśli mamy do czynienia z zanikającym gradientem, warto zastosować RELU.

Czym jest problem wybuchającego gradientu
?
Korzystanie z RELU może powodować wysokie wartości gradientu, które w wyniku metody łańcuchowej mogą się zbytnio wyskalować. Aby temu zapobiec można zastosowoać obcinanie gradientu powyżej ustalonego progu albo leaky RELU
![[Pasted image 20241203170111.png]]

Bias a wariancja
?
![[Pasted image 20241203170638.png]]

## Wykład 5

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




















