# Projekt: Turniej Strategii w Iterowanym Dylemacie Więźnia

## Opis projektu
Celem projektu jest zaimplementowanie środowiska symulacyjnego dla teorii gier w języku Python. Program musi umożliwiać rozgrywanie powtarzalnych partii dylematu więźnia pomiędzy różnymi algorytmami w systemie "każdy z każdym", a następnie agregować i sprawdzać wyniki punktowe.

## Wymagania funkcjonalne

### 1. Architektura klas
Dowolna, aby tylko spełaniała paradygamty OOP.

### 2. Implementacja strategii podstawowych
Wymagane jest oprogramowanie minimum czterech unikalnych botów:
*   **Zawsze Współpracujący (Always Cooperate):** W każdej turze niezmiennie wybiera `'C'`.
*   **Zawsze Zdradzający (Always Defect):** W każdej turze niezmiennie wybiera `'D'`.
*   **Oko za oko (Tit for Tat):** W pierwszej turze współpracuje. W każdej kolejnej wykonuje dokładnie taki ruch, jaki jego przeciwnik wykonał w turze poprzedniej.
*   **Pamiętliwy (Grudger):** Współpracuje do momentu, w którym przeciwnik zdradzi po raz pierwszy. Od tamtej pory do końca meczu wybiera wyłącznie `'D'`.

### 3. Logika rozgrywki i punktacja
*   Mecz pomiędzy dwoma graczami składa się ze stałej liczby tur (domyślnie 100 lub 200).
*   Po wykonaniu ruchów przez obu graczy, system przyznaje punkty na podstawie poniższej macierzy wypłat:(Mam nadzieję, że dobrze pamiętam xD)
    *   Obaj współpracują (C, C) -> po 3 punkty.
    *   Obaj zdradzają (D, D) -> po 1 punkcie.
    *   Gracz A współpracuje, Gracz B zdradza (C, D) -> Gracz A: 0 punktów, Gracz B: 5 punktów.
    *   Gracz A zdradza, Gracz B współpracuje (D, C) -> Gracz A: 5 punktów, Gracz B: 0 punktów.

### 4. Silnik turniejowy
*   Program musi przeprowadzić turniej w formule "każdy z każdym", uwzględniając również sytuację, w której kopia danej strategii gra przeciwko sobie.
*   Przed każdym meczem historie graczy muszą zostać zresetowane.
*   Wyniki punktowe ze wszystkich pojedynków muszą być sumowane dla każdego gracza.
*   Po zakończeniu turnieju program ma wyświetlić ranking końcowy posortowany malejąco według liczby zdobytych punktów.

---

## Zadanie Bonusowe (Zaawansowane)

### Symulacja ewolucyjnej dynamiki replikatora z szumem informacyjnym

Rozbuduj projekt o mechanizm ewolucyjny działający w środowisku podatnym na błędy komunikacji.

#### Krok 1: Wprowadzenie szumu (Noise)
Wprowadź do silnika meczowego parametr prawdopodobieństwa błędu (np. `noise_rate = 0.02`). Zanim ruch gracza zostanie przekazany do macierzy wypłat i historii przeciwnika, istnieje 2% szans na to, że zostanie on losowo odwrócony (z 'C' na 'D' lub z 'D' na 'C'). Gracz w swojej własnej historii zapisuje intencję, ale jego przeciwnik widzi i zapisuje efekt błędu.

#### Krok 2: Algorytm genetyczny / Dynamika populacji
Zamiast prostego rankingu punktów, zaimplementuj system pokoleń:
*   Rozpocznij z populacją składającą się ze 100 osobników (np. po 25 każdego typu).
*   W każdej generacji uruchom pełny turniej "każdy z każdym". Sumaryczna liczba punktów zdobyta przez dany typ bota określa jego dostosowanie (fitness).
*   Po zakończeniu generacji następuje faza reprodukcji i selekcji:
    *   Stały procent najgorszych strategii (np. 10-20% populacji z najniższymi wynikami) wymiera i jest usuwany.
    *   Miejsca usuniętych botów zajmują kopie strategii, które osiągnęły najwyższe wyniki w tej generacji.
*   Program powinien symulować np. 50 lub 100 pokoleń i na koniec wyświetlić udział procentowy poszczególnych strategii w końcowej populacji.

## Wnioski
Który algorytm wygrał jak jest szum, a który jak jest on nieobecny? Dlaczego? 