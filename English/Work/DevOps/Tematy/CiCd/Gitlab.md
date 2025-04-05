# GitLab CI/CD

## 1. Wprowadzenie
- **Co to jest?** GitLab CI/CD to wbudowane narzędzie w GitLabie do automatyzacji procesów [[Continuous Integration (CI)]] i [[Continuous Deployment (CD).]]
- **Dlaczego warto?** 
  - Integracja z repozytorium GitLab.
  - Łatwa konfiguracja za pomocą pliku `.gitlab-ci.yml`.
  - Wsparcie dla pipeline’ów, testów, deploymentu i monitorowania.

## 2. Kluczowe pojęcia
- **[[Pipeline]]:** Zestaw zadań (jobs) uruchamianych w odpowiedzi na zmiany w kodzie.
- **[[Job]]:** Pojedyncze zadanie w pipeline, np. testowanie, budowanie, deployment.
- **[[Stage]]:** Grupa jobs uruchamianych równolegle (np. `build`, `test`, `deploy`).
- **[[Runner]]:** Agent wykonujący jobs (może być lokalny, w chmurze lub na własnym serwerze).
- **[[Artifacts]]:** Pliki generowane przez jobs (np. skompilowana aplikacja).

## 3. Konfiguracja podstawowa
- **Plik konfiguracyjny:** `.gitlab-ci.yml` w głównym katalogu repozytorium.
- **Struktura:**
  - Definiujesz `stages`, `jobs` i ich zależności.
  - Używasz zmiennych środowiskowych dla bezpieczeństwa (np. klucze API).

### Przykład prostego pipeline
```yaml
stages:
  - build
  - test
  - deploy

build_job:
  stage: build
  script:
    - echo "Budowanie aplikacji..."
    - npm install
    - npm run build
  artifacts:
    paths:
      - dist/

test_job:
  stage: test
  script:
    - echo "Uruchamianie testów..."
    - npm test

deploy_job:
  stage: deploy
  script:
    - echo "Wdrożenie na serwer..."
  only:
    - main
```
- **Wyjaśnienie:**
    - build_job: Buduje aplikację i zapisuje wynik w dist/.
    - test_job: Uruchamia testy.
    - deploy_job: Wdraża tylko na branchu main.

## 4. Zaawansowane funkcje

- **Variables:** Definiuj zmienne w .gitlab-ci.yml lub w ustawieniach GitLab (Settings > CI/CD > Variables).
- Przykład: API_KEY: $CI_API_KEY.
- **Cache:** Przyspiesz jobs, przechowując zależności (np. node_modules).
```yaml
    cache: 
	     paths: 
		     - node_modules/
```

- **Environments:** Śledź wdrożenia w różnych środowiskach (np. staging, production).
- **Schedules:** Automatyzuj pipeline’y (np. codzienne budowanie).

## 5. Praktyczne wskazówki

- **Debugowanie:**
    - Sprawdzaj logi w GitLab UI.
    - Dodaj echo w skryptach, by śledzić wykonanie.
- **Optymalizacja:**
    - Używaj równoległych jobs (parallel).
    - Skracaj czas pipeline’a dzięki cache.
- **Bezpieczeństwo:**
    - Przechowuj sekrety w zmiennych chronionych.
    - Ogranicz dostęp do runnerów.

## 6. Praktyka

- **Zadanie:**
    - Stwórz repozytorium w GitLabie.
    - Dodaj prostą aplikację (np. w Node.js).
    - Skonfiguruj pipeline z etapami build, test, deploy.
- **Cel:** Zrozum, jak jobs współdziałają i jak zarządzać artefaktami.

## 7. Zasoby

- **Dokumentacja:** [GitLab CI/CD Docs](https://docs.gitlab.com/ee/ci/)
- **Tutoriale:**
    - YouTube: "GitLab CI/CD Tutorial for Beginners".
    - Kurs na Udemy: "Mastering GitLab CI/CD".
- **Notatki:** Twórz w Obsidianie powiązane strony, np. [[Pipeline]], [[Runner]].

## 8. Pytania na rozmowę

- Jak skonfigurujesz pipeline dla aplikacji wielojęzykowej?
- Co zrobisz, jeśli job się zawiesi?
- Jak zabezpieczysz sekrety w GitLab CI/CD?