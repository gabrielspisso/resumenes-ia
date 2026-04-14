# 02 — Análisis de Protocolos

> **Playlist:** Análisis de Protocolos  
> **Objetivo:** Técnica de educción del conocimiento para extraer lo que un experto sabe pero no puede verbalizar fácilmente.

---

## ¿Qué es?

El experto **piensa en voz alta** mientras resuelve una tarea. Se graba todo lo que dice.  
**Ventaja clave:** revela procedimientos que el experto usa pero **no puede verbalizar conscientemente** (conocimiento tácito).

---

## Etapas

### 1. Grabación del Protocolo
1. El Ingeniero en Conocimientos (IC) explica el objetivo al experto
2. Puesta en situación: pequeños ejercicios para generar confianza
3. Registro: grabación real mientras el experto resuelve el problema

### 2. Transcripción
- El IC escucha la grabación y **transcribe segmentando** el protocolo
- Se agregan anotaciones sobre acciones del experto (consultó un libro, buscó en internet, etc.)
- No hay una única forma correcta de segmentar

### 3. Codificación
Se divide en 3 subetapas:

#### Subetapa 1: Conceptos, Características, Valores y Relaciones

| Elemento | Analogía DER | Descripción |
|----------|-------------|-------------|
| **Concepto** | Entidad | Sustantivos principales del dominio |
| **Característica** | Atributo | Cualidad propia de un concepto |
| **Valor** | Valor del atributo | El valor concreto de la característica |
| **Relación** | Relación | Vínculo entre conceptos o entre concepto y característica |
| **Operador** | — | Medio para pasar de un estado a otro más próximo de la solución |

**Ejemplo de análisis:**

> "El paciente presenta fiebre superior a 38°"

| Texto | Tipo |
|-------|------|
| paciente | Concepto |
| presenta | Relación |
| fiebre | Característica |
| superior a 38° | Valor |

> "El mareo fue repentino y de larga duración"

→ El mareo **no es una característica** porque tiene su propio tipo (repentino) y su propia duración → es un **Concepto** con características propias.

**Tabla CCV resultante:**

| Concepto | Característica | Valores |
|----------|---------------|---------|
| paciente | fiebre | superior a 38° |
| | dolor de garganta | fuerte |
| | tos | seca |
| | frecuencia respiratoria | muy elevada |
| | dolores musculares | intensos |
| | dolor de cabeza | persistente |
| mareo | (tipo) | repentino |
| | duración | larga |
| análisis de laboratorio | resultado | positivo al virus H1N1 |

> **Nota:** Características entre paréntesis = **implícitas** (el experto no las dice explícitamente; hay que preguntar).

**Dos formas de considerar los estados:**
- **Estados como conceptos:** coronavirus, gripe clase A son conceptos (sin atributo diagnóstico explícito)
- **Estados como valores:** coronavirus, gripe clase A son valores del atributo *diagnóstico* del paciente

Ambas son válidas, pero hay que elegir **una sola** y ser consistente.

**Relaciones implícitas** (solo entre conceptos):
- Si estados son conceptos: `paciente → tiene → coronavirus`, `paciente → sufre de → mareo`
- Si estados son valores: `paciente → sufre de → mareo`, `paciente → se realiza → análisis de laboratorio`
- **No hay relaciones implícitas entre sinónimos**

#### Subetapa 2: Identificación de la Búsqueda
Identificar:
- **Estados** por los que pasó el experto
- **Operadores** que utilizó
- **Condiciones** para llegar a cada estado

#### Subetapa 3: Sinónimos, Metacomentarios e Incertidumbres

| Elemento | Definición | Ejemplo |
|----------|-----------|---------|
| **Sinónimos** | Palabras distintas que refieren al mismo concepto | "paciente" y "persona" |
| **Metacomentario** | Comentario del experto que no aporta al razonamiento directo | "el paciente debe permanecer aislado por precaución" |
| **Incertidumbre** | Expresión de duda sobre el cambio de estado | "podríamos pensar que..." |

Formato de tabla para metacomentarios:

| Líneas | Metacomentario | Significado |
|--------|---------------|------------|
| [10-12] | "debe permanecer aislado..." | Referencia a la contagiosidad del COVID-19 |
| [13] | "en una segunda observación" | Indica subetapa del razonamiento |

### 4. Interpretación
Identificar las **reglas de razonamiento** en formato pseudocódigo:

```
SI (concepto.caracteristica = valor) Y (...)
ENTONCES asignar (atributo_objetivo, valor_resultado)
```

**Reglas del ejemplo:**

```
SI  (paciente.fiebre = superior a 38°) Y
    (paciente.dolor de garganta = fuerte) Y
    (paciente.tos = seca) Y
    (paciente.frecuencia respiratoria = muy elevada) Y
    (paciente.dolores musculares = intensos)
ENTONCES asignar (diagnóstico, coronavirus COVID-19)

SI  (paciente.dolor de cabeza = persistente) Y
    (mareo.tipo = repentino) Y
    (mareo.duración = larga) Y
    (análisis de laboratorio.resultado = positivo al virus H1N1)
ENTONCES asignar (diagnóstico, gripe clase A)
```

> **Importante:** Las reglas se tratan de forma **atómica** (independientes entre sí en esta etapa).

---

## Resumen clave para el final

1. El análisis de protocolos sirve para capturar conocimiento **implícito** del experto.
2. Las 4 etapas: **Grabación → Transcripción → Codificación → Interpretación**.
3. En codificación: identificar **Concepto / Característica / Valor / Relación / Operador**.
4. Los estados pueden ser **conceptos o valores**, no mezclar ambas visiones.
5. Las reglas se escriben como: `SI (concepto.caracteristica = valor) ENTONCES (diagnóstico = X)`.
6. Los **metacomentarios** no aportan al razonamiento; las **incertidumbres** indican duda en el cambio de estado.
