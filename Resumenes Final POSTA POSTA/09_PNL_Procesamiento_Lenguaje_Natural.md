# 09 — PNL: Procesamiento del Lenguaje Natural

> **Playlist:** PNL  
> **Objetivo:** Permitir a las máquinas comprender, interpretar y generar lenguaje humano.

---

## ¿Qué es el PNL?

Rama de la IA que se enfoca en la **interacción entre computadoras y el lenguaje humano**. Comparte territorio con ML y Deep Learning.

**Aplicaciones principales:**
- Análisis de sentimientos
- Traducción automática
- Extracción de información
- Generación de lenguaje natural
- Respuesta a preguntas, clasificación de textos

---

## Tipos de Lenguaje

| Tipo | Descripción | ¿Requiere SI? |
|------|-------------|--------------|
| **Artificial** (prog., técnico, científico) | Normas estrictas, sintaxis predecible | **No** (se procesa sin IA) |
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
| **Comprensión del lenguaje natural** | NLU | Análisis sintáctico y semántico para entender el significado |
| **Generación del lenguaje natural** | NLG | Genera texto completo a partir de una entrada |

---

## Pipeline de Procesamiento de Texto

### 1. Tokenización
Divide el texto en unidades básicas llamadas **tokens** (palabras, frases, caracteres).

**Para qué sirve:**
- Facilita el análisis
- Permite indexación y búsqueda eficiente
- Estandariza el texto
- Mejora el rendimiento del modelo

### 2. Normalización
Convierte distintas formas de palabras a una forma estándar.

**Técnicas:**

| Técnica | Descripción | Ejemplo |
|---------|-------------|---------|
| **Lematización** | Reduce al lema (forma base en el diccionario) | "corriendo", "corrió" → "correr" |
| **Stemming** | Reduce a la raíz (núcleo del significado) | "corriendo", "corrió" → "corr" |
| **Minúsculas** | Todo a minúsculas | "Hola" → "hola" |
| **Eliminar puntuación** | Quitar símbolos que no aportan al análisis | "hola!" → "hola" |

**Para qué sirve:** reducir variabilidad, mejorar la precisión del modelo.

### 3. Segmentación
Agrupa tokens en unidades de nivel superior: oraciones, párrafos.

**Para qué sirve:** mejorar la comprensión, mayor eficiencia, facilitar el procesamiento por oraciones completas.

---

## Técnicas Complementarias

### Categorización (Part-of-Speech Tagging)
Asigna etiquetas gramaticales a cada token.

**Categorías léxicas (Open Classes):** sustantivos, adjetivos, verbos, adverbios  
*(en constante cambio, pueden surgir nuevas palabras)*

**Categorías funcionales (Closed Classes):** pronombres, preposiciones, conjunciones, interjecciones  
*(no surgen nuevas palabras de estos tipos)*

### Autocorrección
**Objetivo:** transformar palabras mal escritas en sus versiones correctas.

**Funcionamiento:**
1. Identificar que la palabra no está en el vocabulario
2. Buscar palabras cercanas usando **distancia de edición** (ej: Levenshtein)
3. Sustituir por las palabras a distancia determinada
4. Seleccionar la de mayor probabilidad según el contexto

### Autocompletado
**Objetivo:** predecir la siguiente palabra mientras el usuario escribe.

**Funcionamiento:**
1. Recopilación de datos (corpus de lenguaje)
2. Modelado del lenguaje (aprender probabilidades de secuencias)
3. Predicción: dado el contexto (últimas n palabras) → predecir siguiente
4. Sugerencias al usuario

**Modelo básico:** n-gram (modelo que considera las últimas n palabras)

---

## NLP Tradicional vs NLP con ML

### NLP Tradicional
**Enfoque:** combinación de ciencias de la computación + lingüística, con reglas y métodos estadísticos básicos.

**Ventajas:**
- Simple y transparente
- Pocos datos de entrenamiento
- Pocos recursos computacionales
- Fácil de implementar y mantener

**Limitaciones:**
1. Ambigüedad léxica y estructural
2. Dependencia entre palabras
3. Falta de contexto

### NLP con ML (sin Deep Learning)

**Representación de texto:**

| Técnica | Qué hace |
|---------|---------|
| **TF-IDF** | Vector numérico considerando importancia de una palabra en el corpus |
| **GloVe** | Vector con relaciones semánticas/sintácticas por co-ocurrencia |

**Modelos:**

| Tipo | Algoritmos | Ejemplo de uso |
|------|-----------|---------------|
| **Regresión** | Regresión lineal, Regresión logística | Predicción de calificación, clasificación positivo/negativo |
| **Árboles** | Árbol de decisión, Random Forest | Clasificación de sentimientos, clasificación de noticias |
| **Clustering** | K-Means, DBSCAN | Descubrir tópicos, análisis de comentarios |

**Tareas de comprensión (NLU):**
- Análisis semántico y sintáctico
- Análisis de sentimiento
- Extracción de información

**Tareas de generación (NLG):**
- Generación automática de texto
- Personalización de contenido
- Informes / resúmenes
- Control de estilo y tono

---

## Resumen clave para el final

1. PNL = IA + lingüística para que las máquinas entiendan y generen lenguaje humano.
2. **Lenguaje artificial** no necesita IA para procesarse; **lenguaje natural** sí.
3. Pipeline básico: **Tokenización → Normalización → Segmentación**.
4. **Lematización** → forma base (semántica); **Stemming** → raíz (morfología).
5. **NLU:** comprende texto; **NLG:** genera texto.
6. **Autocorrección** usa distancia de edición (Levenshtein); **Autocompletado** usa modelos n-gram.
7. NLP tradicional: simple pero limitado en ambigüedad y contexto.
8. NLP con ML: usa TF-IDF/GloVe para vectorizar, luego regresión/árboles/clustering.
