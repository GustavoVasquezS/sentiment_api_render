# Sentiment Analysis API v4.0 (Español/Portugués)

API para análisis de sentimiento en español y portugués, basada en un modelo TF-IDF + Regresión Logística calibrada. El modelo fue entrenado sobre reseñas multilingües y clasifica comentarios en tres categorías: **Negativo**, **Neutro** y **Positivo**.

## Modelo
- **Pipeline:** Limpieza de texto → TF-IDF → Regresión Logística → Calibración de probabilidades
- **Entrenamiento:** Reseñas en español y portugués, etiquetas derivadas de estrellas (1-2 Negativo, 3 Neutro, 4-5 Positivo)
- **Artefacto:** `sentiment_bundle_es_pt_v2.joblib` contiene el pipeline calibrado, umbral de confianza, metadatos y términos explicativos

## Predicciones
- **Entrada:** Texto libre (string, 5-2000 caracteres)
- **Salida:**
  - `prevision`: Sentimiento predicho (`Negativo`, `Neutro`, `Positivo`)
  - `probabilidad`: Confianza de la predicción (0-1)
  - `review_required`: `true` si la confianza es baja y requiere revisión humana

## Endpoints principales
- `GET /health`: Estado y versión del modelo
- `POST /predict`: Predicción individual
- `POST /predict/batch`: Predicción múltiple (máx 100 textos)

## Instrucciones de uso

1. Instala dependencias:
   ```bash
   pip install -r requirements.txt
   ```
2. Ejecuta la API:
   ```bash
   python main.py
   ```
3. Accede a la documentación interactiva en [http://localhost:8000/docs](http://localhost:8000/docs)

## Ejemplo de predicción
```json
{
  "prevision": "Positivo",
  "probabilidad": 0.95,
  "review_required": false
}
```

## Despliegue en Render
- Usa el comando: `uvicorn main:app --host 0.0.0.0 --port $PORT`
- El modelo debe estar en la raíz del proyecto
