[Polski](README.md) · **English**

---

# Computer Science Matura, extended level - Python course, part 5. "Loops"

> ### 🎬 Video walkthrough
> You can find a full step-by-step walkthrough of this lesson on my YouTube channel:
> **[YouTube video link](https://youtu.be/MKseAN-Qnrg)**
>
> In the video I show, in Python, the while loop, the while True construct with the break statement, the continue statement, the for loop with the range function, iterating over a list and a string, and nested loops.

---

## Description

This is the fifth part of my Python course, which prepares students for the Matura exam in computer science at the extended level. In the previous part I covered conditional statements. Now I move on to loops.

Loops let you perform the same operations many times and show up very often when implementing algorithms. They usually work together with conditional statements, which is why I introduce them right after conditionals. Python has two kinds of loops: `while` and `for`. A `while` loop runs as long as a given condition is met. A `for` loop is used most often when the number of iterations is known in advance, or to go through the elements of a list or a string one by one.

The repository contains files from consecutive lessons of the course. The code discussed in this video is in the file `app-5-petle.py`.

## Requirements

- Python 3.10 or newer, because the file `app-4-instrukcje-warunkowe.py` uses the `match` statement. The file `app-5-petle.py` on its own already runs on Python 3.8, since it only needs f-strings with the `{n=}` syntax.
- No external dependencies. The code uses only the standard library (the `random` and `math` modules).

## Running

```bash
git clone https://github.com/kmprograms/matura-kurs-python-5-petle
cd matura-kurs-python-5-petle
python app-5-petle.py
```

You run the other files the same way, by passing their name. None of them waits for keyboard input, because the fragment with the `input` function in `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` is commented out.

The program `app-5-petle.py` draws the value `n` from the range 1000 to 9999, so the output of the first example changes on every run. All other results are always the same.

## Project structure

| File | Description |
| --- | --- |
| `app-1-pierwszy-program-zmienne.py` | First program, variables, formatted f-strings, arithmetic operators, swapping variable values, the `end` and `sep` arguments of `print`, type conversion and the `+=`, `-=` and `*=` operators |
| `app-2-liczby-calkowite.py` | Integers: the `**`, `//` and `%` operators, parity and divisibility, relational operators, the `and` and `or` connectives, extracting the digits of a number, converting seconds into hours, minutes and seconds |
| `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` | Reading data with `input` (commented out), generating random numbers with the `random` module, number systems, bitwise operations and functions from the `math` module |
| `app-4-instrukcje-warunkowe.py` | Logical expressions and short-circuit evaluation, `if`, `if ... else`, `if ... elif ... else`, the conditional expression, the `match` statement, the `min`, `max` and `abs` functions |
| `app-5-petle.py` | The `while` loop, `while True` with `break`, the `continue` statement, the `for` loop with the `range` function, iterating over a list and a string, nested loops. The file discussed in this video |

## Examples and solution approach

### How the while loop works

The `while` loop resembles the `if` statement. After the `while` keyword you write a condition, and below it, indented, the loop body. The difference is that after executing the loop body the program does not move on. It goes back to the condition and checks it again. The loop repeats as long as the condition is true. When the condition becomes `False`, the program continues with the statements written below the loop. If the condition is false on the very first check, the loop does not run even once.

### Example 1. Powers of two

Task from the code: print the powers of two with a natural exponent that are less than the value of the variable `n`, that is 1, 2, 4, 8 and so on. The value of `n` is drawn with `random.randint(1000, 9999)`.

```python
p = 1
while p <= n:
    print(f"Kolejna potęga 2: {p}")
    p *= 2
print("Koniec potęg 2.")
```

The variable `p` starts at 1, which is 2 to the power of zero. In each iteration the loop prints the current power, and the statement `p *= 2`, a shorthand for `p = p * 2`, moves on to the next power. The loop ends when `p` exceeds `n`. The program then prints a message saying the powers are finished.

### Example 2. Sum of consecutive numbers up to 50

Task: keep adding consecutive positive natural numbers until the sum exceeds 50. I show two solutions that produce the same result.

Version 1 places the condition in the loop header. This condition says when the loop should repeat.

```python
suma_calkowita = 0
k = 1
while suma_calkowita + k <= 50:
    suma_calkowita += k
    k += 1
print(f"{k - 1}, {suma_calkowita}")
```

Version 2 is a `while True` loop, whose condition is always true. The condition in the `if` statement works the opposite way to version 1, that is, it says when the loop has to be left. The `break` statement ends the loop immediately and the program jumps to the code below it.

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

In both versions, once the loop ends, the variable `k` holds the number whose addition would exceed the limit. That number has to be rejected, which is why the result is `k - 1`. The sum 1 + 2 + ... + 9 equals 45, and adding 10 would give 55, which is more than 50.

In this task version 1 is the better choice. The `while True` construct is useful when you need to run additional statements before or after checking the condition. It is a matter of how conveniently you can write it in a given situation, and you will come across both approaches in code.

### Example 3. Sum of numbers not divisible by 3

Task: keep adding consecutive positive natural numbers that are not divisible by 3 until the sum exceeds 50. This example introduces the `continue` statement.

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

The `continue` statement skips the rest of the loop body and moves on to the next iteration. The loop does not end, only the current iteration does. When `k` is divisible by 3, the number is not added to the sum and is not stored in `ostatnia_dodana`. Only when adding the next `k` would exceed 50 does the `break` statement end the whole loop. In short: `continue` interrupts an iteration, while `break` interrupts the whole loop.

The variable `k` starts at 0 and is incremented at the very beginning of each iteration. This matters. Without that statement `k` would stay at 0 the whole time, and 0 is divisible by 3. Then `continue` would run in every iteration, `k` would never change, and the loop would spin forever.

The variable `ostatnia_dodana` stores the last number that was added to the sum. Printing `k - 1` as in example 2 is not enough here, because the previous value of `k` may have been skipped by `continue`.

### The for loop and the range function

In typical Matura tasks the `while` loop depends on a specific condition, while the `for` loop is rather used to perform a number of iterations fixed in advance. The `range` function supplies consecutive values, which are assigned to the loop variable in each iteration.

```python
for i in range(5):  # range(n) dostarcza kolejne wartości od 0 do n - 1
    print(i, end=" ")
```

The `end=" "` argument makes `print` output a space after each value instead of a new line.

When you do not need the value of the loop variable and only the number of repetitions matters, you write `_` in place of the variable name. In Python this character signals that you are not interested in the value. The language syntax still requires something to be there.

```python
for _ in range(5):
    print("Wykonuje się pewna operacja")
```

The `range` variants from the file `app-5-petle.py`:

| Label | Call | Values |
| --- | --- | --- |
| `For - 1` | `range(5)` | 0 1 2 3 4 |
| `For - 3` | `range(2, 10)` | 2 3 4 5 6 7 8 9 |
| `For - 4` | `range(2, 20, 3)` | 2 5 8 11 14 17 |
| `For - 5` | `range(20, 1, -2)` | 20 18 16 14 12 10 8 6 4 2 |

The end value is never included. The third argument is the step. It can be negative, and then the values decrease. If you changed the end of the range in `For - 5` from 1 to 2, the last printed value would be 4.

Counting from zero will come in handy with lists and strings, where element positions are also counted from zero. Thanks to this, a `for` loop with `range` will make it easy to go through elements when their position matters.

### Iterating over a list and a string

A `for` loop can also go through elements directly, without `range`. A list is a collection of elements written in square brackets. I will cover lists and strings in detail in later lessons of the course.

```python
liczby = [10, 32, 34, 45]
for liczba in liczby:
    print(liczba)
```

In each iteration the variable `liczba` receives the next element of the list. In the same way you go through a string character by character:

```python
imie = "Krzysztof"
for znak in imie:
    print(znak)
```

### break and continue in a for loop

The `break` and `continue` statements work in a `for` loop exactly the same way as in a `while` loop.

```python
for i in range(20):
    print(f"Przed {i=}")
    if i > 10:
        # break
        continue
    print(f"Po {i=}")
```

In the version with `continue`, for `i` from 0 to 10 you see both messages, "Przed" and "Po". For `i` from 11 to 19 only "Przed" appears, because `continue` skips the rest of the iteration. If you replace `continue` with `break`, which is commented out in the code, the loop ends after printing `Przed i=11`.

### Nested loops

```python
for i in range(1, 5):
    for j in range(1, 5):
        print(f"{i=},{j=}", end="\t")
    print()
```

For each value of `i`, the inner loop runs in full, so `j` takes the values 1 to 4 in turn. Only then does the outer loop move on to its next iteration. The empty `print()` at the level of the outer loop moves the output to a new line. We will use this construct later to go through two-dimensional structures.

## Results

Output of the while loop part for the drawn value `n=1131`, as in the video:

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

Both versions of example 2 give the same result, `9, 45`. In example 3 the last added number is 11 and the sum is 48, that is 1 + 2 + 4 + 5 + 7 + 8 + 10 + 11. The next number not divisible by 3 is 13, and 48 + 13 = 61 would exceed the limit.

Output of the nested loops:

```
For - 9:
i=1,j=1	i=1,j=2	i=1,j=3	i=1,j=4	
i=2,j=1	i=2,j=2	i=2,j=3	i=2,j=4	
i=3,j=1	i=3,j=2	i=3,j=3	i=3,j=4	
i=4,j=1	i=4,j=2	i=4,j=3	i=4,j=4	
```

## Implementation notes

The comment with the task for example 1 talks about powers less than `n`, while the loop uses the condition `p <= n`. When the drawn `n` is itself a power of two (1024, 2048, 4096 or 8192), it gets printed as well. If the task requires a strict inequality, it is enough to change the condition to `p < n`.

The variables `suma_calkowita` and `k` are reused in examples 2 and 3. In such a short file this is a deliberate choice. In a larger program it is easy to accidentally overwrite a value this way that you want to refer to later. In that case it is safer to introduce new names, for example `suma_calkowita2` and `k2`.

A `while True` loop must contain a `break` statement. Without it the program gets stuck in the loop.

If you know there will be code in a given place but you have not written it yet, you can put the `pass` keyword there. The indented block is then not empty and there is no error in the code.

Every `while` loop can be replaced with a `for` loop and vice versa. There is no point in doing it by force, though. You choose the loop that is more convenient to write in the given situation.

Once functions appear later in the course, some of the behaviour we now get with `break` and `continue` will be achieved by splitting the program into functions appropriately. Even so, you need to know both statements.