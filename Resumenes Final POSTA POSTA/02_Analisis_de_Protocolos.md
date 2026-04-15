# 02 — Análisis de Protocolos

> **Playlist:** Análisis de Protocolos  
> **Objetivo:** Técnica de educción del conocimiento para extraer lo que un experto sabe pero no puede verbalizar fácilmente.  
> **Origen:** Basada en el procedimiento de protocolos verbales de Ericsson (1993), originario del ámbito de la psicología cognitiva.

---

## ¿Qué es?

El **Análisis de Protocolos** es una técnica donde el experto **piensa en voz alta** mientras resuelve una tarea en su dominio de experticia. Se graba todo lo que verbaliza durante el proceso.

### Ventaja clave
Revela procedimientos que el experto utiliza pero **no puede verbalizar conscientemente** (conocimiento tácito). El experto durante la ejecución puede:
- Consultar libros o referencias externas
- Buscar información en internet
- Realizar acciones secundarias que enriquecen el razonamiento

Esta técnica **trasladada de la psicología a la Inteligencia Artificial** permite capturar el razonamiento completo de especialistas en diagnósticos, resolución de problemas y toma de decisiones.

---

## Etapas

### 1. Grabación del Protocolo

#### Subetapa 1: Explicación del Objetivo
- El **Ingeniero en Conocimientos (IC)** explica al experto cuál es el objetivo de la técnica
- Se clarifica que se busca capturar **cómo razona el experto** al ejecutar la tarea
- Se instruye al experto sobre el comportamiento requerido: informar **todo lo que piensa** en el momento
- Se aclara que si el experto se queda callado o tiene dudas, será interrumpido para poder completar la grabación correctamente

#### Subetapa 2: Puesta en Situación
- Se proponen **pequeños ejercicios de práctica** (anagramas, multiplicaciones, divisiones, etc.)
- El experto practica verbalizando en voz alta para familiarizarse con la técnica
- **Objetivo:** Dar confianza al experto antes de la grabación real
- *Nota:* Si el experto ya está habituado al análisis de protocolos, esta subetapa puede omitirse

#### Subetapa 3: Registro del Protocolo (Grabación Real)
- El IC se reúne con el experto en su entorno de trabajo (consultorio, oficina, etc.)
- Se graba íntegramente el proceso de resolución del problema
- Es crítico **definir con claridad el objetivo** que el experto debe resolver
- **Ejemplo real (caso médico):**
  - Objetivo: Diagnosticar la enfermedad según los síntomas presentados
  - El experto examina al paciente y verbaliza: "el paciente presenta fiebre superior a 38 grados, manifiesta un fuerte dolor de garganta y tos seca, su frecuencia respiratoria es muy elevada y tiene dolores musculares intensos. Podríamos pensar que estamos ante un coronavirus COVID-19. El paciente debe permanecer aislado por precaución..."

---

### 2. Transcripción

- El IC **escucha la grabación** y la transcribe de forma **segmentada**
- **No se copia todo en una sola hoja**, sino que se divide en **frases manejables**
- Cada línea recibe un número para facilitar referencias posteriores

#### Criterios de Segmentación
La segmentación flexible se basa en:
- Separación entre **sujeto y predicado**
- División de frases grandes en múltiples líneas
- Equilibrio: ni frases demasiado largas, ni palabras aisladas
- Importancia posterior: la segmentación debe facilitar el análisis futuro
- **Nota:** No existe una única forma "correcta" de segmentar; diferentes ICs pueden segmentar de formas distintas

#### Anotaciones en la Transcripción
Se agregan anotaciones sobre **acciones observadas del experto** durante la grabación:
- Si consultó un libro, blog o documento propio
- Si buscó información en internet
- Si se quedó callado (silencio) → puede indicar falta de información o conocimiento implícito no verbalizado

Estas anotaciones son críticas porque:
- Revelan **conocimiento que el experto no verbaliza** pero sí consulta
- Permiten identificar **brechas de información** en el razonamiento

---

### 3. Codificación

La etapa más importante. Divide el análisis en **tres subetapas** que transforman el protocolo en conocimiento estructurado.

#### Subetapa 1: Conceptos, Características, Valores, Relaciones y Operadores

**Analogía con Diagrama de Entidad-Relación (DER):**

| Elemento | Analogía DER | Descripción |
|----------|-------------|-------------|
| **Concepto** | Entidad | Sustantivos principales del dominio; elementos centrales del problema |
| **Característica** | Atributo | Cualidad propia de un concepto; propiedad que lo describe |
| **Valor** | Valor del atributo | El valor concreto de la característica (puede ser único, múltiple o un rango) |
| **Relación** | Relación | Vínculo entre conceptos, o entre concepto y característica, o característica y valor |
| **Operador** | — | Medio para pasar de un estado a otro más próximo de la solución; lo que "impulsa" el razonamiento |

**Ejemplo de análisis detallado:**

> "El paciente presenta fiebre superior a 38°"

| Texto | Tipo | Justificación |
|-------|------|---------------|
| paciente | Concepto | Sustantivo principal del dominio |
| presenta | Relación | Vínculo entre paciente y su síntoma |
| fiebre | Característica | Cualidad del paciente |
| superior a 38° | Valor | Valor específico de la característica fiebre |

**Caso especial: Diferenciar Concepto de Característica**

> "El mareo fue repentino y de larga duración"

- ¿Es "mareo" una característica? NO, porque:
  - Tiene su propio tipo (repentino)
  - Tiene su propia duración (larga)
  - Tiene características propias
- **Conclusión:** Mareo es un **Concepto** con sus propias características

**Tabla CCV (Concepto-Característica-Valor) Resultante:**

| Concepto | Característica | Valores |
|----------|---------------|---------|
| paciente | fiebre | superior a 38° |
| | dolor de garganta | fuerte |
| | tos | seca |
| | frecuencia respiratoria | muy elevada |
| | dolores musculares | intensos |
| mareo | tipo | repentino |
| | duración | larga |
| análisis de laboratorio | resultado | positivo al virus H1N1 |

> **Nota sobre características implícitas:** Características entre paréntesis (tipo) = implícitas (el experto no las verbaliza explícitamente; hay que preguntar para confirmar).

**Estados: Dos Visiones Válidas (pero no mezclar)**

Los estados pueden considerarse de dos formas alternativas:

1. **Estados como Conceptos:** 
   - coronavirus, gripe clase A son conceptos por sí solos
   - Sin atributo diagnóstico explícito
   
2. **Estados como Valores:** 
   - coronavirus, gripe clase A son valores del atributo "diagnóstico"
   - El diagnóstico es la característica del paciente

**Regla importante:** Elegir **una sola visión** y ser consistente en todo el análisis.

**Relaciones Implícitas** (solo entre conceptos):

Si los estados se consideran **conceptos:**
- `paciente → tiene → coronavirus`
- `paciente → sufre de → mareo`
- `paciente → se realiza → análisis de laboratorio`

Si los estados se consideran **valores:**
- Ya están incluidos en la tabla CCV
- `paciente → sufre de → mareo`
- `paciente → se realiza → análisis de laboratorio`

**Criterio fundamental:** No existen relaciones implícitas entre **sinónimos** (paciente ≠ persona en términos de relación; son lo mismo).

---

#### Subetapa 2: Identificación de la Búsqueda

A pesar del nombre, **no se construye un árbol de búsqueda formal**, sino que se identifican:

1. **Estados** por los que pasó el experto
2. **Operadores** que utilizó para transicionar
3. **Condiciones** necesarias para llegar a cada estado

**Visualización gráfica:**

```
OBJETIVO: Diagnosticar al paciente según síntomas
    ↓
[ESTADO 1: "Podría ser coronavirus COVID-19"]
    ↑
    Operador: "Estamos ante un..."
    Condiciones:
    - paciente.fiebre = superior a 38°
    - paciente.dolor de garganta = fuerte
    - paciente.tos = seca
    - paciente.frecuencia respiratoria = muy elevada
    - paciente.dolores musculares = intensos

[ESTADO 2: "Se trata de gripe clase A"]
    ↑
    Operador: "Concluimos que se trata de una..."
    Condiciones (segunda observación):
    - paciente.dolor de cabeza = persistente
    - mareo.tipo = repentino
    - mareo.duración = larga
    - análisis de laboratorio.resultado = positivo al virus H1N1
```

**Proceso:**
1. Identificar los estados finales (o intermedios) a los que llegó el experto
2. Identificar los operadores que permitieron la transición
3. Releer la transcripción para extraer las **condiciones exactas** que el experto consideró

---

#### Subetapa 3: Sinónimos, Metacomentarios e Incertidumbres

**A) Sinónimos:**
- Palabras o frases distintas que refieren al **mismo concepto**
- Ejemplo: "paciente" y "persona" se usan indistintamente en el protocolo
- **Acción:** Formalizar estos sinónimos y **eliminar relaciones implícitas** entre ellos
- Importante para evitar redundancias en las relaciones

| Sinónimo 1 | Sinónimo 2 |
|-----------|-----------|
| paciente | persona |

**B) Metacomentarios:**
- Son comentarios del experto que **no aportan información directa** al razonamiento
- Se registran por línea y significado, ya que pueden ser útiles para futuros protocolos
- Ejemplo: "El paciente debe permanecer aislado por precaución, dado lo contagioso del virus"
  - Líneas: [10-12]
  - Significado: Referencia a la contagiosidad del COVID-19
  - Utilidad: Para futuro: ante COVID-19, marcar necesidad de aislamiento

| Líneas | Metacomentario | Significado | Utilidad Futura |
|--------|---------------|-----------|-----------------|
| [10-12] | "debe permanecer aislado..." | Contagiosidad del COVID-19 | Medidas de aislamiento requeridas |
| [13] | "en una segunda observación" | Indica subetapa del razonamiento | Separa búsqueda inicial de análisis posterior |

**C) Incertidumbres:**
- Expresiones de **duda** sobre el cambio de estado
- Solo se registran las que afecten la **transición entre estados**
- Ejemplo: "Podríamos pensar que..." (línea 7)
- Indica que la conclusión no es determinística (puede ocurrir en 80% de casos, no 100%)

| Línea | Incertidumbre | Tipo |
|-------|---------------|------|
| [7] | "Podríamos pensar que..." | Duda sobre cambio a estado coronavirus |

---

### 4. Interpretación

Última etapa: **Identificar las reglas de razonamiento** del experto en formato pseudocódigo.

#### Estructura de Reglas

Formato estándar:
```
SI (condición1) Y (condición2) Y ... (condiciónN)
ENTONCES asignar (atributo_objetivo = valor_resultado)
```

Las condiciones siempre tienen la forma:
```
concepto.característica = valor
```

#### Reglas del Ejemplo

**Regla 1: Diagnóstico de Coronavirus**
```
SI (paciente.fiebre = superior a 38°) Y
   (paciente.dolor de garganta = fuerte) Y
   (paciente.tos = seca) Y
   (paciente.frecuencia respiratoria = muy elevada) Y
   (paciente.dolores musculares = intensos)
ENTONCES asignar (paciente.diagnóstico = coronavirus COVID-19)
```

**Regla 2: Diagnóstico de Gripe Clase A**
```
SI (paciente.dolor de cabeza = persistente) Y
   (mareo.tipo = repentino) Y
   (mareo.duración = larga) Y
   (análisis de laboratorio.resultado = positivo al virus H1N1)
ENTONCES asignar (paciente.diagnóstico = gripe clase A)
```

#### Nota sobre Atomicidad de Reglas

- Las reglas se tratan de forma **atómica** (independientes entre sí en esta etapa)
- No se busca crear subsunción o jerarquía de reglas en análisis de protocolos
- Posteriormente, cuando se tienen **múltiples protocolos**, se relacionan y organizan las reglas
- Esta separación permite capturar el razonamiento puro del experto sin interpretaciones

#### Proceso de Múltiples Protocolos

- **Un protocolo** = primer paso incompleto
- Se requieren **muchos protocolos** con el mismo (u otros) experto para capturar el razonamiento completo
- Después de múltiples protocolos, se comienza a **relacionar y organizar** el conocimiento

---

## Resumen Ejecutivo

1. **Propósito:** El análisis de protocolos captura **conocimiento implícito** del experto que no puede verbalizar conscientemente.

2. **4 Etapas principales:**
   - **Grabación:** El experto piensa en voz alta mientras resuelve un problema
   - **Transcripción:** Se segmenta y anota la grabación
   - **Codificación:** Se identifican conceptos, características, valores, relaciones, operadores, estados, sinónimos, metacomentarios e incertidumbres
   - **Interpretación:** Se formulan reglas de razonamiento en pseudocódigo

3. **Elemento clave - Codificación:**
   - Identificar **Concepto / Característica / Valor / Relación / Operador**
   - Construir tabla **CCV** ordenada
   - Identificar **Estados** y cómo transiciona entre ellos
   - Marcar **características implícitas** entre paréntesis para validar con el experto

4. **Decisión de Diseño Importante:**
   - Los **estados** pueden ser considerados como **conceptos** O como **valores**, pero elegir **una sola visión** y mantenerla consistente

5. **Reglas de Interpretación:**
   - Formato: `SI (concepto.característica = valor) ENTONCES (atributo_objetivo = valor_resultado)`
   - Las reglas son **atómicas** en esta etapa
   - No hay jerarquía ni subsunción dentro de un protocolo

6. **Metacomentarios e Incertidumbres:**
   - **Metacomentarios:** No aportan al razonamiento directo pero son útiles para contexto futuro
   - **Incertidumbres:** Expresan dudas solo sobre transiciones de estado

7. **Iteración:**
   - Un protocolo es apenas el comienzo
   - Se requieren **múltiples protocolos** para capturar el razonamiento completo del experto

---

## 📝 Cambios respecto al original

### Agregados principales:

1. **Origen histórico:** Se incorporó referencia a Ericsson (1993) y el procedimiento de protocolos verbales desde la psicología cognitiva

2. **Detalles de Subetapa 1 - Grabación:** 
   - Explicación clara del rol del IC
   - Instrucciones específicas dadas al experto (verbalizar, tolerancia a interrupciones)
   - Ejemplo real completo del caso médico tomado de la transcripción

3. **Mejora en Segmentación:**
   - Se aclaró que "no existe forma correcta única"
   - Se mostró que diferentes ICs pueden segmentar diferente
   - Se explicó el equilibrio entre frases y palabras aisladas

4. **Profundización en Anotaciones:**
   - Se explicó qué tipo de anotaciones se hacen (libros consultados, búsquedas en internet, silencios)
   - Se justificó por qué estas anotaciones son críticas

5. **Ejemplo detallado de CCV:**
   - Se añadió tabla con ejemplos completos
   - Se explicó con caso especial del "mareo" (por qué no es característica)
   - Se aclaró la diferencia entre características explícitas e implícitas

6. **Dos visiones de Estados:**
   - Se presentó claramente la decisión de diseño
   - Se mostró cómo cambia la tabla según la elección
   - Se enfatizó la importancia de ser consistente

7. **Subetapa 2 - Visualización gráfica:**
   - Se agregó diagrama visual del flujo de estados
   - Se mostró cómo se extraen condiciones de la transcripción
   - Se aclaró que "búsqueda" no significa construir árbol de búsqueda formal

8. **Subetapa 3 - Tabla mejorada:**
   - Se agregó columna de "Utilidad Futura" para metacomentarios
   - Se aclaró que incertidumbres solo cuentan si afectan transiciones de estado
   - Se explicó la diferencia entre sinónimos (no tienen relaciones) y otros conceptos

9. **Interpretación - Contexto:**
   - Se explicó por qué las reglas son atómicas
   - Se justificó por qué no hay subsunción en esta etapa
   - Se aclaró que la organización viene después con múltiples protocolos

10. **Atomicidad de Reglas:** Se profundizó en este concepto clave que justifica por qué una regla no incluye todas las condiciones de otra

11. **Iteración y Escala:** Se explicó claramente que un protocolo es incompleto y se requieren múltiples para capturar el razonamiento completo
