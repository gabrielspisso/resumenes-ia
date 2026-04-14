# 07 — Lógica Difusa y Razonamiento Aproximado

> **Playlist:** Lógica / Razonamiento Aproximado y Lógica Difusa  
> Fuente: Clase 6, Para el Coloquio

---

## ¿Por qué usar Lógica en IA?

- **Representar conocimientos:** educidos de un experto para volcarlos en la base de conocimientos
- **Realizar deducciones:** necesarias para el motor de inferencias en el SBC/SET

---

## Tipos de Lógica

| Tipo | Valores | Uso en IA |
|------|---------|-----------|
| **Lógica Proposicional** | Verdadero / Falso | Solo para representar hechos simples. Demasiado limitada para IA |
| **Lógica de Primer Orden** | Verdadero / Falso | Variables, constantes, funciones de verdad, cuantificadores (∀, ∃) |
| **Lógica Difusa** | Continuo [0.0, 1.0] | Manejo de imprecisión e incertidumbre |

---

## Lógica de Primer Orden (LPO)

**Componentes:**
- **Proposiciones:** representan hechos o conocimientos (poseen valor verdad V o F)
- **Operadores lógicos:** AND, OR, ENTONCES (→), SI Y SOLO SI (↔), Negación (¬)
- **Variables:** objetos indeterminados dentro de un dominio
- **Constantes:** objetos determinados
- **Funciones de verdad (predicados):** establecen una cualidad respecto de un objeto: `H(x)`, `P(x,y)`
- **Cuantificadores:** Para todo (∀), Existe (∃)

**Deducción Natural** — método para demostrar una tesis a partir de hipótesis usando reglas de inferencia:
- Cada fórmula está numerada y debe ser hipótesis o conclusión de reglas anteriores
- Solo se puede suponer UNA vez a lo largo del método

**Reglas principales:**
- Introducción a la implicación: suponer A → si se deduce B → se obtiene A → B
- Eliminación de la implicación (Modus Ponens): si A y A→B → entonces B
- Para todo (∀): si vale para cualquier variable genérica → vale para un elemento específico
- Existe (∃): si un elemento tiene una propiedad → existe un elemento que la cumple

---

## Razonamiento Aproximado

Modelos que imitan cómo las personas toman decisiones ante información **imprecisa y/o incierta**.

### Incertidumbre vs Imprecisión

| Concepto | Definición | Ejemplos |
|----------|-----------|---------|
| **Incertidumbre** | Falta de seguridad/confianza sobre algo | Juegos de azar, bolsa de valores |
| **Imprecisión** | Vaguedad o desconocimiento del valor concreto | "el vaso está a la mitad" |

**Fuentes:**
- Mundo real: complejo, no determinista, falta de evidencias
- Información deficiente: incompleta, errónea, contradictoria
- Deficiencias del lenguaje o los modelos

### Métodos para tratar la incertidumbre

| Tipo | Métodos | Aplicación |
|------|---------|-----------|
| **Cualitativos** | Razonamiento por defecto, teoría de justificadores | Solo fundamentos teóricos |
| **Cuantitativos** | Probabilista clásico, Factores de certeza, **Lógica difusa**, Markov, Redes Bayesianas | Aplicaciones prácticas |

---

## Lógica Difusa

**Lógica tradicional:** solo 2 valores: Verdadero (1) o Falso (0)  
**Lógica difusa:** valores **continuos** en el rango **[0.0, 1.0]**

### Conjunto Difuso

Grupo de cosas que no puede definirse con precisión por la naturaleza vaga del concepto.  
*Ejemplo: "temperatura alta" → no hay un corte exacto entre "alta" y "no alta".*

**Función de pertenencia μ_A(x):** indica cuánto pertenece el elemento x al conjunto difuso A.

| Valor μ | Significado |
|---------|-------------|
| μ_A(x) = 0.00 | No pertenece al conjunto |
| 0 < μ_A(x) < 1 | Pertenencia parcial |
| μ_A(x) = 1.00 | Pertenencia total |

> **IMPORTANTE:** La función de pertenencia **NO tiene sentido probabilístico**. No es una probabilidad. No hay transición abrupta.

---

## Operadores de Lógica Difusa

| Operador | Símbolo | Fórmula |
|----------|---------|---------|
| **Negación** | ¬A = A' | μ_A'(x) = **1 - μ_A(x)** |
| **Disyunción (OR)** | A ∨ B = A ∪ B | μ_(A∪B)(x) = **max[μ_A(x), μ_B(x)]** |
| **Conjunción (AND)** | A ∧ B = A ∩ B | μ_(A∩B)(x) = **min[μ_A(x), μ_B(x)]** |

---

## Implicación Difusa (SI A → ENTONCES B)

**Pasos:**
1. Calcular μ de cada función del antecedente A (una por cada término)
2. Aplicar operadores difusos (AND/OR) para obtener **un único grado de pertenencia** del antecedente
3. Propagar ese grado al consecuente B (el consecuente toma ese valor como máximo)

---

## Sistemas Difusos

Aplican lógica difusa para representar datos imprecisos y tomar decisiones.

**Arquitectura similar a SBC** con módulos extra:
- **Fuzzification (codificación):** convierte los valores de entrada en grados de pertenencia
- **Base de reglas difusas**
- **Motor de inferencia difuso**
- **Defuzzification (decodificación):** convierte el resultado difuso en un valor concreto

> Si las reglas vienen de un experto → **Sistema Difuso Experto**

---

## Modelo Mamdani

**Más simple** pero requiere más reglas para problemas complejos.

**Proceso:**
1. Identificar todas las reglas aplicables
2. Para cada regla: calcular el grado de pertenencia del antecedente (usando AND/OR)
3. El consecuente de cada regla toma ese grado de pertenencia
4. Combinar los consecuentes con uno de estos métodos:
   - **Centro de masa:** resultado ponderado por el área bajo la curva (más preciso)
   - **Promedio del máximo:** promedio de los valores con máxima pertenencia (más simple)

---

## Modelo Takagi-Sugeno

Requiere **menos reglas** para problemas complejos o no lineales.

**Diferencia clave:** el consecuente no es un conjunto difuso sino una **función lineal** de las entradas.

**Proceso:**
1. Identificar todas las reglas aplicables
2. Para cada regla i, calcular el consecuente con la función lineal:  
   `y_i = a_0 + a_1×x_1 + a_2×x_2 + ...`
3. Combinar usando **media ponderada:**  
   `y = Σ(μ_i × y_i) / Σ(μ_i)`

---

## Comparación Mamdani vs Takagi-Sugeno

| Aspecto | Mamdani | Takagi-Sugeno |
|---------|---------|--------------|
| **Complejidad** | Más simple de entender | Más complejo |
| **Reglas necesarias** | Más reglas para problemas complejos | Menos reglas |
| **Consecuente** | Conjunto difuso | Función lineal |
| **Defuzzificación** | Necesaria (centro de masa o promedio del máximo) | Media ponderada directa |
| **Uso** | Problemas simples | Problemas no lineales complejos |

---

## Críticas a los Sistemas Difusos

1. **Sin capacidad de aprendizaje** (no aprenden solos de los datos)
2. Funcionan peor que un modelo matemático exacto (cuando existe uno)
3. Al combinar reglas, **no se refuerzan entre sí** (más reglas ≠ más certeza)

**Solución:** Sistemas **neurodifusos** — combinan RNA con lógica difusa para agregar capacidad de aprendizaje.

---

## Trampas del examen

- La función de pertenencia **NO es una probabilidad**
- Negación: `1 - μ`, Disyunción: `max`, Conjunción: `min`
- **Mamdani:** más simple, más reglas; necesita defuzzificación
- **Takagi-Sugeno:** menos reglas, consecuente es función lineal, usa media ponderada directa
- Los sistemas difusos **no aprenden** → para aprendizaje → sistemas neurodifusos
- Si no hay modelo matemático exacto disponible, la lógica difusa es una buena alternativa
- La Lógica Proposicional es demasiado limitada para IA real → se usa LPO o Lógica Difusa
