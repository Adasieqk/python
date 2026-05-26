## Wprowadzenie: Typy danych i operatory

W Pythonie nie deklarujesz typu zmiennej jawnie (typowanie dynamiczne). Typ jest przypisywany na podstawie wartości.

*   `int` (całkowite): Liczby bez części ułamkowej (np. `5`, `-10`).
*   `float` (zmiennoprzecinkowe): Liczby z częścią ułamkową (np. `3.14`). Zawsze używaj kropki, nie przecinka.
*   `complex` (zespolone): Liczby z częścią rzeczywistą i urojoną (np. `2+3j`).
*   `bool` (logiczne): Prawda (`True`) lub fałsz (`False`). W Pythonie `True` to pod spodem `1`, a `False` to `0`.

Do sprawdzania typu służy funkcja **`type()`**.

```python
x_int = 10
x_float = 3.5
x_bool = True
x_complex = 1 + 2j

print(type(x_float))  # Zwróci: <class 'float'>
```

**Operatory matematyczne:**
*   Dodawanie: `+`, Odejmowanie: `-`, Mnożenie: `*`
*   Dzielenie standardowe: `/` (zawsze zwraca `float`)
*   Dzielenie całkowite: `//` (odcina część ułamkową)
*   Reszta z dzielenia (modulo): `%` (kluczowe do sprawdzania parzystości)
*   Potęgowanie: `**`

```python
wynik = 10 // 3  # Zwróci 3
reszta = 10 % 3  # Zwróci 1
potega = 2 ** 3  # Zwróci 8
```

## Pętle

Pętle służą do wielokrotnego wykonywania bloku kodu.

### Pętla `while`
Wykonuje kod, dopóki podany warunek jest prawdziwy (`True`). Wymaga ręcznej kontroli licznika, inaczej powstanie nieskończona pętla.

```python
licznik = 0
while licznik < 3:
    print(licznik)
    licznik += 1  # Zwiększamy licznik, zapobiega nieskończonej pętli
```

### Pętla `for`
Służy do iteracji (przechodzenia) po elementach kolekcji (np. liście, łańcuchu znaków) lub w wygenerowanym zakresie (funkcja `range()`).

```python
imiona = ["Anna", "Jan", "Piotr"]

# Iterowanie po elementach listy
for imie in imiona:
    print(imie)

# Iterowanie z użyciem range (od 0 do 4)
for i in range(5):
    print(i)
```

## Kolekcje

Kolekcje to struktury pozwalające przechowywać wiele wartości w jednej zmiennej. 

### Listy i Krotki
*   **Lista (`list`)**: Uporządkowana, modyfikowalna (mutowalna) kolekcja. Zapisywana w nawiasach kwadratowych `[]`.
*   **Krotka (`tuple`)**: Uporządkowana, **niemodyfikowalna** kolekcja. Zapisywana w nawiasach okrągłych `()`. Szybsza i bezpieczniejsza niż lista, jeśli dane nie mają się zmieniać.

```python
jakas_lista = ["string", 4, True] # Lista
jakas_krotka = (0, 3, 4, 4, 4)    # Krotka

print(jakas_lista)
print(jakas_krotka)

# Modyfikacja listy zadziała
jakas_lista[0] = 9

# jakas_krotka[0] = 12 
# BŁĄD: Krotki są niemodyfikowalne. Nie można zmienić ich elementu.

# Rzutowanie (konwersja) krotki na listę (teraz można modyfikować)
jakas_lista = list(jakas_krotka)
jakas_lista[0] = False

# Konwersja z powrotem na krotkę
jakas_krotka = tuple(jakas_lista)
print(jakas_krotka)

# len() - zwraca długość kolekcji
print(len(jakas_lista), len(jakas_krotka))
```

**Operacje na liście:**

```python
# .append() - dodaje element na sam koniec listy
jakas_lista.append(9)

# .insert(indeks, wartość) - wstawia element na konkretne miejsce, przesuwając resztę
jakas_lista.insert(1, -5)

# .sort() - sortuje listę w miejscu. reverse=True sortuje malejąco.
# UWAGA: Sortowanie zadziała, bo w Pythonie False to 0, więc jest traktowane jako liczba.
jakas_lista.sort(reverse=True)

# .count(wartość) - zlicza, ile razy wartość występuje w kolekcji
print(jakas_lista.count(3))

# .pop() - usuwa i zwraca OSTATNI element z listy (można podać indeks, np. pop(0))
ostatni = jakas_lista.pop()

# .clear() - czyści listę ze wszystkich elementów
jakas_lista.clear()
```

### Zbiory (Sets) i specyfika Bool

**Zbiór (`set`)** to nieuporządkowana kolekcja unikalnych elementów. Zapisywana w nawiasach klamrowych `{}`. Brak indeksów (nie użyjesz `zbiór[0]`). Służy do szybkiego usuwania duplikatów i operacji matematycznych.

```python
lista_z_duplikatami = [4, 4, 4, 7, 7]
# Szybkie usunięcie duplikatów przez rzutowanie na zbiór
lista_bez_duplikatow = list(set(lista_z_duplikatami)) 
print(lista_bez_duplikatow) # Zwróci [4, 7]

jakis_zbior = {0, False, 1, True, 4, 5, 5, 5, 9}
print(jakis_zbior)
```

**Ważne (Mechanika zbioru `{0, False, 1, True}`):**
Jeśli wyprintujesz powyższy zbiór, otrzymasz np. `{0, 1, 4, 5, 9}`. Dlaczego `False` i `True` zniknęły?
W Pythonie `True` jest równe `1`, a `False` jest równe `0`. Ponieważ zbiory wymuszają **unikalność**, Python traktuje `0` i `False` jako ten sam element, tak samo `1` i `True`. W zbiorze zostaje ten element, który został zadeklarowany jako pierwszy.

**Operacje na zbiorach:**

```python
# .add() - dodaje pojedynczy element
jakis_zbior.add(8)

# .pop() w zbiorach - usuwa i zwraca LOSOWY element (zbiory nie mają kolejności!)
jakis_zbior.pop()

jakis_zbior.clear() # Czyści zbiór

zbior1 = {2, 3, 4}
zbior2 = {4, 5, 6}

# Suma zbiorów (union / |). Łączy elementy, usuwa duplikaty
zbior3 = zbior1.union(zbior2) # lub: zbior3 = zbior1 | zbior2

# Część wspólna (intersection / &)
zbior3 = zbior1.intersection(zbior2) # lub: zbior3 = zbior1 & zbior2

# Różnica (difference / -). Elementy w zbiorze 1, których nie ma w zbiorze 2
zbior3 = zbior1.difference(zbior2) # lub: zbior3 = zbior1 - zbior2

# Różnica symetryczna (symmetric_difference). Elementy, które nie są częścią wspólną
zbior3 = zbior1.symmetric_difference(zbior2)
```

### Słowniki (`dict`)
Kolekcja par **klucz: wartość**. Szybkie wyszukiwanie po unikalnym kluczu.

```python
uczen = {
    "imie": "Jan",
    "klasa": "3A",
    "wiek": 18
}
print(uczen["imie"])  # Dostęp do wartości po kluczu
```

## Klasy i Obiekty (Programowanie Obiektowe)

**Klasa** to szablon. **Obiekt** to instancja zbudowana na podstawie szablonu.
Metoda **`__init__(self)`** to konstruktor wywoływany automatycznie przy tworzeniu obiektu. `self` to odniesienie do konkretnego (obecnego) obiektu.

```python
class Samochod:
    # Konstruktor parametryczny (przyjmuje dane przy tworzeniu)
    def __init__(self, marka, model):
        self.marka = marka   # Przypisanie argumentu do atrybutu obiektu
        self.model = model
    
    # Metoda kopiująca atrybut z innego, przekazanego obiektu
    def skopiuj_marke(self, inny_obiekt):
        self.marka = inny_obiekt.marka

# Tworzenie obiektów
auto1 = Samochod("Ford", "Mustang")
auto2 = Samochod("Fiat", "Punto")

# Użycie metody kopiującej
auto2.skopiuj_marke(auto1)
print(auto2.marka) # Wypisze: Ford
```

## Dobre praktyki: Nazewnictwo i Importy

**Nazewnictwo:**
*   Używaj opisowych nazw. Zmienna `count` (licznik) natychmiast mówi, co robi, w przeciwieństwie do `a`, `x`, `temp`.
*   **Dlaczego zmienna `my.list` wyrzuci błąd?** W Pythonie znak kropki `.` jest operatorem dostępu do atrybutów lub metod obiektu. Python zinterpretuje `my.list` jako "weź obiekt `my` i odwołaj się do jego właściwości `list`". Do oddzielania słów w nazwach używaj podkreślników (tzw. `snake_case`), np. `my_list`.

**Importowanie modułów:**
Aby zachować czystość kodu i nie pisać długich nazw, używamy aliasów `as`.

```python
import math as m

# Teraz zamiast math.sqrt() piszemy m.sqrt()
pierwiastek = m.sqrt(16)
```

## Algorytmy (INF.03)

### Sprawdzanie liczby pierwszej
Liczba pierwsza dzieli się tylko przez 1 i samą siebie. Zaczynamy sprawdzać dzielniki od 2.

```python
def is_prime(n):
    if n < 2:
        return False
    # Sprawdzamy dzielniki od 2 do pierwiastka z n (optymalizacja)
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False # Znaleziono dzielnik, nie jest pierwsza
    return True
```

### Wyszukiwanie liczb pierwszych w zakresie od 1 do n
```python
def primes_in_range(n):
    primes = []
    for i in range(1, n + 1):
        if is_prime(i):
            primes.append(i)
    return primes
```

### Średnia arytmetyczna i Mediana
```python
def wylicz_srednia(lista):
    if not lista: return 0
    return sum(lista) / len(lista)

def wylicz_mediane(lista):
    if not lista: return 0
    lista.sort() # Mediana wymaga posortowanego zbioru
    n = len(lista)
    srodek = n // 2
    
    # Jeśli parzysta liczba elementów, średnia z dwóch środkowych
    if n % 2 == 0:
        return (lista[srodek - 1] + lista[srodek]) / 2.0
    # Jeśli nieparzysta, po prostu środkowy element
    else:
        return lista[srodek]
```

## Operacje na Plikach

Pliki należy otwierać i zamykać. Tryby: `"r"` (odczyt), `"w"` (zapis, nadpisuje plik), `"t"` (tekstowy - domyślny).

**Sposób 1: Ręczne zarządzanie (podatne na błędy, jeśli program "wywali się" przed `.close()`)**
```python
f = open("plik.txt", "rt") # rt = read text
tresc = f.read()
f.close() # ZAWSZE musisz zamknąć
```

**Sposób 2: Menedżer kontekstu `with` (Zalecany)**
Automatycznie zamyka plik, nawet jak wystąpi błąd.

```python
# wt = write text. Jeśli plik nie istnieje, zostanie utworzony. Jeśli istnieje, zostanie nadpisany.
with open("plik.txt", "wt") as f:
    f.write("Przykładowy tekst")
# Tu plik jest już automatycznie zamknięty
```

## Łańcuchy znaków (Stringi)

Stringi to w Pythonie tablice znaków. Możemy wycinać ich fragmenty za pomocą **Slicingu** w formacie `[start:stop]`.

```python
tekst = "Programowanie"

# Wycinanie (Slicing)
print(tekst[5:])  # Od 5 indeksu do końca: "mowanie"
print(tekst[:5])  # Od początku do 4 indeksu włącznie: "Progr"

# Metody na stringach
t = "  hello WORLD 123  "

print(t.capitalize()) # "  hello world 123  " (Tylko pierwsza litera zdania wielka)
print(t.title())      # "  Hello World 123  " (Pierwsza litera każdego słowa wielka)
print(t.upper())      # "  HELLO WORLD 123  " (Wszystko wielkimi)
print(t.lower())      # "  hello world 123  " (Wszystko małymi)
print(t.strip())      # "hello WORLD 123"    (Usuwa białe znaki - spacje z początku i końca)
print(t.replace("WORLD", "Python")) # Podmienia dany fragment tekstu

# Metody sprawdzające (zwracają True/False)
print("12345".isnumeric()) # True (Czy składa się tylko z cyfr)
print("Abcd".isalpha())    # True (Czy składa się tylko z liter)
print("Abc1".isalnum())    # True (Czy składa się tylko z liter i/lub cyfr)

# Inne
print(tekst.count("o"))    # Zlicza wystąpienia litery "o" w "Programowanie"
print("A,B,C".split(","))  # Dzieli tekst według separatora i zwraca listę: ['A', 'B', 'C']
```

## Formatowanie: f-stringi

Począwszy od Pythona 3.6, używamy f-stringów (przedrostek `f` przed stringiem). Pozwalają na interpolację, czyli wstrzykiwanie zmiennych oraz wyrażeń matematycznych bezpośrednio w tekst przy użyciu klamer `{}`.

```python
temperatura = 25.456
imie = "Kuba"

# Podstawowe wstawianie i operacje matematyczne wewnątrz klamer
print(f"Cześć {imie}, 5 * 2 = {5 * 2}")

# Formatowanie float: :.2f oznacza "zostaw 2 miejsca po przecinku"
print(f"Temperatura wynosi: {temperatura:.2f} stopni.") 
# Wynik: Temperatura wynosi: 25.46 stopni. (Zwróć uwagę na poprawne zaokrąglenie)

# Symulacja warunkowa (Operator trójargumentowy / Ternary) wewnątrz f-stringa
print(f"Dzisiaj jest {'ciepło' if temperatura > 20 else 'zimno'}.")
```
