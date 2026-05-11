# Smart Greenhouse CPS Optimizer 

## Opis projektu
Projekt przedstawia koncepcję i implementację **Systemu Cyber-Fizycznego (CPS)** przeznaczonego do inteligentnego zarządzania doświetlaniem roślin w szklarniach. System łączy świat cyfrowy (prognozy pogody, giełdowe ceny energii, modele biologiczne) z fizycznym (czujniki nasłonecznienia, lampy LED, zdrowie roślin).

Głównym zadaniem modelu jest dostarczenie roślinom optymalnej dawki światła (**DLI - Daily Light Integral**) przy jednoczesnej minimalizacji kosztów operacyjnych i śladu węglowego.

## Kluczowe Funkcjonalności
* **Smart Optimizer**: Algorytm decyzyjny, który analizuje zapotrzebowanie rośliny i wybiera najtańsze okna czasowe na doświetlanie.
* **Zarządzanie Cyklem Życia**: Rozpoznawanie fazy wzrostu rośliny (`Growth_Stage`) i automatyczne dopasowanie celów świetlnych.
* **Odporność na Błędy (Resilience)**: Mechanizmy uzupełniania brakujących danych z czujników (imputacja danych), zapobiegające awariom systemu sterowania.
* **Weryfikacja Krzyżowa**: Koncepcja wykorzystania obrazu z kamer (wskaźnik **NDVI**) do weryfikacji poprawności odczytów z czujników PPFD.

## Struktura Danych
System operuje na zbiorze danych `plants_dataset.csv`, który zawiera:
* **Parametry środowiskowe**: Nasłonecznienie aktualne i prognozowane.
* **Parametry rynkowe**: Cena energii [PLN/kWh], intensywność emisji CO2.
* **Parametry biologiczne**: Gatunek rośliny, faza wzrostu, wskaźnik NDVI, cel DLI oraz próg stresu świetlnego.

## Technologie
* **Python 3.x**
* **Pandas**: Przetwarzanie i czyszczenie danych szeregów czasowych.
* **Matplotlib**: Wizualizacja interakcji między światem cyfrowym a fizycznym.
* **Jupyter Notebook**: Środowisko eksperymentalne i dokumentacja procesu.

## Setup środowiska
Zainstaluj `uv` manager dla python'a na swojej maszynie. Np. za pomocą `brew` na MAC OS:

```bash
brew install uv
```
Następnie:
```bash
uv sync
```

Wybierz kernel w notebook'u i jesteś gotowy do pracy.

## Sposób użycia
1. Załaduj plik `plants_dataset.csv`.
2. Uruchom komórki Notebooka w celu przetworzenia i posortowania danych.
3. Wywołaj funkcję `smart_optimizer`, aby wygenerować harmonogram doświetlania.
4. Przeanalizuj wykres końcowy, aby zweryfikować efektywność modelu.

## Interpretacja Wyników
System uznaje się za zoptymalizowany, gdy:
* Krzywa zakumulowanego światła osiąga cel (Target DLI) pod koniec doby.
* Praca lamp LED jest skorelowana z najniższymi cenami energii.
* Suma światła słonecznego i sztucznego nie przekracza dopuszczalnych norm dla danego gatunku.