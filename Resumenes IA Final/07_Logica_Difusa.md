# 07 — Lógica Difusa y Razonamiento Aproximado

> **Playlist:** Lógica / Razonamiento Aproximado y Lógica Difusa  
> **Objetivo:** Manejar incertidumbre e imprecisión en los sistemas inteligentes.

---

## Razonamiento Aproximado

Modelos que imitan cómo las personas toman decisiones ante información **imprecisa y/o incierta**, aplicando métodos para representar, combinar y propagar esa información con un **grado de certeza**.

### Incertidumbre vs Imprecisión

| Concepto | Definición | Ejemplos |
|----------|-----------|---------|
| **Incertidumbre** | Falta de seguridad/confianza sobre algo | Juegos de azar, bolsa de valores |
| **Imprecisión** | Vaguedad o desconocimiento del valor concreto | "el vaso está a la mitad" |

**Fuentes:**
- Características del mundo real: complejo, no determinista, falta de evidencias
- Deficiencias de información: incompleta, errónea, contradictoria
- Deficiencias del lenguaje o los modelos

### Métodos para tratar la incertidumbre

| Tipo | Métodos | Uso |
|------|---------|-----|
| **Cualitativos** | Razonamiento por defecto, teoría de justificadores | Solo para fundamentos teóricos, no prácticos |
| **Cuantitativos** | Probabilista clásico, Factores de certeza, **Lógica difusa**, Markov, Redes Bayesianas | Aplicaciones prácticas |

---

## Lógica Difusa

**Lógica tradicional:** solo 2 valores: Verdadero (1) o Falso (0)  
**Lógica polivalente:** 3 o más valores discretos → complejo de implementar  
**Lógica difusa:** valores **continuos** en el rango [0.0, 1.0]

### Conceptos clave

**Conjunto Difuso:** grupo de cosas que no puede definirse con precisión por la naturaleza vaga del concepto (ej: "temperatura alta").

**Función de pertenencia** μ_A(x): indica cuánto pertenece un elemento al conjunto A.
- μ_A(x) = 0.00 → no pertenece
- 0.00 < μ_A(x) < 1.00 → pertenencia parcial
- μ_A(x) = 1.00 → pertenencia total

> **Importante:** La función de pertenencia **no tiene sentido probabilístico**. No hay transición abrupta entre pertenecer y no pertenecer.

---

## Operadores de Lógica Difusa

| Operador | Símbolo | Fórmula |
|----------|---------|---------|
| **Negación** | ¬A = A' | μ_A'(x) = 1 - μ_A(x) |
| **Disyunción (OR)** | A ∨ B = A ∪ B | μ_(A∪B)(x) = max[μ_A(x), μ_B(x)] |
| **Conjunción (AND)** | A ∧ B = A ∩ B | μ_(A∩B)(x) = min[μ_A(x), μ_B(x)] |

### Implicación Difusa (SI A → ENTONCES B)

1. **Determinar entradas difusas del antecedente A:** calcular μ de cada función del antecedente
2. **Aplicar operadores difusos:** resolver Y/O para obtener un único grado de pertenencia
3. **Propagar al consecuente B:** aplicar el mismo grado de pertenencia del antecedente al consecuente

---

## Sistemas Difusos

Aplican lógica difusa para representar datos imprecisos y aplicar reglas que consideran esa imprecisión al tomar decisiones.

**Arquitectura:** similar a un SBC + módulo de **codificación** (fuzzification) + módulo de **decodificación** (defuzzification).

- Reglas en la BC pueden venir de fuentes públicas o privadas
- Si vienen de un experto → **Sistema Difuso Experto**

### Dos modelos principales:

#### Modelo Mamdani
**Más simple** pero requiere más reglas para problemas complejos.

**Funcionamiento:**
1. Identificar todas las reglas aplicables
2. Calcular el valor de pertenencia del consecuente de cada regla (con operadores difusos)
3. Combinar los valores con:
   - **Centro de masa:** resultado ponderado por área bajo la curva
   - **Promedio del máximo:** promedio de los valores con máxima pertenencia

#### Modelo Takagi-Sugeno
Requiere menos reglas para problemas complejos o no-lineales.

**Funcionamiento:**
1. Identificar todas las reglas aplicables
2. Calcular el consecuente de cada regla i con una **función lineal:**  
   `y_i = a_0 + a_1*x_1 + a_2*x_2 + ...`
3. Combinar usando **media ponderada:**  
   `y = Σ(μ_i × y_i) / Σ(μ_i)`

---

## Críticas a los Sistemas Difusos

1. **Capacidad de aprendizaje limitada** (no aprenden solos)
2. Tiende a funcionar peor que un modelo matemático exacto (aunque si no existe uno, es buena alternativa)
3. Al combinar reglas, **no se refuerzan entre sí** (agregar más reglas no aumenta la credibilidad)

**Solución:** Sistemas **neurodifusos** (combinan RNA con lógica difusa para agregar capacidad de aprendizaje).

---

## Resumen clave para el final

1. La lógica difusa maneja **valores continuos** [0,1] en lugar de solo verdadero/falso.
2. **Función de pertenencia** μ_A(x): qué tan perteneciente es x al conjunto A (no es probabilidad).
3. Operadores: negación (1-μ), disyunción (max), conjunción (min).
4. La implicación difusa: calcular pertenencia del antecedente → propagar al consecuente.
5. **Mamdani:** más simple, más reglas. **Takagi-Sugeno:** menos reglas, usa función lineal.
6. Los sistemas difusos **no aprenden** → solución: sistemas neurodifusos.
7. Si no hay modelo matemático disponible, la lógica difusa es una buena alternativa.
