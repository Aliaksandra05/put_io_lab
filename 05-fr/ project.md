# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny.

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2), [System](#ac3).

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego. |

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu.
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu.

**Scenariusze alternatywne:**

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.



## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję.
* [UC2](#uc1): Przekazanie produktu Kupującemu.

[Kupujący](#ac2)
* [UC3](#uc2): Oferowanie nowej kwoty.
* [UC4](#uc2): Przekazanie naleznosci [Sprzedajacemu](#ac1).

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:**

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Przekazanie produktu Kupującemu

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2).

**Scenariusz główny:**
1. [Sprzedający](#ac1) potwierdza sprzedaż produktu.
2. System informuje o zakończeniu aukcji i przekazuje dane odbiorcy.
3. [Sprzedający](#ac1) przekazuje produkt [Kupującemu](#ac2).


**Scenariusze alternatywne:**

3.A. Produkt nie został dostarczony.
* 3.A.1. System informuje [Kupującego](#ac2) o opóźnieniu.
* 3.A.2. Transakcja pozostaje w statusie „oczekuje na dostarczenie”.

<a id="uc3"></a>
### UC3: Oferowanie nowej kwoty

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2).

**Scenariusz główny:**
1. [Kupujący](#ac2) wybiera aktywną aukcję.
2. [Kupujący](#ac2) składa ofertę z nową kwotą.
3. System zapisuje ofertę i aktualizuje najwyższą kwotę.


**Scenariusze alternatywne:**

2.A. Kwota jest niższa niż aktualna oferta.
* 2.A.1. Kystem odrzuca ofertę.
* 2.A.2. [Kupujący](#ac2) może wprowadzić nową kwotę.

<a id="uc4"></a>
### UC4: Przekazanie naleznosci [Sprzedajacemu](#ac1)

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2).

**Scenariusz główny:**
1. [Kupujący](#ac2) wybiera metodę płatności.
2. System przetwarza transakcję.
3. System potwierdza przekazanie należności [Sprzedającemu](#ac1).


**Scenariusze alternatywne:**

2.A. Płatność nie powiodła się.
* 2.A.1. System informuje o błędzie płatności.
* 2.A.2. [Kupujący](#ac2) może ponowić próbę.

---

## Obiewkty biznesowe (inaczje obiekty dziedzinowe lub informatycjne)


### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupy produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę.

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt | Oferta | Transakcja | Platnosc | Uzytkownik |
| ------------------------------------------------- | ------ | ------- | ------ | ---------- | -------- | ---------- |
| UC1: Wystawienia produktu na aukcję               |   C/R  |   C/R   |    L   |            |          |     R      |
| UC1: Przekazanie produktu Kupującemu              |    U   |    R    |    R   |     R      |     U    |     R      |
| UC2: Oferowanie nowej kwoty                       |    R   |   R/L   |   C/R  |            |          |     R      |
| UC2: Przekazanie naleznosci [Sprzedajacemu](#ac1) |    R   |    R    |    R   |    C/R     |    C/U   |     R      |

## Krok 4 – Brakujące przypadki użycia

1. Rejestracja i logowanie użytkownika.  
2. Edycja albo usunięcie aukcji.  
3. Anulowanie oferty przez kupującego.  
4. Zakończenie aukcji po czasie.  
5. Powiadomienia o przebiciu oferty lub płatności.  
