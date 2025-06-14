# 🧪 *Postman API Automation + CI con GitHub Actions*

Este repositorio contiene pruebas automatizadas de una API de prueba usando Postman, ejecutadas con **Newman** y validadas en cada push mediante **GitHub Actions**.

---

## 📦 *Contenido*

- `LibraryAPI.postman_collection.json`: colección de tests Postman
- `QA.postman_environment.json`: entorno con variables necesarias
- `.github/workflows/postman-tests.yml`: workflow para correr los tests automáticamente en GitHub

---

## 🚀 *Cómo correr los tests localmente*

## ✅ Requisitos previos

1. Instalar [Node.js](https://nodejs.org)
2. Instalar Newman:

```bash
npm install -g newman
```
---

## *Correr la collection localmente*

```
newman run LibraryAPI.postman_collection.json \
  -e QA.postman_environment.json \
  -r cli,html \
  --reporter-html-export reporte.html
```

# 🚀 Pasos para Ejecutar la Collection con Newman en GitHub Actions

Este proyecto describe cómo ejecutar pruebas de una colección de Postman usando Newman en un workflow automatizado de GitHub Actions.

---

## ✅ Requisitos previos

- Tener una cuenta en GitHub, con las credenciales SSH debidamente seteadas
- Tener Postman instalado

---

## 🧪 Pasos

1. Crear un repositorio Git local (una carpeta local que luego inicializás con `git init`)
2. Crear un repositorio en GitHub con el mismo nombre
3. Conectar ambos repositorios (`git remote add origin <url-del-repo>`)
4. Desde Postman, exportar la colección (Archivo `*.postman_collection.json`) y dejarla en el directorio raíz de la carpeta creada en el paso 1
5. Desde Postman, exportar la configuración del ambiente (Archivo `*.postman_environment.json`) y dejarla en el directorio raíz de la carpeta creada en el paso 1
6. En tu máquina, crear un directorio llamado `.github` en la carpeta raíz del proyecto, creado en el paso 1
7. Dentro de ese directorio `.github`, crear un subdirectorio llamado `workflows`
10. Crear dentro de `workflows` un archivo `.yml` con la configuración para correr los tests con Newman (Ver: **Ejemplo de archivo .yml**)
11. Subir todos los archivos y cambios al repositorio en GitHub:
    
    ```bash
    git add .
    git commit -m "Configuración inicial de Postman + Newman"
    git push origin main
    ```
13. Verificar los resultados de la ejecución automática en la pestaña **Actions** del repositorio en GitHub

---

## 📄 Ejemplo de archivo `.yml`

```yaml
name: Run Postman Tests

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Instalar Node y Newman
        run: |
          npm install -g newman
          npm install -g newman-reporter-html

      - name: Ejecutar colección
        run: |
          newman run TuColeccion.postman_collection.json \
            -e TuEnvironment.postman_environment.json \
            -r cli,html \
            --reporter-html-export reporte.html

      - name: Subir reporte como artefacto
        uses: actions/upload-artifact@v3
        with:
          name: newman-report
          path: reporte.html
