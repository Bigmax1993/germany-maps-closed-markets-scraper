# Germany temporarily closed markets scraper

Skrypt w Pythonie wykorzystujący Selenium do skrapowania Google Maps dla wybranych marek spożywczych w Niemczech.

Do CSV zapisywane są **wyłącznie sklepy oznaczone jako tymczasowo zamknięte**:

- polski: `tymczasowo zamknięte / tymczasowo zamkniete`
- niemiecki: `vorübergehend geschlossen / voruebergehend geschlossen`
- angielski: `temporarily closed`

## Najważniejsze cechy

- Domyślnie działa w tle (`headless`).
- Gdy pojawi się CAPTCHA, automatycznie otwiera widoczną przeglądarkę do ręcznego potwierdzenia.
- Po rozwiązaniu CAPTCHA wraca do działania w tle.
- Obsługuje wznowienie pracy na podstawie istniejącego CSV i cache JSON.
- Może działać zarówno z terminala, jak i z Jupyter Lab.

## Instalacja

1. Zainstaluj zależności:

   ```bash
   pip install -r requirements.txt
   ```

## Uruchomienie z terminala

```bash
python scraper.py
```

Skrypt uruchamia `main()`, która wywołuje `run_scraper(headless_default=True, jupyter_mode=False)`.

## Uruchomienie z Jupyter Lab

W notebooku użyj:

```python
from scraper import run_scraper

run_scraper(headless_default=True, jupyter_mode=True)
```

W trybie Jupyter, przy CAPTCHA:

1. Otworzy się widoczna przeglądarka.
2. Rozwiąż CAPTCHA ręcznie.
3. Wróć do komórki i potwierdź Enterem.
4. Skrypt kontynuuje działanie w tle.

## Wyniki

- CSV: `C:\Users\kanbu\Documents\Budowy\germany_markets_selenium_closed_only.csv`
- cache JSON: `C:\Users\kanbu\Documents\Budowy\germany_markets_cache.json`
- logi: `C:\Users\kanbu\Documents\Budowy\germany_markets_scraper.log`

## Testy

Uruchom testy:

```bash
python -m pytest tests/test_status_parsing.py tests/test_captcha_and_driver.py
```

Skrypt można wznawiać – wykorzystuje istniejący CSV i cache JSON, dzięki czemu nie pobiera ponownie już znanych miejsc.
