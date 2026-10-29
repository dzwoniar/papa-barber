# Papa Barber Shop — prototyp strony salonu

Jednostronicowa witryna demonstracyjna salonu barberskiego w Kruszwicy. Pokazuje ofertę usług, cennik, opinie, lokalizację i zaprojektowaną sekcję rezerwacji.

**Status:** statyczny prototyp. W miejscu kalendarza widoczny jest placeholder; integracja rezerwacji Cal.com jest opisana w komentarzu kodu, ale nie została uruchomiona.

## Co jest zaimplementowane

- Responsywny układ z cennikiem usług, opiniami, FAQ i sekcją dojazdu.
- Osadzona mapa Google oraz odnośniki `tel:` do kontaktu telefonicznego.
- Nawigacja między sekcjami z uwzględnieniem wysokości nagłówka.
- Nagłówek ukrywany podczas przewijania w dół i pokazywany przy przewijaniu w górę.
- FAQ z pojedynczą otwartą odpowiedzią i animacje pojawiania się sekcji.
- Metadane Open Graph i dane strukturalne JSON-LD typu `BarberShop`.

## Stos i architektura

HTML, CSS i JavaScript bez frameworka, pakietów npm oraz procesu budowania. Wszystkie treści, style i skrypty są w [index.html](index.html).

JavaScript obsługuje lokalne interakcje DOM przez `toggleFaq()`, `IntersectionObserver` i zdarzenia przewijania. Nie ma backendu, bazy danych ani konfiguracji zmiennych środowiskowych.

Aktywne zależności zewnętrzne to fonty Playfair Display i DM Sans z Google Fonts oraz iframe Google Maps. Przykładowy skrypt i iframe Cal.com znajdują się wyłącznie w komentarzu HTML.

## Uruchomienie lokalne

Wymagania: Git, Python 3 i współczesna przeglądarka.

```sh
git clone https://github.com/dzwoniar/papa-barber.git
cd papa-barber
python -m http.server 8000 --bind 127.0.0.1
```

Otwórz [http://127.0.0.1:8000](http://127.0.0.1:8000). Serwer zatrzymasz przez `Ctrl+C`. Mapa i fonty wymagają dostępu do usług zewnętrznych.

## Struktura i miejsca zmian

```text
.
├── index.html   # strona, JSON-LD, style i interakcje
└── README.md    # dokumentacja projektu
```

- Oferta i ceny: sekcja `#uslugi`.
- Miejsce pod kalendarz: sekcja `#rezerwacja`, element `.cal-placeholder` i poprzedzający go komentarz wdrożeniowy.
- Mapa: sekcja `#dojazd`.
- Dane wyszukiwarek i podglądów linków: `<head>` oraz blok `application/ld+json`.

## Granice demo

Strona nie sprawdza dostępności terminów, nie tworzy rezerwacji i nie wysyła przypomnień SMS lub e-mail. Teksty opisujące te funkcje prezentują docelowy przebieg usługi. Połączenia telefoniczne są przekazywane do urządzenia przez linki `tel:`.

Treści oferty, godziny pracy i opinie są wpisane na stałe. Dane strukturalne mają puste pola `image` i `url`; przed wdrożeniem wymagają uzupełnienia oraz potwierdzenia pozostałych danych biznesowych.

## Sprawdzenie po zmianach

Nie ma skonfigurowanych testów automatycznych. Sprawdź lokalnie układ mobilny, FAQ, przewijanie do sekcji i zachowanie nagłówka. Mapę oraz metadane kontroluj oddzielnie od przyszłej integracji rezerwacji. Podgląd strony nie wymaga wykonywania połączenia ani rezerwacji.
