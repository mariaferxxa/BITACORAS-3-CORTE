# INTRODUCCIÓN
El diseño de controladores PID en lazo cerrado representa una metodología poderosa y frecuentemente utilizada en la industria. A diferencia del enfoque en lazo abierto, este método parte de pruebas realizadas con el sistema en operación bajo retroalimentación. Esto permite capturar de forma directa el comportamiento del sistema en condiciones reales de funcionamiento, mejorando la calidad del ajuste del controlador.
El objetivo es identificar parámetros característicos como la ganancia última (Ku) y el período último (Pu), a partir de los cuales se calcula la configuración del controlador PID utilizando reglas empíricas como las de Ziegler & Nichols. Asimismo, se abordan variantes como el método del relé y estrategias de protección como el anti wind-up.

## CONCEPTOS CLAVE

Lazo cerrado: Sistema con retroalimentación activa.

Marginalmente estable: Estado de oscilación sostenida sin crecimiento ni decrecimiento.

Ganancia última (): Ganancia que produce oscilación sostenida.

Periodo último (): Tiempo de un ciclo de oscilación sostenida.

Ziegler & Nichols: Método de sintonización empírica basado en oscilaciones.

Relé con histéresis: Controlador binario usado para forzar oscilaciones.

Wind-up: Acumulación de la acción integral durante saturación.

Anti wind-up: Técnicas para evitar el sobreacumulamiento de la acción integral.

Frecuencia de oscilación (): Utilizada para calcular .

Estado estacionario: Condición donde el sistema se estabiliza tras una perturbación.

## DISEÑO EN LAZO CERRADO

En este enfoque, se realiza la sintonización directamente sobre el sistema cerrado. Esto implica:
-Forzar al sistema a oscilar de manera controlada.

-Medir las características de esa oscilación (frecuencia y amplitud).

-Calcular los parámetros del controlador a partir de esas mediciones.

Este método proporciona un diagnóstico más directo y útil de la estabilidad y comportamiento dinámico real del sistema.

## MÉTODO DE ZIEGLER & NICHOLS (CICLO ÚLTIMO)

Este método empírico consiste en:

Llevar a cero los parámetros del controlador PID (solo usar ganancia proporcional).

Aumentar  hasta obtener una oscilación sostenida en la salida del sistema (estado marginalmente estable).

Medir el período de esa oscilación .

Registrar la ganancia utilizada en ese punto como .

Con esos valores se calculan los parámetros del controlador PID:

-P: 

-PI: 

-PID: 

Este método busca que la segunda oscilación de la respuesta sea aproximadamente 1/4 de la primera (criterio de caída de ¼).

## MÉTODO DEL RELÉ

Mejora el método anterior evitando forzar oscilaciones con altos valores de ganancia. Utiliza un relé con histéresis como controlador temporal. La metodología es:

-Medir el tiempo de respuesta en lazo abierto.

-Cerrar el lazo con un relé y esperar una oscilación sostenida.

-Medir el período de oscilación () y su amplitud ().

-Calcular la ganancia crítica  mediante la fórmula:

Permite diseñar controladores PI o PID de forma menos agresiva que con Ziegler & Nichols.

## FENÓMENO WIND-UP Y ANTI WIND-UP

El fenómeno wind-up ocurre cuando la acción integral del controlador continúa acumulando error aunque el actuador ya esté saturado, lo que retrasa o daña la respuesta del sistema.

Existen estrategias para mitigar este problema:

-Anti wind-up por saturación: Detiene la integración cuando el actuador está en sus límites.

-Integración condicional: Suspende la acción integral en condiciones específicas.

-Re-cálculo y seguimiento: Predice saturación del actuador y ajusta la acción integral progresivamente. Se usa un parámetro .

Estas estrategias mejoran la velocidad de recuperación del sistema y protegen los actuadores.

## CONCLUSIONES

El diseño de controladores PID en lazo cerrado permite una aproximación más realista y práctica a la sintonización de controladores, especialmente en entornos industriales. Métodos como el de Ziegler & Nichols siguen siendo vigentes por su simplicidad y efectividad.

El método del relé ofrece una alternativa segura que evita dañar componentes y permite calcular parámetros a partir de oscilaciones forzadas con controladores discontinuos. Además, es esencial considerar el fenómeno wind-up para evitar comportamientos ineficientes o peligrosos en sistemas con actuadores limitados.

Implementar técnicas anti wind-up, elegir correctamente el tipo de controlador (P, PI o PID) y basarse en datos experimentales reales son factores claves para lograr un sistema de control robusto, estable y eficaz.



