# 📊 Diffs — Resumenes Final POSTA POSTA vs Resumenes IA Final

> Este archivo documenta los cambios y mejoras incorporadas en cada resumen respecto a la versión original.
> Los nuevos resúmenes fueron generados combinando los resúmenes previos + **transcripciones completas de las clases del profesor** (procesadas con Whisper).

---

## 01 — Conceptos Iniciales

**Transcripciones usadas:** `IA - Conceptos Iniciales` (5 videos) + `IA - Introducción a la Inteligencia Artificial` (5 videos)

### Agregado / Mejorado:
- **IA Débil vs Fuerte**: distinción clara que faltaba en el original, con explicación de por qué los SI de la materia son IA débil
- **Pirámide de la Información**: nueva sección (datos → información → conocimiento → sabiduría) con ejemplos
- **Características de problemas aptos para IA**: 4 características concretas que hacen a un problema candidato para IA
- **Solapamiento de tecnologías**: aclaración del diagrama de Venn IA/ML/DL y por qué los límites son difusos
- **Algoritmos de Inducción (ampliado)**: ganancia de información, entropía, casos especiales (solo una clase, nodo puro)
- **Proceso ML completo**: analogía del profesor-examen, importancia de separación train/test, overfitting explicado en detalle
- **Métricas (ampliadas)**: ejemplo real del problema de clases desbalanceadas (91% exactitud pero modelo inútil), tradeoff precisión/recall, ejemplos de RMSE/MAE contextualizados
- **Ejemplos del profesor**: analogía de la planta (algoritmo = semilla, datos = agua), ejercicio de caracteres chinos para supervisado/no supervisado, física (cinemática de Newton) como regresión

---

## 02 — Análisis de Protocolos

**Transcripciones usadas:** `IA - Análisis de Protocolos` (4 videos)

### Agregado / Mejorado:
- **Contexto histórico**: origen en Ericsson (1993) y psicología cognitiva
- **Etapa de Grabación (detallada)**: rol preciso del Ingeniero del Conocimiento, instrucciones exactas al experto, ejemplo médico completo
- **Segmentación**: aclaración de que no hay forma "correcta única" y que distintos ICs pueden segmentar diferente
- **Anotaciones**: explicación de por qué son críticas (libros consultados, búsquedas, silencios, gestos)
- **Tabla CCV ampliada**: ejemplo completo con el caso especial del mareo (concepto vs característica) que estaba ausente
- **Estados — dos visiones**: presentación de la visión concepto vs visión valor con necesidad de consistencia interna
- **Diagrama de flujo de estados**: visualización gráfica del flujo de operadores y estados
- **Metacomentarios e incertidumbres**: tablas mejoradas con explicación de su utilidad futura
- **Interpretación — atomicidad**: contexto sobre atomicidad de reglas y por qué no hay subsunción en esta etapa
- **Iteración del proceso**: aclaración de que un único protocolo es apenas el inicio del proceso

---

## 03 — Algoritmos Genéticos

**Transcripciones usadas:** `IA - Algoritmos Genéticos` (7 videos: 5 teóricos + 2 de práctica)

### Agregado / Mejorado:
- **Historia y contexto**: Darwin, postulados evolutivos y cómo inspiran el algoritmo
- **Cuándo usar AG**: espacios exponenciales, comparación con métodos clásicos, concepto de "navegación en sabana de soluciones"
- **Convergencia prematura**: explicación del problema y técnicas para evitarlo
- **Métodos de selección (ampliados)**: ventajas y desventajas específicas de cada método + tabla comparativa
- **Control s/nro. Esperado**: pasos detallados con valores numéricos concretos
- **Mutación adaptativa**: método por desvío estándar (completamente nuevo)
- **Cromosomas compuestos**: distinción entre genes y posiciones, modelado de problemas complejos
- **Problema del Pesecito**: caso concreto del zebra puzzle con modelado de cromosoma compuesto
- **Sistema de Guardias Médicas**: caso real de implementación con parámetros específicos (100 individuos, 1000 iteraciones, tiempos de 7-93 segundos)
- **Patrones de implementación**: enfoque OO, interfaces, framework imperativo vs declarativo
- **Parámetros prácticos**: salto generacional 0.5, máximo 1000 vueltas, ejemplos de convergencia (-200 → -4 → 0 errores)

---

## 04 — Redes Neuronales Artificiales

**Transcripciones usadas:** `transcripciones RNA` (15 videos)
**Base:** `04_Redes_Neuronales_v2.md` (la versión más completa)

### Agregado / Mejorado:
- **Datos cuantitativos del cerebro**: cantidad de neuronas, conexiones sinápticas, velocidad de procesamiento
- **Contexto histórico ampliado**: Perceptrón abandonado en años 60, renacimiento con backprop en los 80, CNN en 2012, Google en 2014
- **Vanishing Gradient Problem**: explicación detallada y por qué limita las redes profundas
- **Diseño de topología automático**: Algoritmos Genéticos para arquitectura, AutoKeras
- **La "regla dorada del ML"**: sobre normalización, explicada con énfasis del profesor
- **Postulado de Hebb**: explicación formal + memoria asociativa con ejemplos prácticos
- **Catástrofe de interferencia**: problema de aprendizaje continuo, por qué las RNA olvidan
- **Cross-entropy y Shannon**: conexión entre entropía de información y función de pérdida
- **Tabla comparativa de optimizadores**: velocidad, memoria, casos de uso de SGD, Adam, RMSProp, etc.
- **Debugging cuando la red no aprende**: pasos ordenados de diagnóstico (nuevo)
- **Data augmentation**: técnicas, casos de uso, organización de imágenes
- **Early stopping — limitaciones**: cuándo funciona y cuándo puede ser contraproducente
- **Distinción step/época/ciclo**: aclaración de terminología que genera confusión

---

## 05 — Emparrillado

**Transcripciones usadas:** `IA - Emparrillado` (3 videos)

### Agregado / Mejorado:
- **Contexto histórico**: origen en 1955 y uso original en psicología clínica (George Kelly)
- **Ejemplo concreto consistente**: dominio médico con virus respiratorios (COVID-19, MERS-CoV, SARS-CoV, 229E) y síntomas específicos
- **Procedimiento numérico detallado**: cálculo paso a paso de matrices de distancias con valores concretos
- **Parrilla opuesta**: su rol en el cálculo de características, que no estaba explicado
- **Dendrogramas mejorados**: visualización más clara y estructurada
- **Análisis de relaciones entre características**: ejemplo práctico de cómo interpretar relaciones (paralela, recíproca, ortogonal, ambigua, no tipificada)
- **Limitaciones explícitas**: énfasis en que la técnica no es útil por sí sola y requiere validación con el experto

---

## 06 — Métodos de Búsqueda

**Transcripciones usadas:** `IA - Métodos de Búsqueda` (3 videos)

### Agregado / Mejorado:
- **Concepto de "estado" profundizado**: representación completa del sistema, qué información incluir/excluir
- **Espacios finitos vs infinitos**: tratamiento explícito de la distinción
- **Origen de "heurística"**: etimología y significado conceptual
- **Crecimiento exponencial de memoria**: ejemplo numérico concreto (20 MB en nivel 9, 25 GB en nivel 14 para BFS)
- **Primero en Profundidad Iterativa**: algoritmo completo que faltaba en el original
- **Búsqueda Bidireccional**: requisito de conocer el estado final, funcionamiento top-bottom y bottom-up
- **Aplicaciones prácticas de búsqueda heurística**: rutas, verificación de software (SAGE), sistemas expertos, optimización
- **Heurística en nodos vs transiciones**: distinción que el original no hacía
- **Escalada Simple vs Máxima Pendiente vs Primero el Mejor**: diferencias precisas en selección de nodos
- **Beam Search**: variante con memoria limitada, completamente nueva
- **A\***: fórmula f(n) = g(n) + h(n) con garantía de optimalidad y condición de heurística admisible
- **Tabla comparativa mejorada**: columna de características especiales y trade-offs memoria/tiempo

---

## 07 — Lógica Difusa

**Transcripciones usadas:** `IA - Razonamiento Aproximado y Lógica Difusa` (8 partes)

### Agregado / Mejorado:
- **Ejemplos del profesor**: caso de la maestra con disfraces (ambigüedad lingüística), descripción de una vaca (distintos niveles de precisión), juegos de azar y bolsa de valores (incertidumbre)
- **Historia académica**: Zaheh (1965 conjuntos difusos, 1971 lógica difusa), evolución desde lógica tradicional → polivalente → difusa
- **Sistema de altura (completo)**: funciones de pertenencia con valores numéricos específicos y cálculos
- **Sistema de contextura**: combinación de altura y muñeca con cálculos completos de inferencia
- **Sistema de reconocimiento de emociones (Kismet)**: caso real con arquitectura neurodifusa
- **Predicción de lluvia**: 165 reglas generadas automáticamente por sistema neurodifuso
- **Defuzzificación ampliada**: fórmula completa de Centro de Masa, Promedio del Máximo, ejemplo numérico completo
- **6 casos de uso reales**: diagnóstico cardíaco, lavadora fuzzy, control de automóviles, estimación de costos, emociones, predicción climática
- **Sistemas neurodifusos**: arquitectura completa, ventajas sobre sistemas difusos puros, ejemplo con resultados (68.85% efectividad)
- **Tabla comparativa**: Lógica Difusa vs Lógica Tradicional

---

## 08 — Implementación de Sistemas Inteligentes

**Transcripciones usadas:** `IA - Implementación Sistemas Inteligentes` (10 videos)

### Agregado / Mejorado:
- **Contexto organizacional**: cómo surge un SI, quién lo solicita, dinámicas de equipo
- **Elicitación de requerimientos**: desafíos específicos, por qué los expertos tienen dificultad para externalizar su conocimiento
- **Proceso iterativo de comprensión**: abstracción, descomposición, proyección, modularización
- **Evaluación de viabilidad de IA**: con ejemplo del ventilador (¿cuándo tiene sentido aplicar IA?)
- **Tabla de acciones formalizadas**: optimización, clasificación, predicción, clustering, etc. — con descripción y ejemplos
- **Método de emparrillado en identificación de datos**: integración con el tema de Emparrillado
- **Caso práctico dataset Iris**: detección de sesgos, gestión de versiones de datos
- **Regla de oro de normalización**: destacada explícitamente con énfasis del profesor
- **Ciclo ML detallado**: parámetros clave, prototipado iterativo, validación vs. prueba (3 conjuntos)
- **AG en construcción de modelos**: características deseables de cromosoma y función de aptitud, resolución de conflictos, penalización con niveles
- **Pipeline de aplicación**: 5 componentes detallados
- **Modelo "pan de pasas"**: completamente nuevo, explicación de por qué los problemas en producción son raros pero importantes
- **Caso real reconocimiento facial en Buenos Aires**: 81.6% de falsos positivos por datos incorrectos — ejemplo de importancia de datos de calidad

---

## 09 — PNL (Procesamiento del Lenguaje Natural)

**Sin cambios** — No hay transcripciones disponibles para este tema. Se copió el original sin modificaciones.

---

## Resumen general

| Tema | Archivos transcripción | Tamaño original | Tamaño nuevo | Mejora |
|------|----------------------|-----------------|--------------|--------|
| 01 Conceptos Iniciales | 10 videos | ~8KB | 19KB | +138% |
| 02 Análisis de Protocolos | 4 videos | ~10KB | 16KB | +60% |
| 03 Algoritmos Genéticos | 7 videos | ~12KB | 18KB | +50% |
| 04 Redes Neuronales | 15 videos | ~18KB | 28KB | +56% |
| 05 Emparrillado | 3 videos | ~9KB | 17KB | +89% |
| 06 Métodos de Búsqueda | 3 videos | ~8KB | 15KB | +88% |
| 07 Lógica Difusa | 8 videos | ~11KB | 18KB | +64% |
| 08 Implementación SI | 10 videos | ~14KB | 24KB | +71% |
| 09 PNL | Sin transcripciones | 5.8KB | 5.8KB | Sin cambios |

> 💡 **Recomendación para el examen:** Los temas con mayor contenido nuevo son Conceptos Iniciales (10 videos de dos playlists), Redes Neuronales (15 videos) e Implementación SI (10 videos). Priorizá leer esos diffs primero.
