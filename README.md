## Documentación de notebooks

### `llms.ipynb`

#### Propósito
Notebook de referencia para interactuar con modelos de lenguaje grandes (LLMs) alojados en la API de NVIDIA. Muestra cómo:

1. Cargar variables de entorno mediante `python-dotenv`.
2. Consultar el catálogo de modelos disponibles usando `requests`.
3. Realizar inferencias por REST usando `requests.post` en modo streaming.
4. Utilizar SDKs de alto nivel como `openai` (cliente compatible) y `langchain` (`ChatNVIDIA`).

#### Requisitos previos
- Python 3.10 o superior.
- Dependencias principales: `python-dotenv`, `requests`, `openai>=1.40`, `langchain`, `langchain-nvidia-ai-endpoints`.
- Variable de entorno `NVIDIA_API_KEY` con un token válido. Opcionalmente `OPENAI_API_KEY` si se desea usar la API de OpenAI.
- Archivo `.env` (opcional) con las claves anteriores si se quiere cargar automáticamente via `dotenv`.

#### Estructura del notebook
1. **Configuración inicial:** carga variables de entorno con `load_dotenv()` y valida el acceso a la API.
2. **Exploración de modelos:** petición GET a `https://integrate.api.nvidia.com/v1/models` para listar modelos disponibles.
3. **Chat completions vía REST:** ejemplo completo de request streaming a `https://integrate.api.nvidia.com/v1/chat/completions`, incluyendo utilitario para procesar tokens.
4. **Clientes compatibles con OpenAI:** uso del cliente `openai.OpenAI` apuntando al endpoint de NVIDIA, con ejemplos streaming y non-streaming.
5. **Integración con LangChain:** creación de un `ChatNVIDIA` y ejemplos de `invoke`, `stream` y `StrOutputParser`.
6. **Inspección de contexto:** muestra cómo acceder a los inputs/outputs recientes (`llm._client.last_inputs` y `last_response`).

#### Cómo ejecutar
1. Crear y activar un entorno virtual (recomendado).
2. Instalar dependencias: `pip install python-dotenv requests openai langchain langchain-nvidia-ai-endpoints`.
3. Definir la variable `NVIDIA_API_KEY` (en terminal o archivo `.env`).
4. Abrir el notebook en Jupyter (`jupyter lab` o `jupyter notebook`) y ejecutar las celdas en orden.

#### Notas y buenas prácticas
- Nunca subas tus claves a control de versiones; usa `.env` y agrégalo a `.gitignore`.
- Si un modelo devuelve error 404, prueba con otro modelo listado en la sección de exploración.
- Ajusta `temperature`, `top_p` y `max_tokens` según el caso de uso.
- Para workloads largos, considera manejar los tokens de stream en lugar de imprimirlos directamente para reutilizar la respuesta.