# 📚 Resúmenes Clave para el Final


> Compilado de todos los resúmenes clave de cada tema.

---


## 01 - Conceptos Iniciales

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


---


## 03 - Algoritmos Genéticos

1. **Los AG son para optimización** con muchos parámetros, sin necesidad de datos históricos, cuando el espacio de soluciones es exponencialmente grande.

2. **El cromosoma codifica una solución**; el **fitness la evalúa**.

3. **Flujo**: **GPI → Selección → Cruzamiento → Mutación → ¿Paro?**

4. **Ruleta con control s/nro. esperado** = más completo (garantiza los buenos + variedad probabilística).

5. **La mutación evita la convergencia prematura** (máximos locales).

6. **En producción**:
   - Múltiples corridas con los mismos parámetros
   - Guardar logs de cada ciclo
   - Tomar el mejor individuo de todos los logs
   - Decodificar esa solución

7. **El algoritmo busca soluciones suficientemente buenas**, no necesariamente la mejor, lo que lo hace útil en espacios de búsqueda exponenciales.

8. **Importante**: distinguir entre **vueltas** (ciclos individuales) y **corridas** (ejecución completa).

---


---


## 04 - Redes Neuronales

1. **Lo único que cambia durante el entrenamiento son los pesos W** (no funciones, no estructura).
2. **Perceptrón:** 1 neurona, solo lineal, 1958. Alfa 0.05–0.30. Ajuste por `α × error × entrada`.
3. **Backpropagation:** multicapa, lineal y no lineal. Usa gradiente decreciente + error propagado hacia atrás. Función sigmoidal (derivable). Teorema de aproximación universal (pero cantidad de neuronas es empírica).
4. **Hopfield:** autoasociativa, aprende con `M = p^T × p` (tachar diagonal), converge cuando 2 ciclos iguales. Patrones deben ser ortogonales.
5. **CNN:** para imágenes. Usa filtros (pesos compartidos) → reduce parámetros de millones a miles. Etapas: convolución + ReLU + Max Pooling. Luego capas lineales.
6. **Normalización:** misma fórmula y parámetros en entrenamiento, validación, prueba Y producción (regla dorada).
7. **Mini-batch:** el método de procesamiento más eficiente para grandes volúmenes de datos (típico: 32-64 ejemplos).
8. **Underfitting:** pocas épocas. **Overfitting:** demasiadas épocas. **Early stopping** ayuda pero requiere verificación con datos de prueba.
9. **Fórmula de error:** MSE para salida continua (identidad); CrossEntropy para sigmoidal/softmax. Elegir mal causa que el error no baje.
10. **Algoritmo de optimización:** Adam funciona bien en la mayoría de casos; SGD es mejor para imágenes.

---


---


## 05 - Emparrillado

1. **Propósito:** El emparrillado captura cómo el experto **clasifica y diferencia** elementos del dominio mediante características bipolares.

2. **No es suficiente por sí sola:** No sirve para construir una Base de Conocimiento de manera independiente; necesita complementarse con otras técnicas de adquisición de conocimiento.

3. **Las 6 etapas:** 
   - Diálogo inicial
   - Identificación de elementos
   - Identificación de características
   - Diseño de la parrilla
   - **Formalización** (cálculos de distancias y dendrogramas)
   - **Interpretación** (análisis de árboles y relaciones)

4. **Tipos de parrilla:** Dicotómica, clasificatoria o evaluativa.

5. **Formalización:** Calcular matrices de distancias y construir dendrogramas para elementos y características usando el criterio de mínima (o máxima) distancia.

6. **Características especiales:** Para características, necesitas la parrilla original **y** la opuesta (d1 y d2 → tomar mínimo de cada par).

7. **Relaciones entre características:** Paralela / recíproca / ortogonal / ambigua / no tipificada (solo entre características del mismo grupo).

8. **Validación:** Los resultados deben discutirse y validarse con el experto.

---


---


## 06 - Métodos de Búsqueda

1. **Formalización:** todo problema se modela como estados + operadores + estado inicial + estados solución.

2. **Sin heurística (búsqueda ciega):** 
   - BFS (amplitud): garantiza solución óptima, usa mucha memoria
   - DFS (profundidad): usa poca memoria, no garantiza óptima
   - Generación y Prueba: encuentra todas las soluciones
   - Bidireccional: búsquedas simultáneas desde inicio y fin

3. **Con heurística (búsqueda informada):**
   - Escalada: sin retroceso, puede quedar en máximo local
   - Primero el Mejor: tiene retroceso, garantiza solución (no necesariamente óptima)
   - Beam Search: Primero el Mejor con LNA limitada a N nodos
   - A*: Primero el Mejor + costo acumulado. Óptima si heurística admisible

4. **Trade-off memoria-tiempo:** métodos heurísticos sacrifican exhaustividad (no garantizan óptima) para reducir memoria y tiempo dramáticamente.

5. **Función heurística:** crítica para el desempeño. Debe ser:
   - **Admisible** (para A*, no sobrestima)
   - **Informativa** (discrimina bien entre estados)
   - **Eficiente** de calcular

6. **Escalada:** sin retroceso, puede quedar en máximo local si función no es monotonamente creciente.

7. **Primero el Mejor:** tiene retroceso (LNA), garantiza encontrar solución, no requiere monotonía.

8. **A*:** equivalencia f(n) = g(n) + h(n). Óptimo si la heurística es admisible. Combina mejor lo mejor de información del dominio con costo del camino.

---


---


## 07 - Lógica Difusa

1. **Imprecisión vs Incertidumbre:** La imprecisión es vaguedad (qué tan preciso es un valor), la incertidumbre es duda sobre ocurrencia (no sé si pasará).

2. **Lógica difusa:** Usa valores continuos [0,1] para representar pertenencia a conjuntos vagos, en lugar de solo verdadero/falso.

3. **Función de pertenencia μ_A(x):** Qué tan perteneciente es x al conjunto A (NO es probabilidad, es grado de cualidad).

4. **Operadores:** Negación (1-μ), disyunción (max), conjunción (min), implicación (propagación de antecedente a consecuente).

5. **Implicación difusa:** Antecedente → calcular pertenencia única → propagar al consecuente.

6. **Mamdani:** Más simple, más reglas, defuzzificación por centro de masa o promedio del máximo.

7. **Takagi-Sugeno:** Menos reglas, usa función lineal, media ponderada para combinar.

8. **Sistemas difusos:** Combinan fuzzificación, motor de inferencias con reglas, y defuzzificación.

9. **Limitaciones:** No aprenden, peor que modelos exactos, reglas no se refuerzan, decisiones ambiguas.

10. **Solución:** Sistemas neurodifusos (RNA + lógica difusa) para agregar aprendizaje.

11. **Aplicabilidad:** Usar cuando NO hay modelo matemático disponible y los datos son imprecisos.

---


---


## 09 - PNL

1. PNL = IA + lingüística para que las máquinas entiendan y generen lenguaje humano.
2. **Lenguaje artificial** no necesita IA para procesarse; **lenguaje natural** sí.
3. Pipeline básico: **Tokenización → Normalización → Segmentación**.
4. **Lematización** → forma base (semántica); **Stemming** → raíz (morfología).
5. **NLU:** comprende texto; **NLG:** genera texto.
6. **Autocorrección** usa distancia de edición (Levenshtein); **Autocompletado** usa modelos n-gram.
7. NLP tradicional: simple pero limitado en ambigüedad y contexto.
8. NLP con ML: usa TF-IDF/GloVe para vectorizar, luego regresión/árboles/clustering.


---

