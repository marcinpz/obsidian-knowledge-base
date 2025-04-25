# GitHub Actions

## Czym są GitHub Actions?
GitHub Actions to potężne narzędzie do automatyzacji procesów w ramach repozytoriów GitHub. Umożliwiają one tworzenie niestandardowych przepływów pracy (workflows), które mogą być uruchamiane w odpowiedzi na różne zdarzenia w repozytorium, takie jak push, pull request czy wydanie nowej wersji.

### Kluczowe cechy
- **Automatyzacja CI/CD**: Umożliwiają ciągłą integrację i deployment.
- **Elastyczność**: Możesz pisać własne skrypty lub korzystać z gotowych akcji z GitHub Marketplace.
- **Hostowane środowiska**: Działa na maszynach wirtualnych GitHuba (Linux, Windows, macOS) lub własnych runnerach.

## Jak to działa?
GitHub Actions opiera się na plikach konfiguracyjnych w formacie YAML, umieszczonych w katalogu `.github/workflows/` w repozytorium. Każdy plik definiuje przepływ pracy.

### Podstawowe elementy przepływu pracy
1. **Nazwa**: Określa nazwę przepływu pracy (`name`).
2. **Zdarzenia (on)**: Definiuje, co uruchamia przepływ (np. `push`, `pull_request`).
3. **Zadania (jobs)**: Kolekcja kroków do wykonania.
4. **Kroki (steps)**: Poszczególne akcje, np. checkout kodu, instalacja zależności, uruchomienie testów.

### Przykład prostego przepływu pracy
```yaml
name: CI Pipeline
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
      - run: npm install
      - run: npm test
```

## Popularne zastosowania
- **Testowanie**: Automatyczne uruchamianie testów jednostkowych i integracyjnych.
- **Wdrożenia**: Publikowanie aplikacji na serwery lub platformy (np. AWS, Heroku).
- **Linting**: Sprawdzanie kodu pod kątem stylu i błędów.
- **Powiadomienia**: Wysyłanie alertów na Slacka, e-mail itp.

## Zalety
- Integracja z GitHubem – wszystko w jednym miejscu.
- Duża społeczność i ekosystem akcji w Marketplace.
- Darmowe dla publicznych repozytoriów i limitowane minuty dla prywatnych.

## Wady
- Limit minut dla darmowych planów w prywatnych repozytoriach.
- Krzywa uczenia się dla bardziej złożonych konfiguracji.

## Linki i zasoby
- [Dokumentacja oficjalna](https://docs.github.com/en/actions)
- [GitHub Marketplace](https://github.com/marketplace?type=actions)

---
*Ostatnia aktualizacja: 2 kwietnia 2025*