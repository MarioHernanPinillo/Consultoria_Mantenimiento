# Metodología: Matriz de Criticidad de Activos Industriales

## 1. Alcance y Objetivo
Establecer un método sistemático para jerarquizar los activos del contexto operacional, permitiendo priorizar los esfuerzos de mantenimiento, la asignación de recursos presupuestarios y la estructuración del plan de mantenimiento preventivo/predictivo, en cumplimiento con la norma ISO 55001.

## 2. Algoritmo de Evaluación de Riesgo (Criticidad)
La criticidad de cada activo se calcula evalúa bajo la fórmula de Riesgo Relativo:

$$Riesgo = Frecuencia \times Consecuencia$$

Donde la **Consecuencia** se desglosa en los siguientes factores de impacto operacional:

$$Consecuencia = (Impacto\ Operacional \times Flexibilidad) + Impacto\ Mantenimiento + Impacto\ SHA$$

## 3. Criterios de Ponderación

### A. Frecuencia de Fallas (FF)
* **Alta (Valor 4):** Más de 2 fallas al mes.
* **Media (Valor 3):** Entre 1 y 2 fallas por trimestre.
* **Baja (Valor 2):** Entre 1 y 2 fallas al año.
* **Excelente (Valor 1):** Menos de 1 falla al año.

### B. Matriz de Consecuencias (Factores)
* **Impacto Operacional (IO):** Parada total de planta (10) | Parada parcial (5) | No afecta la producción (1).
* **Flexibilidad (FL):** No existe equipo de respaldo / stand-by (2) | Existe respaldo inmediato (1).
* **Costo de Mantenimiento (CM):** Reparación costosa / requiere soporte externo (5) | Reparación menor / ejecutable por la cuadrilla interna (1).
* **Seguridad, Higiene y Ambiente (SHA):** Afectación severa al personal o infracción ambiental (10) | Sin impacto a personas o entorno (1).

## 4. Clasificación Final del Activo
* **Crítico (Riesgo > 40):** Requiere análisis FMEA inmediato y plan de mantenimiento predictivo prioritario.
* **Semicrítico (Riesgo entre 20 y 40):** Evaluado bajo mantenimiento preventivo sistemático.
* **No Crítico (Riesgo < 20):** Sujeto a estrategias de mantenimiento correctivo (run-to-failure) controlado.
