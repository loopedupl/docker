# Optymalizacja obrazów Dockera

## Cel lekcji

W tej lekcji dowiesz się, jak tworzyć lekkie, szybkie i efektywne obrazy Dockera. Poznasz zasady najlepszych praktyk w pisaniu plików Dockerfile, minimalizowaniu rozmiaru obrazów oraz unikaniu błędów, które mogą negatywnie wpływać na wydajność.

---

## Agenda

1. **Dlaczego optymalizacja obrazów Dockera jest ważna?**

   - Wpływ na wydajność i koszty
   - Przykłady problemów wynikających z dużych obrazów

2. **Najlepsze praktyki w pisaniu Dockerfile**

   - Wybór odpowiednich bazowych obrazów
   - Minimalizacja warstw w obrazie
   - Unikanie niepotrzebnych plików

3. **Używanie lekkich obrazów bazowych**

   - `alpine` vs. pełne obrazy systemowe
   - Porównanie rozmiarów i wydajności

4. **Korzystanie z instrukcji multi-stage build**

   - Jak oddzielić proces budowy od finalnego obrazu
   - Przykłady zastosowania

5. **Analiza i zmniejszanie rozmiaru obrazów**

   - Użycie narzędzi takich jak `docker image inspect` i `dive`
   - Usuwanie zbędnych zależności i plików

6. **Praktyczny przykład optymalizacji obrazu**
   - Optymalizacja obrazu aplikacji Node.js
   - Porównanie przed i po optymalizacji

---

## Materiały lekcji

### 1. Dlaczego optymalizacja obrazów Dockera jest ważna?

Optymalizacja obrazów Dockera ma kluczowe znaczenie w projektach, które:

- Są wdrażane w środowiskach produkcyjnych z ograniczonymi zasobami.
- Wymagają częstych aktualizacji obrazów (np. w CI/CD).
- Działają w środowiskach chmurowych, gdzie koszty transferu i przechowywania danych mają znaczenie.

Przykład: Obraz o rozmiarze 1 GB może znacząco wydłużyć czas wdrożenia i zwiększyć koszty w porównaniu z obrazem o rozmiarze 50 MB.

### 2. Najlepsze praktyki w pisaniu Dockerfile

- **Wybieraj odpowiednie obrazy bazowe**: Zamiast pełnego obrazu systemowego, takiego jak `ubuntu`, używaj lekkich obrazów, np. `alpine`.
- **Minimalizuj liczbę warstw**: Łącz instrukcje `RUN` w jednym poleceniu, aby zmniejszyć liczbę warstw.  
  Przykład:
  ```dockerfile
  RUN apt-get update && apt-get install -y curl && apt-get clean
  ```
- **Usuń zbędne pliki**: Usuń tymczasowe pliki i pamięć podręczną po instalacjach.  
  Przykład:
  ```dockerfile
  RUN rm -rf /var/lib/apt/lists/*
  ```

### 3. Używanie lekkich obrazów bazowych

Obrazy bazowe, takie jak `alpine`, są idealne do aplikacji, które nie wymagają pełnego środowiska systemowego.  
Przykład:

- `ubuntu`: ~29 MB
- `alpine`: ~5 MB

Dzięki temu możesz znacznie zmniejszyć rozmiar finalnego obrazu.

### 4. Korzystanie z instrukcji multi-stage build

Multi-stage build pozwala na oddzielenie procesu budowy aplikacji od finalnego obrazu.  
Przykład dla aplikacji Node.js:

```dockerfile
# Etap 1: Budowa aplikacji
FROM node:18 as builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Etap 2: Finalny obraz
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
CMD ["node", "dist/index.js"]
```

W tym przykładzie finalny obraz zawiera tylko to, co jest niezbędne do uruchomienia aplikacji.

### 5. Analiza i zmniejszanie rozmiaru obrazów

Narzędzia takie jak `dive` mogą pomóc w analizie zawartości obrazu Dockera. Dzięki temu możesz zidentyfikować niepotrzebne pliki i warstwy, które można usunąć.  
Przykład użycia `dive`:

```bash
dive my-docker-image
```

### 6. Praktyczny przykład optymalizacji obrazu

Załóżmy, że tworzysz obraz aplikacji Node.js. Początkowy Dockerfile:

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "index.js"]
```

Rozmiar obrazu: ~900 MB.

Po optymalizacji:

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "index.js"]
```

Rozmiar obrazu: ~60 MB.
