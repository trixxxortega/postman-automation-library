# 🧪 *Postman API Automation + CI con GitHub Actions*

Este repositorio contiene pruebas automatizadas de una API de prueba usando Postman, ejecutadas con **Newman** y validadas en cada push mediante **GitHub Actions**.

---

## 📦 *Contenido*

- `LibraryAPI.postman_collection.json`: colección de tests Postman
- `QA.postman_environment.json`: entorno con variables necesarias
- `.github/workflows/postman-tests.yml`: workflow para correr los tests automáticamente en GitHub

---

## 🚀 *Cómo correr los tests localmente*

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
