# 08 — Implementación de Sistemas Inteligentes

> **Playlist:** Implementación de Sistemas Inteligentes  
> **Objetivo:** Proceso completo para construir e implementar un Sistema Inteligente en la práctica.

---

## SW Tradicional vs Sistema Inteligente

| Aspecto | SW Tradicional | Sistema Inteligente |
|---------|---------------|-------------------|
| **Objetivo** | Construir un sistema software | Construir un SI |
| **Requerimientos** | Deseos y necesidades, características del dominio | Características de la tarea/problema, conocimientos (públicos y privados) |
| **Stakeholders** | Directivos, gerentes, usuarios | + **Expertos** |
| **Tecnología** | Hardware, paradigmas tradicionales | Modelos de IA, arquitecturas tradicionales, IC & ML |
| **Mantenimiento** | Correctivo, Adaptativo | **Perfectivo** |
| **Implementación** | Algorítmica (procedural) | **Declarativa** |

---

## Fases de la Implementación de un SI

```
Definición del problema
        ↓
Identificación y transformación de datos
        ↓
Selección de la tecnología
        ↓
Construcción del modelo
        ↓
Aplicación del sistema inteligente
```

---

## Fase 1: Definición del Problema

### 1.1 Elicitar Requerimientos

**Identificar fuentes de información:**

- **Recursos propios:** DB, formularios, manuales, políticas, actas de reuniones
- **Recursos externos:** datos públicos, estándares, leyes, libros
- **Stakeholders:** grupos de interés impactados (formales e informales)

**Recolectar hechos y necesidades:**

| Técnica | Tipo |
|---------|------|
| Análisis de documentación, datos | Extracción |
| Entrevistas, cuestionarios, prototipado, observación, tormenta de ideas, **emparrillado**, **análisis de protocolos** | Educción |

Preguntas clave a responder:
- ¿Qué incluye el problema? → **Elementos**
- ¿Dónde se produce? → **Contexto**
- ¿A quiénes afecta? → **Nuevos stakeholders**
- ¿Por qué resolverlo? → **Metas y expectativas**
- ¿Cómo se manifiesta? → **Escenarios**
- ¿Qué puede impedir resolverlo? → **Restricciones**

### 1.2 Comprender los Requerimientos

| Técnica | Qué permite |
|---------|-------------|
| **Abstraer** | Ignorar diferencias entre conceptos similares → panorama general |
| **Descomponer** | Dividir en partes más simples (las partes no son independientes) |
| **Proyectar** | Identificar distintas visiones del mismo problema (pueden ser inconsistentes) |
| **Modularizar** | Combinar elementos en módulos estables y reutilizables |

---

## Fase 2: Identificación y Transformación de Datos

### Integración
Unificar datos en una única tabla para facilitar administración y uso.

### Limpieza
Corregir valores nulos, incompletos, con errores o ruido. En columnas (atributos) y filas (ejemplos).

Acciones posibles: asignar nuevo valor, eliminar ejemplo, eliminar atributo.

### Formateo — Tipos de atributos y transformaciones

**Tipos:**
- **Continuos (numéricos):** binarios, enteros, decimales
- **Discretos (no numéricos):** lógicos, alfanuméricos, fecha/hora

**Transformaciones clave:**

| De | A | Cómo |
|----|---|------|
| Continuo | Discreto | Discretización por criterios |
| Discreto alfanumérico | Continuo | Código numérico único por valor, o atributo binario por cada valor |
| Discreto fecha/hora | Continuo | Separar en día/mes/año, calcular días desde fecha fija, asignar código numérico |

**Normalización / estandarización** de atributos numéricos (usando promedio y varianza).

> **Regla de oro:** Si normalizás durante el desarrollo, debés normalizar también en producción.

---

## Fase 3: Selección de la Tecnología

| Situación | Tecnología a usar |
|-----------|------------------|
| Datos disponibles y quiero aprender automáticamente | **ML** |
| No hay datos, pero hay reglas representativas | ML, IA Tradicional, IC |
| No hay datos ni reglas, pero hay heurísticas | **IC (Algoritmos Genéticos)** |

**Tabla de tecnología por tarea:**

| Tarea | ML | IA Tradicional | IC |
|-------|----|--------------|----|
| Optimización | — | — | **Algoritmos Genéticos** |
| Regresión | Algoritmos de regresión (supervisado) | — | — |
| Reglas de asociación | Algoritmos de inducción | — | — |
| Clasificación | RNA (supervisado) | SBC / SET | — |
| Predicción | RNA (supervisado) | SBC / SET | — |
| Clustering | RNA (no supervisado) | — | — |
| Detección de anomalías | RNA (no supervisado) | — | — |

---

## Fase 4: Construcción del Modelo

### Machine Learning
Datos → Algoritmo → Modelo → Entrenamiento → Validación → Prueba

**Prototipado & Experimentación:** entrenar → experimentar → analizar → reentrenar.

- **Entrenamiento:** aprender los pesos/reglas del modelo
- **Validación:** evaluar distintos parámetros para optimizar (en paralelo al entrenamiento)
- **Prueba:** evaluar capacidad de generalización con datos similares a producción

> **Cuidado:** no sobreentrenar (el modelo memoriza en vez de generalizar).

### IA Tradicional
- Identificar reglas y conceptos → volcarlos a la Base de Conocimientos
- La BdC es el modelo

### Inteligencia Computacional (Algoritmos Genéticos)
- Definir **cromosoma** (representación de la solución)
- Definir **función de aptitud** (evaluación de la solución)
- Ver buenas prácticas en módulo 03

---

## Fase 5: Aplicación del Sistema Inteligente

### 5.1 Integrar los modelos (Pipeline)
Determinar cómo ejecutar en producción todas las acciones del SI de forma integrada:
1. Recolección de datos
2. Preparación de datos
3. Ejecución del modelo
4. Ajuste de resultados

> **Regla de oro:** Siempre realizar en producción las **mismas acciones** de recolección y preparación que durante el desarrollo. De lo contrario, el modelo puede tener comportamientos inesperados.

### 5.2 Integrar con sistemas externos y usuarios
Via interfaces (puede integrarse con sistemas existentes).

### 5.3 Instalación
Pruebas de aceptación con datos de producción.

### 5.4 Monitoreo
Verificar que el sistema no esté fallando.

### 5.5 Mantenimiento
Volver a aplicar las fases según sea necesario (mantenimiento **perfectivo**).

---

## Resumen clave para el final

1. El SI implementa de forma **declarativa**; el SW tradicional de forma **algorítmica**.
2. Las fases: **Definir problema → Transformar datos → Elegir tecnología → Construir modelo → Aplicar**.
3. Emparrillado y análisis de protocolos son técnicas de **educción** usadas en la fase 1.
4. **Selección de tecnología:**
   - Datos disponibles → ML
   - Reglas sin datos → IA Tradicional / IC
   - Solo heurísticas → AG (IC)
5. La regla de oro del pipeline: **mismas transformaciones en dev que en producción**.
6. Mantenimiento de SI = **perfectivo** (mejorar y evolucionar el sistema).
