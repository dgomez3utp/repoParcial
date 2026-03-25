# API LLM con Gemini

Una API REST construida con **FastAPI** que integra el modelo de lenguaje **Gemini** de Google para generar contenido basado en prompts.

## 📋 Descripción del Proyecto

Este proyecto expone un servicio web que permite interactuar con el modelo de IA **Gemini 3 Flash** a través de una API HTTP. Los usuarios pueden enviar prompts en texto y recibir respuestas generadas por el modelo de IA.

## 🔧 Requisitos Previos

- Python 3.8 o superior
- pip (gestor de paquetes de Python)
- Clave de API de Google Gemini (`GEMINI_API_KEY`)

## 📦 Instalación

### 1. Clonar el repositorio

```bash
git clone <URL-del-repositorio>
cd repoParcial
```

### 2. Crear un entorno virtual (recomendado)

```bash
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

## ⚙️ Configuración

### 1. Configurar la clave de API

Crea un archivo `.env` en la raíz del proyecto:

```env
GEMINI_API_KEY=tu_clave_api_aqui
```

**Nota:** Nunca compartir ni hacer commit de archivo `.env` con credenciales reales.

### 2. Variables de entorno

El proyecto utiliza `python-dotenv` para cargar variables desde el archivo `.env`.

## 🚀 Uso

### Iniciar la aplicación

```bash
uvicorn main:app --reload
```

La API estará disponible en `http://localhost:8000`

### Documentación interactiva

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## 📡 Endpoints

### GET `/llm/{prompt}`

Genera contenido usando el modelo Gemini basado en el prompt proporcionado.

**Parámetros:**
- `prompt` (string, requerido): El texto del prompt para el modelo de IA

**Respuesta exitosa (200 OK):**
```json
{
  "Respuesta": "Contenido generado por Gemini..."
}
```

**Ejemplo de solicitud:**

```bash
curl "http://localhost:8000/llm/¿Cuál%20es%20la%20capital%20de%20Francia?"
```

**Ejemplo en Python:**

```python
import requests

url = "http://localhost:8000/llm/Explica qué es machine learning"
response = requests.get(url)
data = response.json()
print(data["Respuesta"])
```

## 📁 Estructura del Proyecto

```
repoParcial/
├── main.py                   # Archivo principal de la aplicación
├── requirements.txt          # Dependencias del proyecto
├── .env                      # Variables de entorno (no incluir en git)
├── README.md                 # Este archivo
└── __pycache__/             # Caché de Python
```

## 🔑 Dependencias Principales

| Librería | Versión | Descripción |
|----------|---------|-------------|
| **fastapi** | 0.135.2 | Framework web para APIs REST |
| **uvicorn** | (no especificada) | Servidor ASGI para ejecutar FastAPI |
| **google-genai** | 1.68.0 | Cliente oficial de Google Gemini |
| **python-dotenv** | 1.2.2 | Carga variables de entorno desde `.env` |
| **pydantic** | 2.12.5 | Validación de datos |

## 🛠️ Desarrollo

### Instalar dependencias de desarrollo

```bash
pip install -r requirements.txt
```

### Ejecutar en modo desarrollo con recarga automática

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

## 📝 Notas Importantes

- ⚠️ **Seguridad:** Nunca incluir claves de API en archivos públicos o repositorios
- 📋 **Rate Limiting:** Considerar implementar límite de velocidad en producción
- 🔒 **Autenticación:** Para producción, se recomienda agregar autenticación a los endpoints
- 🐛 **Errores:** Actualmente no hay manejo explícito de errores; considerar agregarlo

## 📄 Ejemplo de Uso Completo

```python
import requests

# URL base
BASE_URL = "http://localhost:8000"

# Realizar consulta
prompt = "¿Qué es la inteligencia artificial?"
response = requests.get(f"{BASE_URL}/llm/{prompt}")

# Procesar respuesta
if response.status_code == 200:
    resultado = response.json()
    print("Respuesta de Gemini:")
    print(resultado["Respuesta"])
else:
    print(f"Error: {response.status_code}")
```

## 📄 Licencia

Este proyecto es de propósito educativo.

## 👤 Autor

Proyecto de parcial - Entornos de Desarrollo de Software

---

**Última actualización:** Marzo 2026
