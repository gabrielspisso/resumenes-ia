# 02 — Análisis de Protocolos

> **Playlist:** Análisis de Protocolos  
> Fuente: Clase 3, Para el Coloquio

---

## ¿Qué es?

Técnica de **educción del conocimiento** para revelar lo que saben los expertos de un dominio.

**Metodología:** se solicita al experto que **piense en voz alta** mientras realiza la tarea.

**Finalidad:** obtener información sobre procedimientos que el experto usa en la resolución de problemas pero **no puede verbalizar en forma consciente** (conocimiento tácito/implícito).

**Responsable:** el Ingeniero en Conocimiento (IC).

**Origen:** definido por primera vez en 1993 en base a protocolos verbales.

---

## Las 4 Etapas del AP

### Etapa 1: Grabación del Protocolo

1. El IC explica al experto el objetivo de la técnica y la metodología
2. Puesta en situación: pequeños ejercicios para generar confianza
3. **Si el experto se calla**, el IC lo interrumpe para recordarle que debe verbalizar
4. Registro: grabación de audio/video mientras el experto resuelve el problema

### Etapa 2: Transcripción

1. El IC escucha la grabación
2. Transcribe **segmentando en frases numeradas** (cada frase = un segmento)
3. También transcribe **acciones** que realiza el experto fuera del habla (consultó un manual, dibujó algo, etc.)
4. No hay una única forma correcta de segmentar

### Etapa 3: Codificación

Se construye una **tabla CCV** (Conceptos – Características – Valores) y se identifican relaciones y operadores.

#### Elementos del protocolo

| Elemento | Analogía en DER | Descripción |
|----------|----------------|-------------|
| **Concepto** | Entidad (Tabla) | Sustantivos principales del dominio |
| **Característica** | Atributo (Campo) | Cualidad propia de un concepto |
| **Valor** | Valor del atributo | El valor concreto de esa característica |
| **Relación** | Foreign Key | Vínculo entre conceptos, o entre concepto y característica |
| **Operador** | — | Medio que usa el experto para pasar de un estado a otro más próximo a la solución |

#### Reglas de la tabla CCV

- **No debe haber huecos** en la tabla (si hay una característica implícita, se pone entre paréntesis y se valida con el experto)
- Los conceptos considerados como **estados no tienen características**
- Los **sinónimos no tienen características** propias
- **No existen relaciones entre sinónimos**
- Todo lo implícito escrito debe **validarse con el experto**

#### ¿Cuándo algo es concepto y cuándo es característica?

Si algo tiene **sus propias características** → es un **Concepto** (no una característica).

**Ejemplo:**
- "El mareo fue repentino y de larga duración"
- "Mareo" tiene tipo y duración → es un **Concepto**, no una característica del paciente

#### Los estados: dos formas válidas

| Visión A | Visión B |
|----------|---------|
| Los estados son Conceptos (ej: COVID-19, gripe son entidades) | Los estados son Valores de un atributo del paciente (ej: diagnóstico = COVID-19) |

Ambas son válidas, pero hay que elegir **una sola y ser coherente**.

#### Subetapa: Identificación de la búsqueda

- Identificar los **estados** por los que pasó el experto
- Identificar las **características** de cada estado
- Identificar los **operadores** que llevaron a las transiciones entre estados

#### Subetapa: Sinónimos, Metacomentarios e Incertidumbres

| Elemento | Definición | Cómo se identifica |
|----------|-----------|-------------------|
| **Sinónimos** | Palabras distintas que refieren al mismo concepto | Se anotan, no se duplican en CCV |
| **Metacomentario** | Comentario del experto que no aporta al razonamiento | Se registra la línea y su significado en tabla aparte |
| **Incertidumbre** | Expresión de duda sobre el cambio de estado | "podría ser...", "quizás..." |

**Tabla de metacomentarios:**

| Líneas | Metacomentario | Significado |
|--------|---------------|------------|
| [10-12] | "el paciente debe permanecer aislado" | Referencia a la contagiosidad del COVID |

### Etapa 4: Interpretación

Se identifican las **reglas de razonamiento** en pseudocódigo SI-ENTONCES:

```
SI (Concepto.Caracteristica = Valor)
   Y (Concepto.Caracteristica = Valor)
ENTONCES asignar (atributo_objetivo, valor_resultado)
```

**Condiciones:** `Concepto.Caracteristica = Valor`

Las reglas se tratan de forma **atómica** (independientes entre sí en esta etapa).

---

## Conocimiento obtenido

| Tipo | Definición | Dónde se encuentra |
|------|-----------|-------------------|
| **Procedimental** | Cómo el experto llegó a la solución (las reglas) | Etapa 4: Interpretación |
| **Declarativo** | Objetos del dominio y sus características y relaciones | Etapas 2, 3 |

---

## Ejemplo completo

**Protocolo del experto:**
> "El paciente tiene fiebre superior a 38° y tos seca. También tiene dolor de garganta fuerte. Dada la frecuencia respiratoria muy elevada y los dolores musculares intensos, lo clasificaría como coronavirus COVID-19. Por otro lado, si el dolor de cabeza es persistente, el mareo es repentino y de larga duración, y el análisis da positivo al H1N1, entonces sería gripe clase A."

**Tabla CCV:**

| Concepto | Característica | Valores |
|----------|---------------|---------|
| paciente | fiebre | superior a 38° |
| | tos | seca |
| | dolor de garganta | fuerte |
| | frecuencia respiratoria | muy elevada |
| | dolores musculares | intensos |
| | dolor de cabeza | persistente |
| mareo | tipo | repentino |
| | duración | larga |
| análisis de laboratorio | resultado | positivo al virus H1N1 |

**Reglas:**

```
SI  (paciente.fiebre = superior a 38°)
  Y (paciente.tos = seca)
  Y (paciente.dolor de garganta = fuerte)
  Y (paciente.frecuencia respiratoria = muy elevada)
  Y (paciente.dolores musculares = intensos)
ENTONCES asignar (diagnóstico, coronavirus COVID-19)

SI  (paciente.dolor de cabeza = persistente)
  Y (mareo.tipo = repentino)
  Y (mareo.duración = larga)
  Y (análisis de laboratorio.resultado = positivo al virus H1N1)
ENTONCES asignar (diagnóstico, gripe clase A)
```

---

## Trampas del examen

- El AP captura conocimiento **implícito**, no explícito
- Las 4 etapas en orden: **Grabación → Transcripción → Codificación → Interpretación**
- Los sinónimos **NO tienen características propias** y **NO se relacionan entre sí**
- Los conceptos-estado **NO tienen características** en la tabla CCV
- Las reglas se escriben siempre como `SI (C.Caract = Valor) ENTONCES (resultado)`
- El conocimiento procedimental está en la **Interpretación**; el declarativo en las demás etapas
- Si algo tiene características propias, es un **Concepto**, no una característica de otro concepto
- Todo lo implícito se **valida con el experto**
