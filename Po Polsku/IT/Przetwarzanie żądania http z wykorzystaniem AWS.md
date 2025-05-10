# Jak działa serwis WWW na AWS?

Gdy wpisujesz adres serwisu WWW w przeglądarce, uruchamia się ciąg procesów, które prowadzą do wyświetlenia strony. Poniżej wyjaśnienie, jak to działa w kontekście serwisu hostowanego na AWS, jakie technologie mogą być użyte oraz przykładowy setup na AWS.

## Proces działania

1. **Wpisanie adresu URL**:
   - W przeglądarce wpisujesz np. `https://example.com`. Przeglądarka rozpoznaje protokół (HTTPS), domenę (`example.com`) i ewentualnie ścieżkę (np. `/strona`).
   - Przeglądarka wysyła żądanie HTTP/HTTPS do serwera powiązanego z domeną.

2. **Rozwiązanie DNS**:
   - Przeglądarka kontaktuje się z serwerem DNS, aby przetłumaczyć nazwę domeny na adres IP serwera.
   - Na AWS domena może być zarejestrowana w **Route 53**, który działa jako usługa DNS i kieruje żądanie do odpowiedniego zasobu (np. load balancera, serwera lub CDN).

3. **Dotarcie do infrastruktury AWS**:
   - Żądanie trafia do punktu wejścia w AWS, np.:
     - **Amazon CloudFront** (CDN) – dla treści statycznych (np. obව

4. **Przetwarzanie żądania**:
   - Serwer (np. na **EC2**, **ECS**, **EKS** lub **Lambda**) przetwarza żądanie:
     - Dla treści statycznych (np. HTML, CSS, JS) serwery zwracają pliki z **S3** lub CloudFront.
     - Dla treści dynamicznych (np. dane z bazy) aplikacja (np. w Node.js, Python, Java) komunikuje się z bazą danych (np. **RDS**, **DynamoDB**) lub innymi usługami.
   - Backend generuje odpowiedź (np. HTML, JSON) i zwraca ją do przeglądarki.

5. **Wyświetlenie strony**:
   - Przeglądarka odbiera odpowiedź, renderuje stronę (parsuje HTML, wykonuje JS, ładuje zasoby jak obrazy czy CSS).
   - Jeśli strona korzysta z JavaScript (np. React, Vue), wykonuje się dodatkowa logika po stronie klienta.

## Technologie wykorzystywane

### Po stronie klienta
- **HTML/CSS/JavaScript**: Podstawa strony.
- **Frameworki JS**: React, Vue.js, Angular do dynamicznych interfejsów.
- **Narzędzia budowania**: Webpack, Vite do kompilacji i optymalizacji kodu.

### Po stronie serwera
- **Języki**: Node.js, Python (Flask, Django), Java (Spring), PHP, Ruby, Go.
- **Serwery WWW**: Nginx, Apache.
- **API**: REST lub GraphQL.

### Po stronie AWS
- **Compute**:
  - **EC2**: Wirtualne maszyny dla aplikacji.
  - **ECS/EKS**: Kontenery (Docker) dla skalowalnych aplikacji.
  - **Lambda**: Serverless dla prostych endpointów.
- **Storage**:
  - **S3**: Pliki statyczne (HTML, CSS, JS, obrazy).
  - **EFS/EBS**: Systemy plików dla EC2.
- **Bazy danych**:
  - **RDS**: Relacyjne bazy (MySQL, PostgreSQL).
  - **DynamoDB**: NoSQL dla wysokiej skalowalności.
  - **ElastiCache**: Redis/Memcached dla cache.
- **Sieć i dostarczanie treści**:
  - **Route 53**: DNS.
  - **CloudFront**: CDN dla treści statycznych.
  - **ELB**: Rozkładanie obciążenia.
  - **ACM**: Certyfikaty SSL/TLS.
- **Monitorowanie i zarządzanie**:
  - **CloudWatch**: Logi, metryki, alarmy.
  - **AWS Systems Manager**: Zarządzanie instancjami.

## Przykładowy setup na AWS

Oto przykład prostego, skalowalnego setupu dla aplikacji webowej:

1. **Domena i DNS**:
   - Domena w **Route 53**, wskazująca na **CloudFront** (treści statyczne) lub **Application Load Balancer (ALB)** (aplikacja dynamiczna).

2. **Treści statyczne**:
   - Pliki HTML, CSS, JS w **S3**.
   - Dystrybucja przez **CloudFront** z HTTPS (certyfikat z **ACM**).

3. **Backend**:
   - Aplikacja (np. Node.js z Express) na **ECS** (kontenery Docker) w trybie Fargate.
   - Skalowanie automatyczne dzięki **Auto Scaling Group** na podstawie metryk **CloudWatch** (np. CPU).
   - **ALB** rozdziela ruch między kontenery.

4. **Baza danych**:
   - **RDS** z PostgreSQL w trybie Multi-AZ dla wysokiej dostępności.
   - Opcjonalnie **DynamoDB** dla danych NoSQL (np. sesje).

5. **Cache**:
   - **ElastiCache** (Redis) dla cache’owania wyników zapytań.

6. **Monitorowanie**:
   - **CloudWatch** dla logów i metryk.
   - Alerty na podstawie metryk (np. błędy 5xx, wysoka latencja).

7. **CI/CD**:
   - Kod w repozytorium (np. GitHub) z pipeline’em w **AWS CodePipeline**.
   - Budowanie i deployment przez **CodeBuild** i **CodeDeploy**.

## Przepływ żądania w setupie
1. Użytkownik wpisuje `https://example.com`.
2. **Route 53** rozwiązuje domenę na IP **CloudFront** lub **ALB**.
3. **CloudFront** zwraca pliki z **S3** (np. index.html, CSS, JS).
4. Przeglądarka wykonuje zapytania API do **ALB**, który kieruje je do **ECS**.
5. Aplikacja w **ECS** komunikuje się z **RDS** lub **DynamoDB**, ewentualnie z **ElastiCache**.
6. Backend zwraca JSON, który przeglądarka renderuje.

## Uwagi dodatkowe
- **Koszty**: Używaj **Spot Instances** na EC2, **Reserved Instances** dla RDS, analizuj koszty w **AWS Cost Explorer**.
- **Bezpieczeństwo**: Włącz **WAF** (Web Application Firewall) na **CloudFront** lub **ALB** dla ochrony przed atakami (np. DDoS).
- **Skalowalność**: Architektura powinna być bezstanowa (stateless) dla łatwego skalowania horyzontalnego.

> **Notatka**: Szczegółowe konfiguracje (np. ECS, optymalizacja kosztów) dostępne na żądanie.