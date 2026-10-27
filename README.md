**Polski** · [English](README.en.md)

---

# Matura z informatyki, poziom rozszerzony - kurs Pythona, część 5. "Pętle"

> ### 🎬 Wideo z omówieniem
> Pełne omówienie tej lekcji krok po kroku znajdziesz na moim kanale YouTube:
> **[Link do filmu na YouTube](https://youtu.be/MKseAN-Qnrg)**
>
> Na filmie pokazuję w Pythonie pętlę while, konstrukcję while True z instrukcją break, instrukcję continue, pętlę for z funkcją range, przeglądanie listy i napisu oraz pętlę w pętli.

---

## Opis

To piąta część mojego kursu Pythona, który przygotowuje do matury z informatyki na poziomie rozszerzonym. W poprzedniej części omawiałem instrukcje warunkowe. Teraz przechodzę do pętli.

Pętle pozwalają wykonywać te same operacje wiele razy i bardzo często pojawiają się przy implementacji algorytmów. Zwykle współpracują z instrukcjami warunkowymi, dlatego wprowadzam je zaraz po nich. Python ma dwa rodzaje pętli: `while` i `for`. Pętla `while` działa tak długo, jak spełniony jest określony warunek. Pętlę `for` wykorzystujemy najczęściej wtedy, gdy liczba obiegów jest ustalona z góry, albo do przeglądania kolejnych elementów listy lub napisu.

Repozytorium zawiera pliki z kolejnych lekcji kursu. Kod omawiany w tym nagraniu znajduje się w pliku `app-5-petle.py`.

## Wymagania

- Python 3.10 lub nowszy, ponieważ plik `app-4-instrukcje-warunkowe.py` korzysta z instrukcji `match`. Sam plik `app-5-petle.py` działa już w Pythonie 3.8, bo wymaga tylko f-stringów z zapisem `{n=}`.
- Brak zewnętrznych zależności. Kod korzysta wyłącznie z biblioteki standardowej (moduły `random` i `math`).

## Uruchomienie

```bash
git clone https://github.com/kmprograms/matura-kurs-python-5-petle
cd matura-kurs-python-5-petle
python app-5-petle.py
```

Pozostałe pliki uruchamiasz w ten sam sposób, podając ich nazwę. Żaden z nich nie czeka na dane z klawiatury, bo fragment z funkcją `input` w pliku `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` jest zakomentowany.

Program `app-5-petle.py` losuje wartość `n` z przedziału od 1000 do 9999, dlatego wynik pierwszego przykładu zmienia się przy każdym uruchomieniu. Pozostałe wyniki są zawsze takie same.

## Struktura projektu

| Plik | Opis |
| --- | --- |
| `app-1-pierwszy-program-zmienne.py` | Pierwszy program, zmienne, f-stringi z formatowaniem, operatory arytmetyczne, zamiana wartości zmiennych, argumenty `end` i `sep` funkcji `print`, zamiana typów oraz operatory `+=`, `-=` i `*=` |
| `app-2-liczby-calkowite.py` | Liczby całkowite: operatory `**`, `//` i `%`, parzystość i podzielność, operatory relacji, spójniki `and` i `or`, wyznaczanie cyfr liczby, zamiana sekund na godziny, minuty i sekundy |
| `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` | Pobieranie danych funkcją `input` (zakomentowane), losowanie liczb modułem `random`, systemy liczbowe, operacje bitowe i funkcje modułu `math` |
| `app-4-instrukcje-warunkowe.py` | Wyrażenia logiczne i leniwe obliczanie, `if`, `if ... else`, `if ... elif ... else`, wyrażenie warunkowe, instrukcja `match`, funkcje `min`, `max` i `abs` |
| `app-5-petle.py` | Pętla `while`, `while True` z `break`, instrukcja `continue`, pętla `for` z funkcją `range`, przeglądanie listy i napisu, pętla w pętli. Plik omawiany w tym nagraniu |

## Treść przykładów i sposób rozwiązania

### Jak działa pętla while

Pętla `while` przypomina instrukcję `if`. Po słowie kluczowym `while` zapisujesz warunek, a pod nim, we wcięciu, ciało pętli. Różnica polega na tym, że po wykonaniu ciała pętli program nie idzie dalej, tylko wraca do warunku i sprawdza go ponownie. Pętla powtarza się, dopóki warunek jest prawdziwy. Gdy warunek przyjmie wartość `False`, program przechodzi do instrukcji zapisanych pod pętlą. Jeżeli warunek jest fałszywy już przy pierwszym sprawdzeniu, pętla nie wykona się ani razu.

### Przykład 1. Potęgi dwójki

Polecenie z kodu: wypisz potęgi dwójki o wykładniku naturalnym mniejsze od wartości w zmiennej `n`, czyli 1, 2, 4, 8 i tak dalej. Wartość `n` jest losowana wywołaniem `random.randint(1000, 9999)`.

```python
p = 1
while p <= n:
    print(f"Kolejna potęga 2: {p}")
    p *= 2
print("Koniec potęg 2.")
```

Zmienna `p` zaczyna od 1, czyli od 2 do potęgi zerowej. W każdym obiegu pętla wypisuje bieżącą potęgę, a instrukcja `p *= 2`, czyli skrócony zapis `p = p * 2`, przechodzi do następnej potęgi. Pętla kończy się, gdy `p` przekroczy `n`. Wtedy program wypisuje komunikat o końcu potęg.

### Przykład 2. Suma kolejnych liczb do 50

Polecenie: dodawaj kolejne liczby naturalne dodatnie, dopóki suma nie przekroczy 50. Pokazuję dwa rozwiązania, które dają ten sam wynik.

Wersja 1 zapisuje warunek w nagłówku pętli. Ten warunek mówi, kiedy pętla ma się powtarzać.

```python
suma_calkowita = 0
k = 1
while suma_calkowita + k <= 50:
    suma_calkowita += k
    k += 1
print(f"{k - 1}, {suma_calkowita}")
```

Wersja 2 to pętla `while True`, której warunek jest zawsze prawdziwy. Warunek w instrukcji `if` działa odwrotnie niż w wersji 1, czyli określa, kiedy pętlę trzeba opuścić. Instrukcja `break` natychmiast przerywa pętlę i program przechodzi do kodu zapisanego pod nią.

```python
suma_calkowita = 0
k = 1
while True:
    # Określasz warunek, który musi zajść, żeby pętla się skończyła
    if suma_calkowita + k > 50:
        break  # Natychmiastowe przerwanie pętli

    suma_calkowita += k
    k += 1
print(f"{k - 1}, {suma_calkowita}")
```

W obu wersjach po zakończeniu pętli zmienna `k` przechowuje liczbę, której dodanie przekroczyłoby limit. Tę liczbę trzeba odrzucić, dlatego wynikiem jest `k - 1`. Suma 1 + 2 + ... + 9 wynosi 45, a dodanie 10 dałoby 55, czyli więcej niż 50.

W tym zadaniu wersja 1 jest lepsza. Konstrukcja `while True` przydaje się wtedy, gdy przed sprawdzeniem warunku albo po nim trzeba wykonać dodatkowe instrukcje. To kwestia wygody zapisu w konkretnej sytuacji, a w kodzie spotkasz się z oboma podejściami.

### Przykład 3. Suma liczb niepodzielnych przez 3

Polecenie: dodawaj kolejne liczby naturalne dodatnie niepodzielne przez 3, dopóki suma nie przekroczy 50. Ten przykład wprowadza instrukcję `continue`.

```python
suma_calkowita = 0
ostatnia_dodana = 0
k = 0

while True:
    k += 1  # Tutaj decydujemy się na zwiększenie zmiennej o 1, żeby
    # continue nie zablokowało pętli

    if k % 3 == 0:
        continue  # Pominięcie reszty ciała pętli i przejście do
        # kolejnego obiegu

    if suma_calkowita + k > 50:
        break  # Natychmiastowe przerwanie pętli

    suma_calkowita += k
    ostatnia_dodana = k

print(f"{ostatnia_dodana}, {suma_calkowita}")
```

Instrukcja `continue` pomija resztę ciała pętli i przechodzi do kolejnego obiegu. Pętla się nie kończy, kończy się tylko bieżący obieg. Gdy `k` jest podzielne przez 3, liczba nie trafia do sumy i nie zostaje zapisana w `ostatnia_dodana`. Dopiero gdy dodanie kolejnego `k` przekroczyłoby 50, instrukcja `break` kończy całą pętlę. W skrócie: `continue` przerywa obieg, a `break` całą pętlę.

Zmienna `k` startuje od 0 i jest zwiększana na samym początku obiegu. To ważne. Bez tej instrukcji `k` cały czas miałoby wartość 0, a 0 jest podzielne przez 3. Wtedy `continue` wykonywałoby się w każdym obiegu, `k` nigdy by się nie zmieniło, a pętla kręciłaby się w nieskończoność.

Zmienna `ostatnia_dodana` przechowuje ostatnią liczbę, która trafiła do sumy. Tutaj nie wystarczy wypisać `k - 1` jak w przykładzie 2, bo poprzednia wartość `k` mogła zostać pominięta przez `continue`.

### Pętla for i funkcja range

W typowych zadaniach maturalnych pętla `while` zależy od konkretnego warunku, a pętla `for` służy raczej do wykonania z góry ustalonej liczby obiegów. Funkcja `range` dostarcza kolejne wartości, które w każdym obiegu trafiają do zmiennej pętli.

```python
for i in range(5):  # range(n) dostarcza kolejne wartości od 0 do n - 1
    print(i, end=" ")
```

Argument `end=" "` sprawia, że po każdej wartości pojawia się spacja zamiast nowej linii.

Gdy wartość zmiennej pętli nie jest potrzebna, a liczy się tylko liczba powtórzeń, w miejscu nazwy zmiennej wpisujesz `_`. W Pythonie ten znak oznacza, że wartość Cię nie interesuje. Składnia języka wymaga jednak, żeby w tym miejscu coś stało.

```python
for _ in range(5):
    print("Wykonuje się pewna operacja")
```

Warianty `range` z pliku `app-5-petle.py`:

| Etykieta | Wywołanie | Wartości |
| --- | --- | --- |
| `For - 1` | `range(5)` | 0 1 2 3 4 |
| `For - 3` | `range(2, 10)` | 2 3 4 5 6 7 8 9 |
| `For - 4` | `range(2, 20, 3)` | 2 5 8 11 14 17 |
| `For - 5` | `range(20, 1, -2)` | 20 18 16 14 12 10 8 6 4 2 |

Wartość końcowa nigdy nie jest brana pod uwagę. Trzeci argument to krok. Może być ujemny i wtedy wartości maleją. Gdybyś w `For - 5` zmienił koniec przedziału z 1 na 2, ostatnią wypisaną wartością byłoby 4.

Numeracja od zera przyda się przy listach i napisach, w których pozycje elementów też liczy się od zera. Dzięki temu pętla `for` z `range` pozwoli wygodnie przeglądać elementy, gdy ważna będzie ich pozycja.

### Przeglądanie listy i napisu

Pętla `for` może też przeglądać elementy wprost, bez `range`. Lista to zestaw elementów zapisanych w nawiasach kwadratowych. Listy i napisy omówię dokładnie w kolejnych lekcjach kursu.

```python
liczby = [10, 32, 34, 45]
for liczba in liczby:
    print(liczba)
```

W każdym obiegu zmienna `liczba` dostaje kolejny element listy. Na tej samej zasadzie przeglądasz napis znak po znaku:

```python
imie = "Krzysztof"
for znak in imie:
    print(znak)
```

### break i continue w pętli for

Instrukcje `break` i `continue` działają w pętli `for` dokładnie tak samo jak w pętli `while`.

```python
for i in range(20):
    print(f"Przed {i=}")
    if i > 10:
        # break
        continue
    print(f"Po {i=}")
```

W wersji z `continue` dla `i` od 0 do 10 widać oba komunikaty, "Przed" i "Po". Dla `i` od 11 do 19 pojawia się tylko "Przed", bo `continue` pomija resztę obiegu. Jeżeli zamienisz `continue` na `break`, który jest w kodzie zakomentowany, pętla zakończy się po wypisaniu `Przed i=11`.

### Pętla w pętli

```python
for i in range(1, 5):
    for j in range(1, 5):
        print(f"{i=},{j=}", end="\t")
    print()
```

Dla każdej wartości `i` pętla wewnętrzna wykonuje się w całości, czyli `j` przyjmuje kolejno wartości od 1 do 4. Dopiero potem pętla zewnętrzna przechodzi do kolejnego obiegu. Pusty `print()` na poziomie pętli zewnętrznej przenosi wypisywanie do nowego wiersza. Taką konstrukcję wykorzystamy później do przeglądania struktur dwuwymiarowych.

## Wyniki

Wynik części z pętlą while dla wylosowanej wartości `n=1131`, tak jak na nagraniu:

```
n=1131
Przykład 1:
Kolejna potęga 2: 1
Kolejna potęga 2: 2
Kolejna potęga 2: 4
Kolejna potęga 2: 8
Kolejna potęga 2: 16
Kolejna potęga 2: 32
Kolejna potęga 2: 64
Kolejna potęga 2: 128
Kolejna potęga 2: 256
Kolejna potęga 2: 512
Kolejna potęga 2: 1024
Koniec potęg 2.
Przykład 2:
Wersja 1:
9, 45
Wersja 2:
9, 45
Przykład 3:
11, 48
```

Obie wersje przykładu 2 dają ten sam wynik `9, 45`. W przykładzie 3 ostatnią dodaną liczbą jest 11, a suma wynosi 48, czyli 1 + 2 + 4 + 5 + 7 + 8 + 10 + 11. Kolejna liczba niepodzielna przez 3 to 13, a 48 + 13 = 61 przekroczyłoby limit.

Wynik pętli w pętli:

```
For - 9:
i=1,j=1	i=1,j=2	i=1,j=3	i=1,j=4	
i=2,j=1	i=2,j=2	i=2,j=3	i=2,j=4	
i=3,j=1	i=3,j=2	i=3,j=3	i=3,j=4	
i=4,j=1	i=4,j=2	i=4,j=3	i=4,j=4	
```

## Uwagi implementacyjne

Komentarz z treścią przykładu 1 mówi o potęgach mniejszych od `n`, a w pętli stoi warunek `p <= n`. Gdy wylosowane `n` samo jest potęgą dwójki (1024, 2048, 4096 lub 8192), też zostanie wypisane. Jeżeli treść zadania wymaga ścisłej nierówności, wystarczy zmienić warunek na `p < n`.

Zmienne `suma_calkowita` i `k` są używane ponownie w przykładach 2 i 3. W tak krótkim pliku to świadoma decyzja. W większym programie łatwo w ten sposób przez przypadek nadpisać wartość, do której chcesz się później odwołać. Bezpieczniej wtedy wprowadzić nowe nazwy, na przykład `suma_calkowita2` i `k2`.

Pętla `while True` musi mieć w środku instrukcję `break`. Bez niej program utknie w pętli.

Jeżeli wiesz, że w danym miejscu będzie kod, ale jeszcze go nie napisałeś, możesz wpisać słowo `pass`. Wcięcie nie jest wtedy puste i w kodzie nie ma błędu.

Każdą pętlę `while` da się zastąpić pętlą `for` i odwrotnie. Nie ma jednak sensu robić tego na siłę. Wybierasz tę pętlę, którą w danej sytuacji zapiszesz wygodniej.

Gdy w dalszej części kursu pojawią się funkcje, część zachowań uzyskiwanych teraz przez `break` i `continue` osiągniemy odpowiednim podziałem programu na funkcje. Mimo to obie instrukcje trzeba znać.