# 08 — Implementación de Sistemas Inteligentes

> **Playlist:** Implementación de Sistemas Inteligentes  
> **Objetivo:** Proceso completo para construir e implementar un Sistema Inteligente en la práctica.

---

## Contexto: IA en Organizaciones

Los **Sistemas de Información** son redes de comunicación y recursos generados por procesos organizacionales. Cuando hay desvíos entre la situación esperada y la real, aparecen **problemas** que requieren soluciones. Un **Sistema Inteligente** es una solución que resuelve tareas poco conocidas que requieren conocimiento especializado, donde la **IA proporciona tecnologías específicas** para abordarlas.

---

## SW Tradicional vs Sistema Inteligente

| Aspecto | SW Tradicional | Sistema Inteligente |
|---------|---------------|-------------------|
| **Objetivo** | Construir un sistema software | Construir un SI |
| **Requerimientos** | Deseos y necesidades, características del dominio | Características de la tarea/problema, conocimientos (públicos y privados) |
| **Stakeholders** | Directivos, gerentes, usuarios | + **Expertos** del dominio |
| **Tecnología** | Hardware, paradigmas tradicionales | Modelos de IA, arquitecturas tradicionales, IC & ML |
| **Mantenimiento** | Correctivo, Adaptativo | **Perfectivo** (mejora continua) |
| **Implementación** | **Algorítmica** (procedural) | **Declarativa** |
| **Capacidad** | Determinista, poca redundancia | Flexible, robusta, adaptativa |
| **Aprendizaje** | No integrado | Puede aprender y mejorar con el tiempo |

---

## Fases de la Implementación de un SI

```
Definición del Problema
        ↓
Identificación y Transformación de Datos
        ↓
Selección de la Tecnología
        ↓
Construcción del Modelo
        ↓
Aplicación del Sistema Inteligente
```

El proceso es **iterativo**: es posible volver atrás en cualquier fase si se detectan problemas o mejoras necesarias.

---

## Fase 1: Definición del Problema

### Introducción

Esta es la fase más crítica. Requiere una construcción conceptual usando **principios ingenieriles** con fin práctico. Implica:

- **Identificar el QUÉ:** Qué problema resolver y cómo lo resolverá el SI
- **Identificar el CÓMO:** Qué datos y tecnologías son necesarios
- **Traducir:** Problemas de negocio → problemas de sistemas de información → modelos de IA

### 1.1 Elicitar Requerimientos

**Identificar fuentes de información:**

**Fuentes formales documentadas:**
- **Recursos propios:** DB, formularios, manuales, políticas, actas de reuniones
- **Recursos externos:** datos públicos, estándares, leyes, libros

**Fuentes informales (estructuras implícitas):**
- Conocimientos privados y experiencias del experto
- Suposiciones no fundamentadas
- Tareas complejas sin formalización

**Recolectar hechos y necesidades:**

| Técnica | Tipo | Descripción |
|---------|------|-------------|
| Análisis de documentación, datos | **Extracción** | Obtiene conocimientos públicos documentados |
| Entrevistas, cuestionarios, prototipado, observación, tormenta de ideas | **Educción** | Obtiene conocimiento privado/tácito del experto |
| **Emparrillado** | **Educción** | Técnica especial: obtiene modelo mental y conocimiento declarativo |
| **Análisis de protocolos** | **Educción** | Técnica especial: extrae reglas procedimentales observando acciones |

**Preguntas clave a responder:**

- ¿Qué incluye el problema? → **Elementos**
- ¿Dónde se produce? → **Contexto** (ambiente, entorno)
- ¿A quiénes afecta? → **Nuevos stakeholders**
- ¿Por qué resolverlo? → **Metas y expectativas**
- ¿Cómo se manifiesta? → **Escenarios**
- ¿Qué puede impedir resolverlo? → **Restricciones**

**Desafíos especiales:**
- El conocimiento no siempre está disponible explícitamente
- Se encuentra distribuido entre múltiples fuentes
- Puede estar incompleto o contradicto
- Está en lenguaje natural
- La presencia del elicitador puede modificar el problema

> **Regla clave:** Los requerimientos no se "capturan" sino que se "inventan" mediante trabajo cooperativo entre cliente y desarrollador.

### 1.2 Comprender los Requerimientos

El proceso de comprensión es **iterativo y evolutivo**, pasando por:

| Técnica | Qué permite | Resultado |
|---------|-------------|----------|
| **Abstracción** | Ignorar diferencias entre conceptos similares | Panorama general simplificado |
| **Descomposición** | Dividir en partes más simples (NO independientes) | Nivel de granularidad específico |
| **Proyección** | Identificar distintas visiones del mismo problema | Detectar inconsistencias y conflictos |
| **Modularización** | Agrupar elementos en módulos estables | Módulos reutilizables y coherentes |

**Modelado conceptual:**

Se generan **modelos conceptuales** que representan la realidad de forma simplificada. Estos modelos:
- Deben ser comprensibles (no tan simples ni tan complejos)
- Detectan problemas: requerimientos no definidos, incompletos, mal definidos, inconsistencias
- Permiten comunicar requerimientos mediante representaciones gráficas

**Herramientas de modelado:**
- Diagramas de composición funcional (descomposición de metas)
- Tablas de decisión
- Árboles de decisión
- Pseudo reglas (derivadas del análisis de protocolos)

### 1.3 Articulación de Requerimientos

**Responde:** ¿Qué se busca resolver? ¿Es viable aplicar IA?

A partir de los modelos conceptuales, se definen:

**Alcance del proyecto:** Todo lo que forma parte vs. lo que está fuera

**Objetivos:** Lo que la IA debe hacer para cumplir expectativas, deseos y necesidades

**Criterios de éxito:** Lo que debe cumplirse para considerar el proyecto exitoso
- Requiere **métricas objetivas** medibles

**Riesgos:** Lo que tiene probabilidad de ocurrir y desviar la ejecución esperada

**Evaluación de viabilidad de IA:**
- ¿Se puede resolver sin IA? (a veces sí)
- ¿Es la mejor alternativa?
- Considerar: tiempo, costo, complejidad, mantenimiento

> **Ejemplo de sobreingeniería:** Una empresa de cosmética japonesa vs. un ventilador industrial: El problema de cajas vacías se resolvió con un ventilador simple, no con un sistema inteligente costoso.

### 1.4 Formalización de Requerimientos

Se genera un **modelo formal** que especifica para cada tarea/objetivo:

```
Objetivo
  ↓
Precondiciones → [Tareas] → Postcondiciones
  ↓
Para cada tarea:
  - Propósito
  - Entradas
  - Acciones (tipo de operación)
  - Salidas
```

**Tipos de acciones (operaciones):**

1. **Optimización:** Encontrar combinación que maximice/minimice función matemática (ej: problema de la mochila)
2. **Clasificación:** Determinar clase de un elemento entre 2+ opciones
3. **Predicción:** Determinar comportamiento futuro con incertidumbre
4. **Regresión:** Encontrar función matemática que represente comportamiento de valores numéricos
5. **Clustering:** Agrupar elementos con características similares
6. **Reglas de asociación:** Encontrar relaciones entre valores de atributos (ej: pañales + cerveza)
7. **Detección de anomalías:** Identificar comportamientos fuera de lo normal (ej: fraudes con tarjeta)

**Resultado final:** Modelos del SI completamente formalizados y listos para la siguiente fase.

---

## Fase 2: Identificación y Transformación de Datos

### Concepto

Un **dato** es información asociada al problema en forma de tabla:
- **Columnas (atributos):** Propiedades/características de instancias
  - Atributos de entrada
  - Atributo objetivo/clase
- **Filas (ejemplos/instancias):** Valores de los atributos

### Proceso de Gestión de Datos

#### 1. Recolección de Datos

**Fuentes posibles:**
- Bases de datos transaccionales
- Planillas de cálculo
- Informes estadísticos
- Datos públicos
- Teorías/opiniones del experto
- Otros sistemas inteligentes

**Cuestiones a evaluar:**
- ¿Son datos confiables? (fuente, creador, modificador)
- ¿Son actuales o muy antiguos?
- ¿Se actualizan regularmente?
- ¿Es costoso acceder?
- ¿Hay consideraciones de privacidad?
- ¿Utilidad para el proyecto?

**Buena práctica:** Gestionar versiones de datos (pueden cambiar a medida que se descubren problemas)

#### 2. Análisis de Datos

Determinar:
- **Cantidad suficiente** para implementación
- **Atributos relevantes** (¿usar todos o solo algunos?)
- **Calidad:** Ruido, errores, duplicados, valores nulos
- **Representatividad:** ¿Son suficientemente representativos para cumplir objetivo?
- **Sesgo:** ¿Hay sesgos que harán los datos no representativos?

**Métodos de análisis:**
- Técnicas estadísticas tradicionales
- Algoritmos de minería de datos
- Métodos especializados (ej: método con **emparrillado** para evaluar datos de ML)

**Método propuesto para evaluación de datos:**
1. **Confección de parillas:** Preparación, diseño de parilla de elementos, diseño de parilla de características
2. **Formalización:** Clasificación, interpretación de resultados, discusión con experto

> **Caso ejemplo:** Dataset de Iris - se identificaron problemas de representatividad en algunas fuentes que se corrigieron usando datos originales de 1936.

#### 3. Preparación de Datos (más consumidor de tiempo)

**Integración:**
- Unificar datos en una única tabla
- Facilitar administración y uso

**Limpieza:**
- Corregir valores nulos, incompletos, con errores o ruido
- **Acciones posibles:**
  - Asignar nuevo valor (promedio, mínimo, máximo)
  - Eliminar ejemplo
  - Eliminar atributo (si no influye)

**Formateo - Transformaciones de tipos:**

**Tipos de atributos:**
- **Continuos (numéricos):** binarios, enteros, decimales
- **Discretos (no numéricos):** lógicos, alfanuméricos, fecha/hora

**Transformaciones:**

| De | A | Cómo |
|-------|---|------|
| **Continuo** | **Discreto** | Discretización: por criterios manuales, igual longitud, igual cantidad de ejemplos, usando atributo objetivo |
| **Discreto alfanumérico** | **Continuo** | Asignar código numérico único por valor O crear atributo binario para cada valor |
| **Discreto fecha/hora** | **Continuo** | Separar en día/mes/año, calcular días desde fecha fija, asignar código numérico |

**Normalización/estandarización:**
- Normalizar atributos numéricos usando promedio y varianza

> **Regla de oro:** Si se normalizan datos durante desarrollo, DEBEN normalizarse con los MISMOS PARÁMETROS en producción.

---

## Fase 3: Selección de la Tecnología

### Árbol de decisión para selección

**Paso 1: Evaluar disponibilidad de conocimiento**

| Situación | Tecnología candidata |
|-----------|------------------|
| **Datos disponibles** (completos, representativos) | **Machine Learning** |
| **Sin datos, pero hay reglas representativas** | ML (generar datos de reglas), IA Tradicional, IC |
| **Sin datos ni reglas, pero hay heurísticas** | **Inteligencia Computacional (Algoritmos Genéticos)** |
| **Sin datos, reglas ni heurísticas** | ❌ No se puede construir SI (volver a Fase 1) |

### Tabla de selección por tarea

| Tarea | Machine Learning | IA Tradicional | Inteligencia Computacional |
|-------|-----------------|------------------|--------------------------|
| **Optimización** | — | — | **Algoritmos Genéticos** ✓ |
| **Regresión** | Algoritmos regresión (supervisado) ✓ | — | AG ✓ |
| **Reglas de asociación** | Algoritmos inducción | — | — |
| **Clasificación** | RNA supervisada ✓ | SBC / SET ✓ | — |
| **Predicción** | RNA supervisada ✓ | SBC / SET ✓ | — |
| **Clustering** | RNA no supervisada (SOM) ✓ | — | — |
| **Detección de anomalías** | RNA no supervisada ✓ | — | — |

**Nota:** La tabla incluye los algoritmos más conocidos vistos en la cursada. Hay otros algoritmos posibles para cada tarea.

---

## Fase 4: Construcción del Modelo

### Generalidades

A partir de:
- Lista de módulos formalizados (Fase 1)
- Datos representativos (Fase 2)
- Tecnología elegida (Fase 3)

Se desarrollan los modelos software del SI.

> Analógía: Entrenar un modelo ML es como cultivar una planta: datos = agua, algoritmo = semilla, modelo = flor.

### 4.1 Machine Learning

**Ciclo:** Datos → Algoritmo → Modelo → Entrenamiento → Validación → Prueba

#### Entrenamiento

Proceso que aprende automáticamente parámetros/pesos del modelo a partir de ejemplos.

**Consideraciones:**
- Algoritmos supervisados vs. no supervisados
- Aprendizaje offline vs. online
- **Parámetros clave (ej: redes neuronales):**
  - **Tasa de aprendizaje (alfa):** Si es muy pequeña → lento, si es muy grande → inestable
  - **Ciclos de entrenamiento:** Demasiados → sobreentrenamiento, muy pocos → sin aprendizaje
  - Otros parámetros según algoritmo

#### Prototipado y Experimentación

**Iterativo:** entrenar → experimentar → analizar → reentrenar

Resolver problemas comunes:
- Falta de parámetros óptimos
- Necesidad de agregar/quitar datos
- Eliminar atributos ruidosos
- Normalizar datos
- Cambiar configuración de algoritmo

#### Validación

Evaluación sistemática de distintos parámetros para **optimizar el modelo**.

Proceso:
1. Entrenar con parámetros
2. Probar con datos de validación (diferentes a entrenamiento)
3. Evaluar precisión (más real que en entrenamiento)
4. Si no es óptimo, ajustar parámetros y repetir

> **Problema:** Iteraciones múltiples pueden llevar a sobreentrenamiento en AMBOS conjuntos.

#### Prueba (Testing)

**Objetivo:** Evaluar capacidad de **generalización** con datos similares a producción.

**Necesario:** Dividir datos disponibles en 3 conjuntos:
- **Entrenamiento:** Para aprender parámetros
- **Validación:** Para optimizar parámetros
- **Prueba:** Para evaluar generalización (datos nunca vistos)

**Métodos:** Muestreo estratificado, validación cruzada, etc.

**Métricas:** Precisión, recall, F1, matriz de confusión, etc. (según tarea)

### 4.2 Inteligencia Artificial Tradicional

**Proceso más manual:**

1. Identificar reglas y conceptos del experto
2. Codificar en **Base de Conocimientos** (BdC)
3. La BdC ES el modelo
4. Motor de inferencias (genérico): usa algoritmos de búsqueda (A*, primero el mejor, etc.)

**Formalismo:**
- Generalmente lógica de primer orden
- Puede ser similar a programación (IF-THEN) o prólogo
- Herramientas específicas: ej. K-PC (con clases, atributos, métodos, reglas)

**Ventaja:** Conocimiento explícito y auditable  
**Desventaja:** Codificación manual y tediosa

### 4.3 Inteligencia Computacional (Algoritmos Genéticos)

**Característica principal:** Requiere definir cuidadosamente 2 componentes clave:

#### 1. Cromosoma

Representación de la solución.

**Características deseables:**

| Característica | Descripción |
|---|---|
| **Tamaño fijo** | Simplifica el algoritmo (aunque otros algoritmos EC permiten tamaño variable) |
| **Mínimo y sin redundancia** | Solo atributos relevantes; evita ruido |
| **Completo** | Representa todas las soluciones posibles |
| **Evitar soluciones inválidas** | Baja probabilidad de combinaciones inválidas (puede usar redundancia estratégica) |
| **Uniformidad** | Todas las soluciones tengan igual probabilidad (puede entrar en conflicto con el anterior) |
| **Fácil de interpretar** | Representación intuitiva y directa |

**Solución a conflictos:**
- Si redundancia vs. uniformidad: priorizar evitar inválidas, luego penalizar inválidas correctamente
- Si mínimo vs. representación completa: priorizar completitud

#### 2. Función de Aptitud

Evalúa la calidad de cada solución (cromosoma).

**Características deseables:**

| Característica | Descripción |
|---|---|
| **Mejor uso del conocimiento** | Usar heurísticas, reglas o procedimientos de forma directa e intuitiva |
| **Consistencia** | Evaluar solo características representadas en cromosoma |
| **Reducir ruido** | Implementación correcta, sin errores |
| **Causalidad fuerte** | Pequeños cambios en cromosoma → pequeños cambios en aptitud (localidad) |
| **Penalización correcta** | Usar niveles de penas, no muerte única |

**Penalización:**
- **Evitar pena de muerte:** Asignar mismo valor a todos los inválidos
- **Usar niveles:** -20 para 1 inválida, -40 para 2, -60 para 3, etc.
- **Adaptativos:** Cambiar pena con progreso del algoritmo
  - Inicio: penas suaves
  - Avanzado: penas más fuertes para descartar inválidas

Ejemplo de penalización adaptativa: considerar calidad promedio de población

**Implementación:** En lugar de convertir heurísticas, usar directamente:
- Si heurística es función → implementar como función matemática
- Si es procedimiento → implementar como procedimiento
- Si son reglas → implementar reglas

> **Riesgo crítico:** Error en cromosoma o aptitud → algoritmo encuentra solución óptima para problema EQUIVOCADO.

---

## Fase 5: Aplicación del Sistema Inteligente

### 5.1 Integración de Modelos (Pipeline)

**Objetivo:** Ejecutar en producción todas las acciones del SI de forma integrada.

**Componentes del pipeline:**
1. **Recolección de datos**
2. **Preparación de datos** (limpieza, normalización, formateo)
3. **Ejecución del modelo**
4. **Ajuste de resultados** (para pasar a siguiente modelo si aplica)
5. Salida a usuario/sistema externo

> **LA REGLA DE ORO:**
> 
> Realizar en producción las **MISMAS acciones** de recolección y preparación que durante desarrollo. Si no, el modelo puede tener **comportamientos inesperados**.
>
> **Ejemplo:** Si se normalizaron datos con parámetros X en desarrollo, DEBEN normalizarse con MISMOS parámetros en producción. Si no, RNA interpreta datos incorrectamente.

**Buena práctica:** Implementar mismo código para preparación en dev y producción

### 5.2 Integración con Sistemas Externos

**Modelo de "pan de pasas" (Raisin Bread Model):**

"Las aplicaciones más exitosas de IA son aquellas donde la IA se integra como las pasas en pan: pequeña pero con nutrición importante."

**Concepto:**
- No desarrollar SI totalmente separado
- Integrar módulos de IA en sistemas existentes
- Hacerlo transparente para usuarios

**Ejemplos:**
- Sistema de stock: predecir materias primas futuras
- Gestión de clientes: segmentación/clustering
- Finanzas: análisis de riesgo, determinar qué clientes pagarán

**Ventajas:**
- Reduce rechazo de usuarios
- Aprovecha inversión existente
- Muchos ERP modernos aplican IA como servicios/batch transparentes

### 5.3 Cuidados al Integrar con Sistemas Externos

**Riesgo:** Datos erróneos del sistema existente afectan al SI.

**Caso real:** Sistema de reconocimiento facial en subtes de Buenos Aires
- **Tecnología:** Muy buena (99% género, 95% edad, 0.5 seg por rostro)
- **Problema:** 81.6% liberaciones de detenidos (datos incorrectos)
- **Causas:**
  - Orden judicial ambigua ("de interés" ≠ "detener")
  - Causas judiciales desactualizadas (sobreseído pero orden activa)
  - Errores en carga de datos (DNI mal, nombre mal)

**Recomendación:** Hacer pruebas de aceptación con datos REALES de producción antes de go-live

### 5.4 Instalación en Producción

- Pruebas de aceptación con datos de producción
- Prueba en paralelo (sistema inteligente vs. proceso actual)
- Go-live gradual si es posible

### 5.5 Monitoreo

Post-instalación:
- **Primeros días/horas:** Monitoreo exhaustivo
- Verificar que sistema no esté fallando
- Detectar problemas de performance
- Considerar variaciones en tiempos de operatoria

### 5.6 Mantenimiento (Perfectivo)

A diferencia del SW tradicional (correctivo, adaptativo), el SI tiene mantenimiento **PERFECTIVO**: mejorar y evolucionar.

**Implica:** Volver a aplicar fases según sea necesario
- Modificar modelos
- Cambiar tecnología
- Buscar nuevos datos
- Cambiar definición del problema (nuevos requerimientos)

> **Proceso iterativo:** El proceso completo es más iterativo que cascada. Es posible/necesario volver atrás en cualquier fase cuando se detecten problemas o mejoras.

---

## Resumen de Decisiones Clave

1. **Definición:** Usar técnicas de elicitación (educción: emparrillado, análisis de protocolos) para capturar conocimiento tácito del experto
2. **Datos:** Evaluar representatividad (método de parillas); garantizar calidad
3. **Tecnología:**
   - Datos disponibles → **ML**
   - Reglas sin datos → **IA Tradicional / IC**
   - Solo heurísticas → **Algoritmos Genéticos**
4. **Construcción:**
   - ML: entrenaimiento + validación + prueba (separar conjuntos)
   - IA Tradicional: codificación de reglas en BdC
   - AG: definir cromosoma y función de aptitud con cuidado
5. **Aplicación:** Usar MISMAS transformaciones dev=producción; integrar sin reemplazar; probar con datos reales

---

## 📝 Cambios respecto al original

### Agregado:

1. **Contexto organizacional:** Explicación de cómo surge un SI dentro de una organización (sistemas de información, desvíos, problemas)

2. **Fase 1 expandida significativamente:**
   - Introducción con énfasis en construcción conceptual
   - Desafíos específicos de elicitar requerimientos (conocimiento distribuido, contradictorio, en lenguaje natural)
   - Proceso de comprensión como iterativo y evolutivo
   - Detalles de herramientas de modelado (composición funcional, tablas, árboles de decisión)
   - Articulación: evaluación de viabilidad de IA (ejemplo del ventilador vs. sistema costoso)
   - Formalización: tabla detallada de tipos de acciones (optimización, clasificación, predicción, etc.)

3. **Fase 2 significativamente mejorada:**
   - Definición clara de dato como tabla (columnas/filas)
   - Proceso estructurado de recolección con cuestiones prácticas a evaluar
   - Gestión de versiones de datos
   - Método propuesto de evaluación con parillas (técnica de emparrillado)
   - Caso de Iris como ejemplo práctico de identificar sesgos
   - Detalles sobre transformaciones de tipos de atributos
   - Regla de oro explícita: normalización con parámetros consistentes

4. **Fase 3 mejorada:**
   - Árbol de decisión más claro para seleccionar tecnología
   - Nota sobre limitaciones de la tabla (no incluye todos los algoritmos)

5. **Fase 4 ampliamente expandida:**
   - Analogía de cultivo de plantas para ML
   - Detalles de parámetros clave (tasa de aprendizaje, ciclos)
   - Explicación clara de ciclo iterativo (entrenamiento → experimento → análisis → reentrenamiento)
   - Sección de prototipado y experimentación
   - Problema de sobreentrenamiento en validación
   - Explicación clara de validación vs. prueba (3 conjuntos de datos)
   - IA Tradicional: uso de herramientas como K-PC con ejemplo de flores
   - Algoritmos Genéticos: características deseables de cromosoma (con soluciones a conflictos)
   - Función de aptitud: características deseables, penalización con niveles, enfoque adaptativo
   - Riesgo crítico: solución correcta para problema equivocado

6. **Fase 5 ampliamente expandida:**
   - Pipeline detallado (5 componentes)
   - LA REGLA DE ORO: explícita y destacada
   - Modelo "pan de pasas": concepto, ventajas, ejemplos
   - **Caso real del reconocimiento facial en Buenos Aires:** Análisis de cómo datos erróneos del sistema externo afectan SI (81.6% falsos positivos)
   - Pruebas con datos reales de producción (recomendación clave)
   - Monitoreo post-instalación
   - Mantenimiento perfectivo vs. correctivo (diferencia clara)

7. **Sección "Resumen de Decisiones Clave":** Nuevo, para resumir puntos críticos del proceso

8. **Nota sobre proceso iterativo:** Clarificación de que no es puramente cascada

### Mejorado:

- Más contexto en cada sección
- Ejemplos concretos de casos reales
- Mejor estructura y flujo
- Tablas más completas
- Énfasis en las reglas de oro y mejores prácticas
- Conexión clara entre fases
