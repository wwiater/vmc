# Proponowane zadania po przeglądzie kodu

## 1) Literówka do poprawy
**Obszar:** konfiguracja slajdów w `_config.yml`.

**Problem:** W komentarzu jest literówka: `dont't show slide numbers`.

**Zadanie:**
- Zmień komentarz na poprawną formę `don't show slide numbers`.

**Uzasadnienie:** Drobna poprawka językowa podnosi czytelność i profesjonalizm konfiguracji.

---

## 2) Błąd do usunięcia
**Obszar:** skrypt bootstrapujący środowisko `script/setup`.

**Problem:** Warunek instalacji Ruby jest oparty o:
- istnienie `.ruby-version`,
- oraz brak wyniku `rbenv version-name`.

To może pominąć przypadek, gdy `rbenv` w ogóle nie jest zainstalowany, a skrypt mimo to zakłada jego obecność i później odwołuje się do `rbenv`.

**Zadanie:**
- Dodać jawne sprawdzenie dostępności `rbenv` (`command -v rbenv`).
- Jeśli `rbenv` jest wymagany, ale nieobecny, zakończyć skrypt czytelnym komunikatem i kodem błędu.
- Alternatywnie: obsłużyć fallback bez `rbenv` (np. instalacja bundlera bez rehash).

**Uzasadnienie:** To usuwa potencjalny błąd inicjalizacji środowiska na maszynach bez `rbenv`.

---

## 3) Korekta komentarza / rozbieżności dokumentacyjnej
**Obszar:** README vs rzeczywista zawartość repozytorium.

**Problem:** `README.md` opisuje repo jako materiał do GitHub Learning Lab i aktywności kursowej, ale obecna struktura to szablon/slideshow Jekyll z Reveal.js. Może to wprowadzać użytkownika w błąd.

**Zadanie:**
- Zaktualizować sekcję wstępną README tak, aby opisywała aktualny cel projektu.
- Dodać krótkie instrukcje uruchomienia (`script/setup`, `script/server`) oraz build (`script/cibuild`).

**Uzasadnienie:** Redukuje dług techniczny w dokumentacji i poprawia onboarding.

---

## 4) Ulepszenie testu
**Obszar:** walidacja HTML w `script/cibuild`.

**Problem:** `htmlproofer` jest uruchamiany tylko na `_site/index.html`, co nie obejmuje ewentualnych dodatkowych stron generowanych przez Jekyll.

**Zadanie:**
- Rozszerzyć check na cały katalog `_site` (np. `htmlproofer _site`).
- Utrzymać/uzupełnić flagi ignorujące znane false-positive.

**Uzasadnienie:** Zwiększa pokrycie testowe i szansę wychwycenia regresji w linkach/HTML poza stroną główną.
