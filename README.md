# Wdrażanie aplikacji w produkcji

## Cel lekcji

W tej lekcji dowiesz się, jak przygotować aplikację kontenerową do wdrożenia w środowisku produkcyjnym. Nauczysz się najlepszych praktyk związanych z konfiguracją, bezpieczeństwem, monitorowaniem oraz skalowaniem aplikacji w Dockerze.

---

## Agenda

1. **Przygotowanie aplikacji do produkcji**

   - Różnice między środowiskiem developerskim a produkcyjnym
   - Tworzenie zoptymalizowanych obrazów Dockera

2. **Zarządzanie zmiennymi środowiskowymi**

   - Przechowywanie i przekazywanie danych konfiguracyjnych
   - Użycie plików `.env` oraz narzędzi takich jak Docker Secrets

3. **Bezpieczeństwo w środowisku produkcyjnym**

   - Ograniczanie uprawnień kontenera
   - Aktualizacja obrazów Dockera i zależności

4. **Monitorowanie i logowanie**

   - Integracja z narzędziami do monitorowania (Prometheus, Grafana)
   - Centralizacja logów z kontenerów

5. **Skalowanie aplikacji**

   - Użycie Docker Compose do uruchamiania aplikacji w trybie produkcyjnym
   - Wprowadzenie do Docker Swarm i Kubernetes

6. **Testowanie aplikacji w środowisku produkcyjnym**

   - Symulowanie ruchu użytkowników
   - Automatyczne testy akceptacyjne

7. **Praktyczne wdrożenie aplikacji**
   - Przykład wdrożenia aplikacji wielokontenerowej na serwerze produkcyjnym

---

## Materiały lekcji

### 1. Przygotowanie aplikacji do produkcji

Przygotowanie aplikacji do produkcji wymaga zoptymalizowania obrazów Dockera:

- **Minimalizacja rozmiaru obrazu**: Używaj lekkich baz, takich jak `alpine`.
- **Usuwanie zbędnych plików**: Usuń pliki tymczasowe po instalacji zależności.  
  Przykład Dockerfile:

```dockerfile
FROM node:alpine
WORKDIR /app
COPY package.json .
RUN npm install && npm cache clean --force
COPY . .
CMD ["node", "server.js"]
```

### 2. Zarządzanie zmiennymi środowiskowymi

W środowisku produkcyjnym należy unikać przechowywania danych wrażliwych w kodzie.

- Tworzenie pliku `.env`:
  ```env
  DB_HOST=localhost
  DB_USER=root
  DB_PASSWORD=securepassword
  ```
- Użycie zmiennych w Docker Compose:
  ```yaml
  version: "3.8"
  services:
    app:
      image: my-app
      env_file:
        - .env
  ```

### 3. Bezpieczeństwo w środowisku produkcyjnym

- **Ograniczenie uprawnień kontenera**:  
  Używaj flagi `--read-only`, aby ograniczyć zapisywanie danych w kontenerze.
  ```bash
  docker run --read-only my-app
  ```
- **Aktualizacja obrazów**:  
  Regularnie aktualizuj obrazy Dockera, aby unikać luk w zabezpieczeniach.

### 4. Monitorowanie i logowanie

Integracja z narzędziami do monitorowania pozwala na wczesne wykrywanie problemów:

- **Prometheus**: Do zbierania danych metrycznych.
- **Grafana**: Do wizualizacji danych.

Przykład konfiguracji Prometheus z Docker Compose:

```yaml
version: "3.8"
services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
```

### 5. Skalowanie aplikacji

Docker Compose umożliwia skalowanie usług:

```bash
docker-compose up --scale app=3
```

Dla bardziej zaawansowanych potrzeb można użyć Docker Swarm lub Kubernetes.

### 6. Testowanie aplikacji w środowisku produkcyjnym

- Symulowanie ruchu: Użyj narzędzi takich jak **Apache JMeter** lub **Postman** do generowania zapytań.
- Automatyczne testy akceptacyjne: Skonfiguruj testy przy użyciu frameworków takich jak Selenium lub Cypress.

### 7. Praktyczne wdrożenie aplikacji

Przykład wdrożenia aplikacji na serwer produkcyjny:

1. Zbuduj obraz:
   ```bash
   docker build -t my-app .
   ```
2. Wypchnij obraz do rejestru:
   ```bash
   docker push my-registry/my-app
   ```
3. Uruchom kontener na serwerze:
   ```bash
   docker run -d -p 80:80 my-registry/my-app
   ```
