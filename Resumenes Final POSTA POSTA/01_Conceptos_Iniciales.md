# 01 — Conceptos Iniciales de IA

> **Playlist:** Conceptos Iniciales  
> **Objetivo:** Entender qué es la IA, qué son los Sistemas Inteligentes, y cómo funciona el Machine Learning básico.

---

## 1. ¿Qué es la Inteligencia Artificial?

**Definición:** Rama de las ciencias computacionales que estudia modelos de cómputo (tecnologías, arquitecturas) para desarrollar software capaz de realizar actividades propias de los seres humanos relacionadas con:
- Razonamiento
- Conducta
- Aprendizaje

**Nota importante:** La IA en esta materia se enfoca en **software y computación**, no en robots (que son conceptos de mecánica y electrónica). El objetivo es desarrollar software que **se mejore con el uso** y que pueda aprender automáticamente.

**Disciplinas que comprende:**
- IA Tradicional (reglas, métodos heurísticos, lógica)
- Inteligencia Computacional (inspiración biológica)
- Machine Learning (Aprendizaje Automático)
- Visión Artificial
- Procesamiento del Lenguaje Natural
- Big Data & Data Mining

**Pirámide de la Información:**
El software tradicional maneja *datos* para obtener *información*. Los sistemas inteligentes llegan más lejos: transaccionan con *conocimiento* (datos con significado y utilidad) para descubrir *patrones ocultos* en los datos, como un iceberg donde no nos quedamos en la punta (datos) sino exploramos las profundidades.

---

## 2. Problemas donde se aplica la IA

Los sistemas inteligentes se usan en **dominios complejos** que cumplen una o más de estas características:

- **El problema no se entiende completamente:** No sabemos bien qué lo causa, pero necesitamos intentar resolverlo.
- **No se pueden anticipar todas las situaciones futuras:** Hay cambios en el dominio que el sistema debe adaptarse.
- **Posibles soluciones demasiado numerosas:** No es posible búsqueda exhaustiva; se necesitan métodos heurísticos que acoten el espacio de búsqueda.
- **Modelado tradicional requiere simplificación perjudicial:** Al programar la solución, tendríamos que descartar demasiados detalles, volviendo la solución inútil.

---

## 3. Sistemas Inteligentes (SI)

**Definición:** Artefactos con **comportamiento inteligente**, que implica:

- **Racional:** Toma decisiones consistentes con su objetivo (no hace cualquier cosa).
- **No omnisciente:** No posee todos los conocimientos ni datos disponibles.
- **No infalible:** No siempre es exitoso; puede dar soluciones satisfactorias pero no perfectas.
- **Puede aprender:** Mejora su desempeño durante su uso.
- **Flexible y robusto:** Soporta cambios del dominio y se adapta a situaciones no previstas.

**Tipos de IA:**
- **IA Débil:** Lo que desarrollamos nosotros. Emula ciertas características de los seres humanos pero **nunca emula todas** las capacidades humanas.
- **IA Fuerte:** Hipotética IA que emularía completamente la inteligencia humana (no es tema de esta materia).

---

## 4. Tipos de Sistemas Inteligentes

### Por fuente de conocimiento:

| Fuente | Tipo | Características |
|--------|------|-----------------|
| **Pública** (libros, manuales, datos digitales, web) | Sistema Inteligente (SI) | Usa solo fuentes públicas explícitas |
| **Privada** (mente del experto) | Sistema Experto (SE) | Captura conocimiento de un experto humano |

> **Regla clave:** Un SI no siempre es un SE, pero un SE **siempre** es un SI. Los SE son un subconjunto de los SI.

**Nota:** Los SE pueden combinar fuentes públicas y privadas, pero lo que los distingue es la inclusión de conocimiento experto.

### Por tecnología:

| Familia | Ejemplos de tecnologías |
|---------|----------|
| **IA Tradicional** | SBC, SET, Lógica Difusa |
| **Machine Learning** | Inducción, Regresión, RNA, Lógica Difusa |
| **Inteligencia Computacional** | RNA, Algoritmos Genéticos, Inteligencia de enjambre |

**Importante:** Las clasificaciones **se solapan**. No es "o esto o lo otro", sino que hay relaciones y combinaciones posibles. Por ejemplo, un algoritmo de inducción puede generar reglas usables en un SE tradicional.

---

## 5. IA Tradicional vs Inteligencia Computacional

### Sistema Basado en Conocimientos (SBC)
- **Fuentes:** Públicas
- **Componentes principales:**
  - Base de conocimientos (hechos + reglas explícitas)
  - Motor de inferencias (aplica métodos de búsqueda)
  - Interfaz E/S
- **Ventaja:** Muy simple de implementar y modificar.

### Sistema Experto Tradicional (SET)
- **Fuentes:** Privadas (+ puede usar públicas)
- **Componentes adicionales:**
  - **Base de datos:** Almacena datos del problema actual (temporal/específico del caso).
  - **Memoria de trabajo:** Registra la traza completa del razonamiento (como un log).
  - **Trazador de explicaciones:** Justifica el resultado al usuario (emula cómo un experto explicaría sus decisiones).
  - **Trazador de consultas:** Pide información adicional al usuario cuando el motor la necesita y explica por qué.
  - **Manejador de comunicaciones:** Interfaz mejorada de E/S.

**Nota:** El SET es más complejo que el SBC porque necesita emular comportamientos adicionales del experto humano (explicar, consultar, justificar).

### Inteligencia Computacional
- **Inspiración:** Biológica
- **Ejemplos:** Redes Neuronales Artificiales (cerebro), Algoritmos Genéticos (evolución), Inteligencia de Enjambre (comportamiento animal grupal), Sistemas Inmunológicos Artificiales.

---

## 6. Machine Learning (ML)

**Definición:** Campo de la computación que genera software capaz de, **automáticamente**, adquirir capacidades y adaptarse a su entorno a través del aprendizaje con datos.

**Flujo fundamental:**
```
Datos → Algoritmo → Modelo (implementado en software)
```

**Analógía útil (del profesor):** Machine Learning es como *cultivar una planta*:
- La **semilla** = algoritmo
- La **tierra y maceta** = ambiente de entrenamiento
- El **agua** = datos (cantidad correcta, no demasiado ni demasiado poco)
- La **planta resultante** = modelo
- Si descuidamos el riego o damos datos no representativos, la planta "se marchita" y el modelo no sirve.

### Estrategias de aprendizaje:

| Estrategia | Descripción | Ejemplo |
|-----------|-------------|---------|
| **Supervisado** | Se dan ejemplos + salida deseada. El algoritmo aprende la relación entre entrada y salida. | Clasificar flores iris según pétalo/sépalo: darle ejemplos con sus etiquetas (setosa, versicolor, virginica) |
| **No supervisado** | Solo ejemplos de entrada. El algoritmo agrupa por similitud sin indicar cómo agrupar. | Clasificar automáticamente vestidos por temporada, talla, precio: el algoritmo decide qué criterios son relevantes |

**Observación:** Estos no compiten por el mismo tipo de problemas. El supervisor es para cuando sabemos qué queremos clasificar; el no supervisado para descubrir patrones desconocidos.

### Tipos de entrenamiento:

| Tipo | Descripción |
|------|-------------|
| **Offline (estático)** | Aprende solo durante entrenamiento; en producción no aprende más. Modelo fijo y determinista. |
| **Online (dinámico)** | Sigue aprendiendo en producción (requiere monitoreo cuidadoso para no olvidar ni divergir). |

### Tipos de algoritmos de ML:

- **Clustering** – Agrupa datos por similitud
- **Inducción** ← importante para el final
- **Regresión** ← importante para el final
- **Basados en Bayes** – Usan probabilidad
- **Redes Neuronales Artificiales** – Inspiración biológica
- (Miles de variantes más)

---

## 7. Algoritmos de Inducción (TDIDT)

**Tipo:** Supervisado + Offline. Identifica reglas de clasificación a partir de una tabla de ejemplos.

**Estructura de datos requerida:**
- **Filas** = ejemplos
- **Columnas** = atributos (características de entrada)
- **Atributo objetivo** = lo que se quiere predecir (único, siempre al final)

**Las reglas generadas tienen:**
- **Antecedente:** Condiciones sobre atributos de entrada
- **Consecuente:** Valor del atributo objetivo

### Algoritmo TDIDT (Top-Down Induction Decision Trees)

Genera árboles de decisión mediante **divide y vencerás**:

```
A partir de un conjunto T de ejemplos:

1. Si T está vacío → finalizar (no hay más ejemplos)

2. Si todos los ejemplos tienen el MISMO valor 
   en atributo objetivo → generar nodo hoja con ese valor
   (genera una regla IF-THEN)

3. Si no se cumplen 1 ni 2:
   a. Seleccionar atributo con mayor GANANCIA DE INFORMACIÓN en T
   b. Particionar T en subconjuntos por cada valor del atributo
   c. Aplicar recursivamente este procedimiento a cada partición
```

**Resultado:** Árbol de decisión → Conjunto de reglas IF-THEN-ELSE

**Ganancia de Información:**

La ganancia se calcula usando **entropía** (concepto de la teoría de la información que mide la "sorpresa" o relevancia de un dato):

$$\text{Ganancia}(atributo) = \text{Entropía}(objetivo) - \text{Entropía}(objetivo | atributo)$$

El atributo que **mayor ganancia** proporciona es el que mejor divide el conjunto de datos para clasificación.

**Ejemplo práctico:** Para decidir si usar Machine Learning en un problema, el algoritmo podría seleccionar primero "tipo de problema" si ese atributo maximiza la ganancia de información, luego dentro de cada tipo selecciona "tipo de datos", etc.

**Casos especiales:** Si al final nos quedan ejemplos con valores conflictivos en el objetivo (ej: 50% sí, 50% no), la regla generada no será confiable (50/50 de acierto) y deberemos obtener más datos.

---

## 8. Algoritmos de Regresión

**Tipo:** Supervisado. A partir de una tabla, identifica una **fórmula matemática** que describe la relación entre atributos de entrada y el atributo objetivo.

**Requisito fundamental:** Todos los atributos (entrada y salida) deben tener **valores numéricos continuos**. Si no los tienen, deben transformarse previamente.

**Proceso:**
1. El algoritmo prueba distintos tipos de fórmulas (lineal, polinomial, exponencial, etc.)
2. Ajusta los coeficientes para **minimizar el error** (diferencia entre valor real y estimado)
3. Retorna la mejor fórmula encontrada

**Funcionamiento:** Similar al procedimiento de Taylor en análisis matemático, pero automatizado. El algoritmo calcula iterativamente qué coeficientes minimizan el error de forma óptima.

**Ejemplo:** A partir de datos de velocidad, aceleración y tiempo con distancias conocidas, puede descubrir la fórmula de cinemática de Newton: $d = v_0 \cdot t + \frac{1}{2} a \cdot t^2$

**Aplicaciones:** Predicción de ventas, stocks, comportamientos continuos, etc.

---

## 9. Procesos de construcción de modelos ML

Para generar un modelo confiable, se requieren **tres procesos paralelos y secuenciales**:

### Los tres procesos:

| Proceso | Cuándo | Qué evalúa |
|---------|--------|-----------|
| **Entrenamiento** | Fase 1 | Aprende los valores del modelo a partir de ejemplos |
| **Validación** | En paralelo con entrenamiento | Evalúa distintos parámetros en tiempo real para optimizar (usa datos diferentes del entrenamiento) |
| **Prueba (Testing)** | Fase final | Evalúa la capacidad de **generalización** del modelo final (usa datos nuevos, nunca vistos) |

### División de datos - **CRÍTICO:**

Necesitas **tres conjuntos de datos distintos**:
- **Entrenamiento:** La mayoría (~70-80%) → genera el modelo
- **Validación:** Pequeña porción (~10%) → optimiza durante el entrenamiento
- **Prueba:** Porción media (~10-20%) → evalúa desempeño final

**¿Por qué separar?** Como un profesor que enseña un tema, practica ejemplos con los alumnos durante la clase, pero en el examen da problemas nuevos para verificar si realmente aprendieron a generalizar (no solo memorizar los ejercicios practicados).

Si pruebas con los mismos datos de entrenamiento, **no sabes si generaliza** y fallarás en producción.

### Parametrización:

El ingeniero **no implementa** el algoritmo (ya existe), pero debe **ajustar parámetros** que el algoritmo define. Algunos parámetros tienen gran impacto en la calidad del modelo, otros poco. Esto requiere experiencia y análisis.

### Evaluación de aprendizaje:

El ingeniero debe verificar si el modelo aprendió bien:
- **Buen aprendizaje:** El modelo se comporta similar al problema real en datos nuevos.
- **Sobreentrenamiento (Overfitting):** El modelo memoriza los datos de entrenamiento pero no generaliza; falla con datos nuevos.

Por eso necesitamos validación y prueba en paralelo.

---

## 10. Métricas de evaluación

### Para salidas discretas (Clasificación):

#### Matriz de Confusión

Tabla que muestra cómo de bien el modelo clasifica:

|  | Clase Real: Sí | Clase Real: No |
|---|---|---|
| **Predice: Sí** | Verdadero Positivo (VP) | Falso Positivo (FP) |
| **Predice: No** | Falso Negativo (FN) | Verdadero Negativo (VN) |

**Interpretación ideal:** Todos los valores en la diagonal (el modelo siempre acierta).

#### Métricas derivadas:

| Métrica | Fórmula | Qué mide |
|---------|---------|---------|
| **Exactitud (Accuracy)** | (VP+VN)/(VP+FP+VN+FN) | Proporción general de aciertos |
| **Precisión** | VP/(FP+VP) | De los que predije "sí", ¿cuántos lo eran realmente? (evita falsos positivos) |
| **Recuperación (Recall)** | VP/(VP+FN) | De los "sí" reales, ¿cuántos identifiqué? (evita falsos negativos) |
| **F1 Score** | 2*(P*R)/(P+R) | Balance armónico entre precisión y recuperación |

#### Consideraciones importantes:

> **Atención crítica:** Buena exactitud ≠ modelo confiable, especialmente con **clases desbalanceadas** (ej: 91 "no" vs 9 "sí").

**Ejemplo de desbalance:**
- Exactitud: 91% (suena bien)
- Precisión: 50% (coincidia con una moneda)
- Recuperación: 11% (identifica solo 1 de 9 casos reales)

→ El modelo es malo, pero la exactitud lo oculta.

**Tradeoff:** Mejorar precisión suele perjudicar recall y viceversa. El F1 Score balancea ambas.

**Soluciones para datos desbalanceados:**
- Balancear los datos en la preparación
- Usar métricas más robustas (F1, no solo exactitud)
- Elegir algoritmos que manejen bien datos desbalanceados

---

### Para salidas continuas (Regresión):

| Métrica | Significado |
|---------|------------|
| **Error Absoluto** | \|valor_real - valor_estimado\| → Error puro |
| **Error Relativo** | Error Absoluto / valor_real → Error como % |

**Interpretación:** Cuanto menores → mejor el modelo.

**Consideraciones:**
- Error absoluto es mejor para valores grandes (impacto real)
- Error relativo es mejor para valores pequeños (proporcionalidad)
- Necesitas evaluar ambos según el contexto
- Computa resumen estadístico: mínimo, máximo, promedio, desviación estándar

**Ejemplo extremo:**
- Quería: 10, obtuve: 10.01 → Error abs: 0.01, Error rel: 0.1% ✓ Excelente
- Quería: 38, obtuve: 10.35 → Error abs: 27.65, Error rel: 72% ✗ Muy malo
- Quería: 0, obtuve: 0.55 → Error abs: 0.55 (pequeño), Error rel: 5.500.000% (enorme) → Analizar contexto
- Quería: 15.000, obtuve: 18.200 → Error abs: 3.200, Error rel: 2% → Para números grandes, el relativo es más informativo

---

## Resumen clave para el final

1. **IA** estudia cómo construir software que razone, actúe y aprenda usando modelos de cómputo.

2. **Sistema Inteligente (SI):** Artefacto con comportamiento inteligente, racional, no omnisciente, no infalible, que aprende y se adapta.
   - **Sistema Experto (SE):** Subcategoría de SI que emula parcialmente a un experto humano.

3. **ML (Aprendizaje Automático):** Datos → Algoritmo → Modelo. Puede ser:
   - **Supervisado** (con etiquetas) o **No supervisado** (sin etiquetas)
   - **Offline** (aprendizaje fijo) u **Online** (aprendizaje continuo)

4. **TDIDT** (Inducción): Genera árboles de decisión → reglas IF-THEN por ganancia de información (divide y vencerás).

5. **Regresión:** Encuentra fórmula numérica que describe relación entre atributos (todos deben ser números).

6. **Procesos ML:** Siempre necesitas 3 conjuntos de datos (entrenamiento, validación, prueba) separados.
   - Entrenamiento genera el modelo
   - Validación optimiza parámetros en paralelo
   - Prueba verifica que generaliza (datos nunca vistos)

7. **Métricas discretas:** Exactitud + Precisión + Recuperación (F1 Score las balancea)
   - El F1 Score es esencial con datos desbalanceados

8. **Métricas continuas:** Error absoluto + Error relativo (contextodependiente cuál usar)

9. **Clave:** Siempre evalúa en datos de prueba diferentes a entrenamiento, sino no sabes si generaliza.

---

## 📝 Cambios respecto al original

### Agregados de las transcripciones:

1. **Sección 1 mejorada:**
   - Aclaración de que la IA enfocada aquí es software, no robots
   - Concepto de la Pirámide de la Información (datos vs conocimiento vs sabiduría)
   - Analogía del iceberg

2. **Nueva Sección 2:**
   - Detalles específicos de cuándo aplicar IA (problemas complejos)

3. **Sección 3 mejorada:**
   - Distinción clara entre IA Débil e IA Fuerte
   - Aclaración de que nuestros sistemas nunca emulan TODAS las capacidades humanas

4. **Sección 4 mejorada:**
   - Notas sobre combinación de fuentes en SE
   - Aclaración del solapamiento entre tecnologías

5. **Sección 5 mejorada:**
   - Ventajas del SBC
   - Mayor detalle de componentes del SET (memoria de trabajo, trazadores)
   - Ejemplos de inspiración biológica

6. **Sección 6 ampliada:**
   - Analogía de la planta (del profesor)
   - Explicación más completa de estrategias supervisadas/no supervisadas
   - Ejemplos concretos (flores iris, vestidos)

7. **Sección 7 ampliada:**
   - Explicación de ganancia de información y entropía
   - Casos especiales (datos conflictivos)
   - Contexto de uso en otras tecnologías

8. **Sección 8 ampliada:**
   - Comparación con procedimiento de Taylor
   - Ejemplo real: cinemática de Newton

9. **Sección 9 completamente reescrita:**
   - Los 3 procesos (entrenamiento, validación, prueba) con más detalle
   - Analogía del profesor y examen
   - Importancia de separar datos
   - Explicación del overfitting

10. **Sección 10 ampliada:**
    - Matriz de confusión visual completa
    - Ejemplo de desbalance de clases real
    - Tradeoff precisión/recall
    - Ejemplos específicos de error en regresión
    - Contexto para interpretar errores

11. **General:**
    - Mejor estructura con ejemplos concretos
    - Notas de advertencia donde es importante
    - Clarificaciones de conceptos confusos
    - Mayor énfasis en aplicabilidad práctica
