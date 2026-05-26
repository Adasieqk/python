## Zadanie 1: Wyjaśnienie pojęć obiektowych i funkcyjnych

*   **Klasa**: To szablon (przepis) określający właściwości i zachowania. Służy do tworzenia wielu podobnych do siebie elementów bez powtarzania kodu.
*   **Obiekt**: To instancja (konkretny "byt" w pamięci) stworzona na podstawie klasy. Posiada realne wartości przypisane do szablonu.
*   **Konstruktor**: W Pythonie to metoda **`__init__()`**. Działa automatycznie przy tworzeniu obiektu i służy do ustawienia jego początkowych wartości (atrybutów).
*   **Dziedziczenie**: Mechanizm, w którym nowa klasa przejmuje właściwości i metody z innej klasy (bazowej). Służy do unikania duplikacji kodu i budowania hierarchii (np. klasa `Pies` dziedziczy po klasie `Zwierze`).
*   **Funkcja**: Wydzielony blok kodu wykonujący konkretne zadanie. Zwraca wynik lub tylko wykonuje operację. Służy do podziału programu na mniejsze, reużywalne moduły.

## Zadanie 2: Analiza pętli `for`

```python
x = 5
for i in range(1, x):
    if i % 2 == 0:
        print(i)
```

**Wynik:**
```text
2
4
```

**Wyjaśnienie działania:** 
Zmienna `x` wynosi `5`. Funkcja `range(1, 5)` generuje liczby od `1` do `4` (w Pythonie przedział jest otwarty z prawej strony). Instrukcja warunkowa sprawdza resztę z dzielenia (`i % 2 == 0`). Jeśli reszta to `0`, liczba jest parzysta i zostaje wydrukowana.

## Zadanie 3: Błędy w kodzie i poprawa

**Wykryte błędy:**
1. Brak dwukropka `:` po nazwie klasy.
2. Brak parametru `self` w metodzie `__init__`.
3. Brak parametru `self` w metodzie `pokaz()`.
4. Metoda `pokaz()` odwołuje się do zmiennej lokalnej `imie`, a powinna do atrybutu obiektu `self.imie`.

**Poprawiony kod:**
```python
class Uczen:
    def __init__(self, imie):
        self.imie = imie
        
    def pokaz(self):
        print(self.imie)
```

## Zadanie 4: Instrukcje sterujące przepływem

*   **`break`**: Natychmiast **przerywa** działanie całej pętli. Służy np. do zakończenia wyszukiwania, gdy znajdziemy żądany element.
*   **`continue`**: Przerywa tylko **obecną iterację** i od razu przechodzi do następnego obrotu pętli. Służy do pomijania niechcianych wartości.
*   **`pass`**: To tzw. instrukcja pusta (placeholder). Nie robi absolutnie nic. Służy do zachowania poprawnej składni, gdy musimy zdefiniować np. pustą funkcję lub klasę "na później".

## Zadanie 5: Analiza pętli `while`

```python
suma = 0
i = 1
while i <= 5:
    suma += i
    i += 1
print(suma)
```

**Wynik:**
```text
15
```

**Wyjaśnienie działania:** 
Program sumuje kolejne liczby całkowite od `1` do `5`. Pętla wykonuje się 5 razy, w każdym kroku dodając wartość licznika `i` do zmiennej `suma` (`1 + 2 + 3 + 4 + 5`).

## Zadanie 6: Operacje na liście

```python
dane = [5, 2, 8, 2, 9, 5]
```

*   `len(dane)` = **`6`** (zwraca całkowitą liczbę elementów w liście).
*   `dane.count(2)` = **`2`** (zlicza, ile razy liczba 2 występuje w liście).
*   `sorted(dane)` = **`[2, 2, 5, 5, 8, 9]`** (zwraca nową, posortowaną rosnąco listę; oryginalna lista `dane` pozostaje niezmieniona).

## Zadanie 7: Przekształcenie listy na zbiór

```python
dane = [5, 2, 8, 2, 9, 5]
zbior_dane = set(dane)
print(zbior_dane)
```

**Wynik (kolejność może być losowa):**
```text
{8, 9, 2, 5}
```

**Wyjaśnienie:** 
Zbiór (`set`) w Pythonie przechowuje wyłącznie **unikalne wartości**. Rzutowanie listy na zbiór automatycznie i najszybciej usuwa z niej wszystkie duplikaty (w tym wypadku nadmiarowe liczby `2` i `5`).

## Zadanie 8: Kiedy używać jakiej kolekcji?

*   **Lista (`list`)**: Kiedy potrzebujesz zmieniać rozmiar kolekcji i modyfikować elementy, a kolejność ma znaczenie.
    *   *Przykład*: Przechowywanie ocen ucznia z danego przedmiotu: `[4, 5, 3, 5]`.
*   **Krotka (`tuple`)**: Kiedy dane są stałe i wiesz, że nigdy nie będą modyfikowane. Jest szybsza od listy i zużywa mniej pamięci.
    *   *Przykład*: Współrzędne geograficzne miasta: `(50.049683, 19.944544)`.
*   **Zbiór (`set`)**: Kiedy potrzebujesz trzymać tylko unikalne wartości i bardzo szybko sprawdzać, czy dany element istnieje (dużo szybciej niż w liście).
    *   *Przykład*: Lista zablokowanych adresów IP na serwerze: `{"192.168.1.1", "10.0.0.5"}`.
*   **Słownik (`dict`)**: Kiedy potrzebujesz par "klucz: wartość", aby szybko wyciągać dane po jednoznacznej nazwie (kluczu) zamiast po indeksie liczbowym.
    *   *Przykład*: Informacje o produkcie w sklepie: `{"id": 105, "nazwa": "Mysz", "cena": 99.99}`.

## Zadanie 9: Projekt klasy `KontoBankowe`

```python
class KontoBankowe:
    def __init__(self, wlasciciel, saldo=0.0):
        self.wlasciciel = wlasciciel
        self.saldo = saldo
        
    def wplata(self, kwota):
        if kwota > 0:
            self.saldo += kwota
            print(f"Wpłacono {kwota} zł.")
            
    def wyplata(self, kwota):
        if kwota <= self.saldo:
            self.saldo -= kwota
            print(f"Wypłacono {kwota} zł.")
        else:
            print("Brak wystarczających środków na koncie.")
            
    def pokaz_stan(self):
        print(f"Konto: {self.wlasciciel} | Saldo: {self.saldo:.2f} zł")

# Przykład użycia
konto = KontoBankowe("Jan Kowalski", 100.0)
konto.wplata(50)
konto.wyplata(30)
konto.pokaz_stan()
```

## Zadanie 10: 3 operacje na zbiorach

```python
zbiór_a = {1, 2, 3}
zbiór_b = {3, 4, 5}

# 1. Suma (union): łączy zbiory, ignorując duplikaty
suma = zbiór_a | zbiór_b  
# Wynik: {1, 2, 3, 4, 5}

# 2. Przecięcie / Część wspólna (intersection): zostawia tylko to, co jest w obu
przeciecie = zbiór_a & zbiór_b  
# Wynik: {3}

# 3. Różnica (difference): odejmuje elementy drugiego zbioru od pierwszego
roznica = zbiór_a - zbiór_b  
# Wynik: {1, 2}
```
