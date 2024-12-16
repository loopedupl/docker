# Tworzenie obrazów Dockera za pomocą Dockerfile

## Cel lekcji

W tej lekcji nauczysz się, jak tworzyć własne obrazy Docker za pomocą pliku `Dockerfile`. Przeprowadzimy Cię przez proces tworzenia pliku, który będzie zawierał instrukcje do budowy obrazu, oraz pokażemy, jak go zbudować i uruchomić kontener na podstawie tego obrazu.

---

## Agenda

1. **Wprowadzenie do Dockerfile**

   - Co to jest Dockerfile i jak działa
   - Podstawowa struktura Dockerfile

2. **Tworzenie Dockerfile dla aplikacji**

   - Wybór obrazu bazowego
   - Instalowanie zależności
   - Kopiowanie plików aplikacji do obrazu

3. **Budowanie obrazu Docker**

   - Komenda `docker build`
   - Budowanie obrazu z Dockerfile
   - Tagowanie obrazu

4. **Uruchamianie kontenera z własnego obrazu**

   - Komenda `docker run`
   - Uruchamianie kontenera z własnego obrazu

5. **Optymalizacja Dockerfile**
   - Użycie wieloetapowego budowania (multi-stage builds)
   - Minimalizowanie rozmiaru obrazu

---

## Materiały lekcji

### 1. Wprowadzenie do Dockerfile

Dockerfile to plik tekstowy, który zawiera zestaw instrukcji do budowy obrazu Docker. Dzięki niemu możemy zautomatyzować proces tworzenia obrazów, co jest szczególnie przydatne w produkcji i automatyzacji.

Podstawowy szablon Dockerfile może wyglądać tak:

```dockerfile
# Wybieramy obraz bazowy
FROM ubuntu:20.04

# Instalujemy zależności
RUN apt-get update && apt-get install -y python3 python3-pip

# Kopiujemy pliki aplikacji
COPY . /app

# Ustawiamy katalog roboczy
WORKDIR /app

# Instalujemy zależności aplikacji
RUN pip3 install -r requirements.txt

# Ustawiamy domyślną komendę
CMD ["python3", "app.py"]
```

### 2. Tworzenie Dockerfile dla aplikacji

#### Wybór obrazu bazowego

Obraz bazowy to obraz, na którym będziemy budować naszą aplikację. W przypadku aplikacji Python, możemy zacząć od obrazu `python`:

```dockerfile
FROM python:3.9-slim
```

#### Instalowanie zależności

Za pomocą komendy `RUN` możemy instalować zależności w obrazie. Przykład instalacji zależności dla aplikacji Python:

```dockerfile
RUN pip install --no-cache-dir -r requirements.txt
```

#### Kopiowanie plików aplikacji do obrazu

Za pomocą komendy `COPY` możemy skopiować pliki aplikacji do obrazu:

```dockerfile
COPY . /app
```

### 3. Budowanie obrazu Docker

Po stworzeniu Dockerfile, możemy zbudować obraz za pomocą komendy `docker build`. Przykład:

```bash
docker build -t my-python-app .
```

Komenda ta zbuduje obraz z bieżącego katalogu (`.`) i nada mu nazwę `my-python-app`.

#### Tagowanie obrazu

Aby nadać obrazowi wersję, możemy go otagować:

```bash
docker build -t my-python-app:v1 .
```

### 4. Uruchamianie kontenera z własnego obrazu

Po zbudowaniu obrazu, możemy uruchomić kontener z tego obrazu za pomocą komendy `docker run`:

```bash
docker run -d -p 5000:5000 my-python-app:v1
```

Ta komenda uruchomi kontener w tle (`-d`) i przekaże port 5000 z kontenera na port 5000 na maszynie hosta.

### 5. Optymalizacja Dockerfile

#### Użycie wieloetapowego budowania (multi-stage builds)

Wieloetapowe budowanie pozwala na zbudowanie obrazu w kilku etapach, co pozwala na zmniejszenie rozmiaru końcowego obrazu. Przykład:

```dockerfile
# Etap 1: Budowanie aplikacji
FROM node:14 AS build-stage
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Etap 2: Uruchamianie aplikacji
FROM nginx:alpine
COPY --from=build-stage /app/build /usr/share/nginx/html
```

Dzięki temu końcowy obraz będzie zawierał tylko pliki potrzebne do uruchomienia aplikacji, a nie wszystkie zależności do budowania.

#### Minimalizowanie rozmiaru obrazu

Zaleca się korzystanie z mniejszych obrazów bazowych, takich jak `alpine`, aby zmniejszyć rozmiar obrazu:

```dockerfile
FROM node:14-alpine
```
