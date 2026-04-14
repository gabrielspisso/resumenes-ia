# 09 — PNL: Procesamiento del Lenguaje Natural

> **Playlist:** PNL  
> Fuente: Para el Coloquio, Resumenes IA Final

---

## ¿Qué es el PNL?

Rama de la IA que se enfoca en la **interacción entre computadoras y el lenguaje humano**. Comparte territorio con ML y Deep Learning.

**Aplicaciones:** análisis de sentimientos, traducción automática, extracción de información, generación de lenguaje, respuesta a preguntas, clasificación de textos.

---

## Tipos de Lenguaje

| Tipo | Descripción | ¿Requiere IA? |
|------|-------------|--------------|
| **Artificial** (programación, técnico, científico) | Normas estrictas, sintaxis predecible | **No** — se procesa sin IA |
| **Natural** (humano, hablado/escrito) | Ambiguo, dependiente del contexto | **Sí** |

---

## Áreas de Lingüística Relevantes

| Área | Estudia |
|------|---------|
| **Fonología** | Sonidos, entonación, acentuación |
| **Morfología** | Estructura de palabras y morfemas |
| **Sintaxis** | Estructura de oraciones y reglas gramaticales |
| **Semántica** | Significado de palabras, frases y oraciones |

---

## Orientaciones del PNL

| Orientación | Sigla | Qué hace |
|------------|-------|---------|
| **Comprensión del Lenguaje Natural** | NLU | Análisis sintáctico y semántico para entender el significado |
| **Generación del Lenguaje Natural** | NLG | Genera texto completo a partir de una entrada |

---

## Pipeline de Procesamiento de Texto

### 1. Tokenización

Divide el texto en unidades básicas llamadas **tokens** (palabras, frases, caracteres).

**Para qué sirve:** facilita el análisis, permite indexación y búsqueda eficiente, estandariza el texto, mejora el rendimiento del modelo.

### 2. Normalización

Convierte distintas formas de palabras a una forma estándar.

| Técnica | Descripción | Ejemplo |
|---------|-------------|---------|
| **Lematización** | Reduce al **lema** (forma base en el diccionario; semántica) | "corriendo", "corrió" → "correr" |
| **Stemming** | Reduce a la **raíz** (núcleo morfológico; no siempre es palabra válida) | "corriendo", "corrió" → "corr" |
| **Minúsculas** | Todo a minúsculas | "Hola" → "hola" |
| **Eliminar puntuación** | Quitar símbolos que no aportan | "hola!" → "hola" |

**Para qué sirve:** reducir variabilidad, mejorar precisión del modelo.

### 3. Segmentación

Agrupa tokens en unidades de nivel superior: oraciones, párrafos.

**Para qué sirve:** mejorar comprensión, facilitar procesamiento por oraciones completas.

---

## Técnicas Complementarias

### Categorización (Part-of-Speech Tagging — PoS)

Asigna etiquetas gramaticales a cada token.

| Tipo | Categorías | Característica |
|------|-----------|---------------|
| **Open Classes (léxicas)** | Sustantivos, adjetivos, verbos, adverbios | En constante cambio; pueden surgir nuevas palabras |
| **Closed Classes (funcionales)** | Pronombres, preposiciones, conjunciones, interjecciones | Fijas; no surgen nuevas palabras de estos tipos |

### Autocorrección

**Objetivo:** transformar palabras mal escritas en sus versiones correctas.

**Proceso:**
1. Identificar que la palabra no está en el vocabulario
2. Buscar palabras cercanas usando **distancia de edición** (ej: Levenshtein)
3. Sustituir por las palabras a esa distancia
4. Seleccionar la de mayor probabilidad según el contexto

### Autocompletado

**Objetivo:** predecir la siguiente palabra mientras el usuario escribe.

**Proceso:**
1. Recopilar corpus de lenguaje
2. Aprender probabilidades de secuencias
3. Dado el contexto (últimas n palabras) → predecir la siguiente
4. Mostrar sugerencias al usuario

**Modelo básico:** **n-gram** (considera las últimas n palabras para predecir)

---

## NLP Tradicional vs NLP con ML

### NLP Tradicional

**Enfoque:** combinación de ciencias de la computación + lingüística, con reglas y métodos estadísticos básicos.

**Ventajas:** simple y transparente, pocos datos, pocos recursos computacionales, fácil de mantener.

**Limitaciones:**
1. Ambigüedad léxica y estructural
2. Dependencia entre palabras (contexto)
3. Falta de contexto semántico

### NLP con ML

**Representación del texto:**

| Técnica | Qué hace |
|---------|---------|
| **TF-IDF** | Vector numérico que considera la importancia de una palabra en el corpus |
| **GloVe** | Vector con relaciones semánticas y sintácticas por co-ocurrencia |

**Modelos:**

| Tipo | Algoritmos | Ejemplo de uso |
|------|-----------|---------------|
| **Regresión** | Regresión lineal, Regresión logística | Predicción de calificación, clasificación positivo/negativo |
| **Árboles** | Árbol de decisión, Random Forest | Clasificación de sentimientos, noticias |
| **Clustering** | K-Means, DBSCAN | Descubrir tópicos, análisis de comentarios |

**Tareas de NLU:**
- Análisis semántico y sintáctico
- Análisis de sentimiento
- Extracción de información

**Tareas de NLG:**
- Generación automática de texto
- Personalización de contenido
- Informes y resúmenes automáticos
- Control de estilo y tono

---

## Resumen clave

1. PNL = IA + lingüística para que las máquinas entiendan y generen lenguaje humano
2. **Lenguaje artificial** → no necesita IA; **Lenguaje natural** → sí necesita IA
3. Pipeline básico: **Tokenización → Normalización → Segmentación**
4. **Lematización** → forma base semántica ("correr"); **Stemming** → raíz morfológica ("corr")
5. **NLU:** comprende texto; **NLG:** genera texto
6. **Autocorrección** usa distancia de edición (Levenshtein)
7. **Autocompletado** usa modelos n-gram
8. NLP tradicional: simple pero limitado. NLP con ML: usa TF-IDF/GloVe + modelos

---

## Trampas del examen

- El lenguaje **artificial** (programación, etc.) NO necesita IA para procesarse
- **Lematización ≠ Stemming:** la lematización da formas semánticas válidas; el stemming da raíces que pueden no ser palabras
- **NLU:** comprensión (análisis, clasificación); **NLG:** generación (texto, resúmenes)
- **Open Classes:** pueden surgir nuevas palabras (sustantivos nuevos, nuevos verbos)
- **Closed Classes:** no surgen nuevas palabras (siempre las mismas preposiciones/conjunciones)
- El autocompletado usa **modelos n-gram** (no distancia de edición — eso es la autocorrección)
