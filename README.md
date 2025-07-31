# RAG con Ollama y Qwen3

Este proyecto implementa un sistema de Retrieval-Augmented Generation (RAG) utilizando Ollama con el modelo Qwen3, ChromaDB para almacenamiento vectorial, y LangChain para orquestación.

## Características

- **Modelo Local**: Utiliza Ollama con Qwen3 para ejecutar el modelo LLM localmente
- **Base de Datos Vectorial**: ChromaDB para almacenamiento y búsqueda de embeddings
- **Procesamiento de PDFs**: Carga y procesa documentos PDF automáticamente
- **Interfaz Simple**: Script Python fácil de usar para consultas de documentos

## Requisitos Previos

- Python 3.8 o superior
- macOS, Linux o Windows
- Al menos 8GB de RAM (recomendado 16GB para mejor rendimiento)

## Instalación y Configuración

### 1. Instalar Ollama

#### En macOS:

```bash
# Descargar e instalar desde el sitio oficial
curl -fsSL https://ollama.ai/install.sh | sh

# O usando Homebrew
brew install ollama
```

#### En Linux:

```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

#### En Windows:

Descarga el instalador desde [https://ollama.ai/download](https://ollama.ai/download)

### 2. Iniciar el Servicio de Ollama

```bash
# Iniciar Ollama (se ejecuta como servicio en background)
ollama serve
```

### 3. Instalar el Modelo Qwen3

```bash
# Instalar el modelo Qwen3 (esto puede tomar varios minutos)
ollama pull qwen2.5:7b

# Verificar que el modelo esté instalado
ollama list
```

### 4. Clonar el Repositorio

```bash
git clone https://github.com/Emilf16/RAG-WITH-OLLAMA-QWEN3.git
cd RAG-WITH-OLLAMA-QWEN3
```

### 5. Crear Entorno Virtual de Python

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno virtual
# En macOS/Linux:
source venv/bin/activate

# En Windows:
# venv\Scripts\activate
```

### 6. Instalar Dependencias de Python

```bash
# Instalar las dependencias necesarias
pip install langchain-community
pip install langchain-ollama
pip install langchain-core
pip install langchain-text-splitters
pip install chromadb
pip install pypdf
pip install python-dotenv

# O crear un requirements.txt e instalar todo de una vez:
pip install -r requirements.txt
```

### 7. Configurar Variables de Entorno (Opcional)

```bash
# Crear archivo .env si necesitas configuraciones específicas
echo "OLLAMA_BASE_URL=http://localhost:11434" > .env
```

## Uso

### 1. Preparar tus Documentos

Coloca tus archivos PDF en la carpeta `data/`. El script está configurado para procesar el archivo `documento_prueba.pdf` por defecto, que contiene información de ejemplo sobre el sistema RAG.

### 2. Ejecutar el Script

```bash
# Asegúrate de que Ollama esté ejecutándose
ollama serve

# En otra terminal, ejecutar el script RAG
python rag_local.py
```

### 3. Realizar Consultas

El script cargará los documentos, creará los embeddings, y te permitirá hacer preguntas sobre el contenido de los PDFs.

## Estructura del Proyecto

```
RAG-WITH-OLLAMA-QWEN3/
├── README.md                 # Este archivo
├── rag_local.py             # Script principal del RAG
├── requirements.txt         # Dependencias de Python
├── .gitignore              # Archivos a ignorar en Git
├── .env                    # Variables de entorno (opcional)
├── data/                   # Carpeta para archivos PDF
│   └── documento_prueba.pdf # Documento de ejemplo con contenido sobre RAG
├── chroma_db/              # Base de datos vectorial (generada automáticamente)
└── venv/                   # Entorno virtual de Python
```

## Comandos Útiles de Ollama

```bash
# Listar modelos instalados
ollama list

# Ejecutar un modelo interactivamente
ollama run qwen2.5:7b

# Actualizar un modelo
ollama pull qwen2.5:7b

# Eliminar un modelo
ollama rm qwen2.5:7b

# Ver información del sistema
ollama ps
```

## Solución de Problemas

### Ollama no se conecta

```bash
# Verificar que Ollama esté ejecutándose
ps aux | grep ollama

# Reiniciar el servicio
ollama serve
```

### Error de memoria insuficiente

- Asegúrate de tener al menos 8GB de RAM disponible
- Considera usar un modelo más pequeño si tienes limitaciones de memoria

### Problemas con ChromaDB

```bash
# Eliminar la base de datos y permitir que se regenere
rm -rf chroma_db/
```

### Dependencias de Python

```bash
# Si hay conflictos, reinstalar en un entorno limpio
deactivate
rm -rf venv/
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Personalización

### Cambiar el Modelo

Edita `rag_local.py` y cambia el nombre del modelo en la configuración de `ChatOllama`.

### Procesar Diferentes PDFs

Cambia la variable `PDF_FILENAME` en `rag_local.py` para procesar diferentes documentos.

### Ajustar Parámetros de Embedding

Modifica los parámetros de `RecursiveCharacterTextSplitter` para diferentes tamaños de chunk.

## Contribuir

1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -am 'Agregar nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Crea un Pull Request

## Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## Referencias

- [Ollama Documentation](https://ollama.ai/docs)
- [LangChain Documentation](https://python.langchain.com/)
- [ChromaDB Documentation](https://docs.trychroma.com/)
- [Qwen Model Information](https://huggingface.co/Qwen)
