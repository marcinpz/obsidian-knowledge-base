# Podstawy DevOps z GCP

## 1. Czym jest DevOps?
- **Definicja**: DevOps to kultura i zestaw praktyk łączących rozwój oprogramowania (Dev) z operacjami IT (Ops), aby przyspieszyć dostarczanie oprogramowania i zwiększyć jego niezawodność.
- **Kluczowe zasady**:
  - Automatyzacja procesów.
  - Ciągła integracja i dostarczanie (CI/CD).
  - Monitorowanie i reagowanie w czasie rzeczywistym.
  - Współpraca między zespołami.

## 2. Google Cloud Platform (GCP) w DevOps
- **Dlaczego GCP?**: Elastyczność, skalowalność, natywne wsparcie dla kontenerów i CI/CD.
- **Podstawowe usługi GCP**:
  - **Compute Engine**: Wirtualne maszyny (VM) do uruchamiania aplikacji.
  - **Kubernetes Engine (GKE)**: Zarządzanie klastrami Kubernetes do konteneryzacji.
  - **Cloud Build**: Narzędzie do CI/CD, automatyzujące budowanie, testowanie i wdrażanie.
  - **Cloud Functions**: Serverless do uruchamiania kodu w odpowiedzi na zdarzenia.
  - **Cloud Storage**: Magazyn obiektowy na dane i artefakty.
  - **Cloud Monitoring i Logging**: Monitorowanie wydajności i debugowanie.

## 3. CI/CD w GCP
- **Proces**:
  1. **Kod**: Repozytorium w Cloud Source Repositories lub GitHub/Bitbucket.
  2. **Budowanie**: Cloud Build kompiluje kod i tworzy artefakty (np. obrazy Docker).
  3. **Testowanie**: Automatyczne testy w pipeline’ach Cloud Build.
  4. **Wdrożenie**: Deploy na GKE, App Engine lub Compute Engine.
- **Narzędzia**:
  - **Cloud Build**: Konfiguracja w `cloudbuild.yaml`.
  - **Artifact Registry**: Przechowywanie obrazów kontenerów.
  - **Spinnaker**: Opcjonalne narzędzie do zaawansowanego CD.

## 4. Konteneryzacja i [[podstawy]]
- **Docker**: Tworzenie lekkich kontenerów z aplikacjami.
- **GKE**:
  - Zarządzane środowisko Kubernetes.
  - Automatyczne skalowanie (HPA) i aktualizacje.
  - Wdrożenie: `kubectl apply -f deployment.yaml`.
- **Podstawowe polecenia**:
  - `docker build -t gcr.io/[PROJECT-ID]/app .`
  - `docker push gcr.io/[PROJECT-ID]/app`
  - `kubectl get pods`

## 5. Infrastruktura jako kod (IaC)
- **Cloud Deployment Manager**: Definiowanie zasobów GCP w YAML lub Jinja.
- **[[terraform]]**: Alternatywa open-source do zarządzania infrastrukturą multi-cloud.
- **Przykład (Deployment Manager)**:
  ```yaml
  resources:
  - name: my-vm
    type: compute.v1.instance
    properties:
      zone: us-central1-a
      machineType: n1-standard-1
  ```

## 6. Monitorowanie i logowanie
- **Cloud Monitoring**: Metryki, dashboardy, alerty.
- **Cloud Logging**: Analiza logów z aplikacji i infrastruktury.
- **Kluczowe metryki**:
  - Użycie CPU/RAM w GKE.
  - Latencja i błędy w App Engine.

## 7. Bezpieczeństwo w DevOps
- **IAM**: Role i uprawnienia (np. `roles/cloudbuild.builds.editor`).
- **Secret Manager**: Przechowywanie kluczy API i haseł.
- **VPC Service Controls**: Izolacja zasobów.

## 8. Typowe pytania na rozmowie
- Jak skonfigurujesz pipeline CI/CD w Cloud Build?
- Jak skalujesz aplikację w GKE?
- Jak debugujesz problem w produkcji na GCP?
- Czym różni się Compute Engine od GKE?

## 9. Praktyczne wskazówki
- **Ćwicz**: Skonfiguruj prosty pipeline CI/CD w GCP.
- **Dokumentacja**: Zapoznaj się z oficjalną dokumentacją GCP.
- **Certyfikaty**: Rozważ „Professional DevOps Engineer” od Google.

---
**Tagi**: #DevOps #GCP #CI/CD #Kubernetes #IaC