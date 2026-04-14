# 08 — Implementación de Sistemas Inteligentes

> **Playlist:** Implementación de Sistemas Inteligentes  
> Fuente: Clase 8, Para el Coloquio

---

## SW Tradicional vs Sistema Inteligente

| Aspecto | SW Tradicional | Sistema Inteligente |
|---------|---------------|-------------------|
| **Tareas** | Sistemáticas y procedimentales | Poco conocidas o especializadas |
| **Implementación** | Algorítmica | **Declarativa** |
| **Flexibilidad** | Determinista, poca redundancia | Flexible y robusto |
| **Requerimientos** | Funcionalidades y datos | + Conocimientos (públicos y privados) |
| **Stakeholders** | Directivos, gerentes, usuarios | + **Expertos** |
| **Mantenimiento** | Correctivo, adaptativo | **Perfectivo** (mejora continua) |

**IA desde dos perspectivas:**
- **Ciencia:** estudia el comportamiento de los sistemas inteligentes
- **Ingeniería:** provee herramientas y métodos para construirlos

---

## Fases de Implementación de un SI

```
1. Definición del Problema
        ↓
2. Identificación y Transformación de Datos
        ↓
3. Selección de la Tecnología
        ↓
4. Construcción del Modelo
        ↓
5. Aplicación del Sistema Inteligente
        ↓
6. Instalación y Mantenimiento
```

---

## Fase 1: Definición del Problema

### 1.1 Elicitar Requerimientos

**Identificar fuentes de información:**

| Fuente | Ejemplos |
|--------|---------|
| **Recursos propios** | BD, formularios, manuales, políticas, actas de reuniones |
| **Recursos externos** | Datos públicos, estándares y leyes, libros |
| **Stakeholders** | Grupos de interés impactados (formales e informales) |

**Técnicas de recolección:**

| Técnica | Tipo | Descripción |
|---------|------|-------------|
| Análisis de documentación y datos | **Extracción** | Recolectar conocimiento explícito |
| Entrevistas, cuestionarios, prototipado, observación, brainstorming | **Educción** | Obtener información del experto |
| **Emparrillado** | Educción | Clasificación de elementos por experto |
| **Análisis de Protocolos** | Educción | Experto piensa en voz alta |

**Preguntas clave a responder:**
- ¿Qué incluye el problema? → Elementos
- ¿Dónde se produce? → Contexto
- ¿A quiénes afecta? → Stakeholders adicionales
- ¿Por qué resolverlo? → Metas y expectativas
- ¿Cómo se manifiesta? → Escenarios
- ¿Qué impide resolverlo? → Restricciones

**Problemas comunes del conocimiento del dominio:**
- No suele estar disponible de forma explícita
- Se encuentra distribuido en muchas fuentes
- Puede haber conflictos entre fuentes
- Está expresado en lenguaje natural

### 1.2 Comprender los Requerimientos

| Técnica conceptual | Qué permite |
|-------------------|-------------|
| **Abstraer** | Ignorar diferencias entre conceptos similares → panorama general |
| **Descomponer** | Dividir en partes más simples (las partes no son independientes) |
| **Proyectar** | Identificar distintas visiones del mismo problema |
| **Modularizar** | Combinar elementos en módulos estables y reutilizables |

**Definición del alcance:** objetivos, criterios de éxito, riesgos.

### 1.3 Formalización de objetivos

Transformar las expectativas, deseos y necesidades en **objetivos** y **tareas concretas** a realizar.

**Preguntas clave:**
- ¿Qué se busca resolver?
- ¿Es viable aplicar IA?

---

## Fase 2: Identificación y Transformación de Datos

*(Solo se aplica cuando hay datos disponibles)*

| Subetapa | Descripción |
|----------|-------------|
| **Recolección** | Obtener datos externos (repo público) o propios de la organización (puede incluir generación) |
| **Estudio** | Visualización con técnicas estadísticas, minería de datos, o métodos ad-hoc |
| **Integración** | Unificar en una única tabla por módulo |
| **Formateo** | Ajuste del formato según las necesidades del algoritmo |
| **Limpieza** | Corregir valores nulos, incompletos, erróneos o con ruido en columnas (atributos) y filas (ejemplos) |
| **Selección** | Elegir los atributos y ejemplos más relevantes |

---

## Fase 3: Selección de la Tecnología

### Machine Learning

**Cuándo usar:** problemas de **clasificación o predicción** con datos disponibles.

| Subtecnología | Cuándo | Requisitos |
|--------------|--------|-----------|
| Árboles de decisión (TDIDT) | Clasificación con datos tabulares | Datos de entrenamiento, validación, prueba |
| RNA (Backpropagation, CNN) | Clasificación o predicción | Datos + definir métricas, prototipado, evaluar generalización |

**Pasos adicionales:**
- Definir métricas de evaluación
- Prototipado y experimentación
- Evaluar capacidad de generalización
- Seleccionar patrones relevantes

### IA Tradicional (SBC, SET)

**Cuándo usar:** cuando hay **reglas y conceptos** de un experto pero no datos suficientes.

**Requisitos:** reglas de razonamiento + conceptos del dominio (extraídos con AP o emparrillado).

### Inteligencia Computacional (Algoritmos Genéticos)

**Cuándo usar:** problemas de **optimización** sin datos históricos pero con heurísticas.

**Requisitos:**
- Definir la estructura del cromosoma
- Definir la función de aptitud
- Pueden usarse también conceptos, características, reglas y/o heurísticas

---

## Fase 4: Construcción del Modelo

*(Específica a cada tecnología — ver los temas correspondientes)*

---

## Fase 5: Aplicación del Sistema Inteligente

**Pipelines (Canalización):** interfaces entre los diferentes módulos del sistema.

Incluye:
- Integración con Software Tradicional existente
- Definición de interfaces y usabilidad

---

## Fase 6: Instalación y Mantenimiento

**Instalación:** instalar el sistema en el entorno de producción.

**Monitoreo:** supervisar el comportamiento del sistema en producción.

**Mantenimiento (perfectivo):** puede ser necesario:
- Ingresar o retirar datos
- Ajustar o cambiar el modelo
- Cambiar de tecnología si el problema evoluciona

---

## Técnicas de Educción del Conocimiento: AP vs Emparrillado

| | Análisis de Protocolos | Emparrillado |
|--|----------------------|-------------|
| **Qué captura** | Conocimiento implícito (procedimental + declarativo) | Similitudes/diferencias entre elementos (declarativo superficial) |
| **Resultado** | Reglas SI-ENTONCES, tabla CCV | Árboles de similitud, red de relaciones entre características |
| **Cuándo** | Cuando el experto razona en voz alta | Cuando se quiere ver cómo el experto clasifica elementos |
| **Limitación** | Complejo de analizar | Por sí solo no sirve para construir la base de conocimientos |

---

## Ingeniería del Conocimiento (INCO)

Metodología para construir sistemas inteligentes:
1. **Adquirir conocimientos:** recolección de info y ciclos de educción
2. **Conceptualización:** entender el dominio y la terminología
3. **Formalización:** expresar el conocimiento mediante técnicas formales
4. **Implementación:** puesta en marcha del sistema

---

## Trampas del examen

- La implementación de un SI es **declarativa** (no algorítmica como el SW tradicional)
- El mantenimiento de un SI es **perfectivo** (no solo correctivo)
- Los **stakeholders** de un SI incluyen también a los **expertos** del dominio
- La educción es para obtener conocimiento **del experto**; la extracción es de **documentos/datos**
- El Emparrillado **por sí solo no sirve** para construir la base de conocimientos
- La formalización de objetivos transforma deseos/necesidades en **tareas concretas**
- La fase de datos es **opcional** (solo si hay datos disponibles)
- Los pipelines conectan los diferentes **módulos** del SI entre sí y con el SW tradicional
