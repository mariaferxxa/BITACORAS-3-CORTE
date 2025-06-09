# Identificacion de sistemmas por curvas de reaccion
## Introduccion
En el diseño y sintonización de controladores, particularmente de los controladores PID, resulta indispensable conocer con suficiente precisión el comportamiento dinámico de la planta que se desea regular. Esta necesidad es clave para garantizar el rendimiento esperado del sistema en condiciones reales de operación. Debido a que en entornos industriales muchas veces no se dispone de un modelo matemático detallado o exacto del sistema, se recurre a diversas metodologías de identificación que permiten obtener modelos aproximados a partir de la observación de la respuesta del sistema ante entradas específicas. Estas técnicas de identificación pueden ser empíricas, de lazo abierto o cerrado, y permiten caracterizar de forma adecuada la dinámica de la planta, facilitando así la correcta elección de los parámetros del controlador.
## Conceptos claves
Modelo de sistema: representación matemática de un proceso físico.

Curva de reacción: respuesta temporal del sistema a un escalón.

Tiempo muerto (): retardo antes de que el sistema responda.

Constante de tiempo (): mide qué tan rápido responde el sistema.

Ganancia estática (): relación entre el cambio de salida y entrada.

Identificación empírica: obtención de modelos a partir de datos.

Sistema inestable: aquel que no regresa al equilibrio sin control.

Integrador: sistema cuya salida se acumula con el tiempo.

FOPDTI: modelo de primer orden con retardo y factor integrador.

IPDT: modelo de sistema integrador con tiempo muerto.

## Identificacion de sistemas
La identificación de sistemas es una técnica de análisis que permite construir modelos matemáticos de un sistema real a partir de datos experimentales. Esto implica aplicar una entrada conocida al sistema (como un escalón) y observar la salida para deducir cómo responde.
Se utiliza en procesos industriales, mecánicos, eléctricos y químicos, entre otros.
Técnicas más comunes:
Curvas de reacción (análisis temporal de la salida ante un escalón).
Identificación en lazo cerrado (con controlador en operación).
Análisis en frecuencia (respuesta a señales sinusoidales).
Modelos empíricos simples (fácil de implementar sin computadoras).
Métodos con inteligencia computacional (IA, machine learning).

## Procedimiento de sintonizacion 
Sintonizar un controlador consiste en ajustar sus parámetros para que la respuesta del sistema cumpla criterios deseados (rápida, estable, sin sobrepaso excesivo). El procedimiento general es:
Realizar una prueba en lazo abierto aplicando una señal escalón.
Obtener parámetros del sistema (ganancia, tiempo muerto, constante de tiempo) usando un método de identificación.
Usar esos parámetros para calcular los del controlador (por ejemplo, con tablas de Ziegler-Nichols).
Esto se puede hacer manualmente, con software especializado o directamente en el controlador industrial.

## Metodologias de tipo empirico
Las metodologías empíricas son aquellas que se basan en la observación y análisis de datos experimentales. No buscan precisión absoluta, sino una aproximación útil para diseño y control. No son prueba y error: requieren mediciones, estadística y análisis lógico.
Métodos destacados:

*Ziegler-Nichols:* traza tangente en punto de inflexión de la respuesta escalón para obtener los parámetros

*Miller:* método similar que usa el 63.2% del valor final para mayor repetibilidad.

*Métodos de dos puntos:* identifican parámetros basándose en dos puntos fijos de la curva, lo que reduce errores.

Se consideran fundamentales en control clásico debido a su simplicidad y aplicabilidad directa.

## Metodologias de identificacion en lazo abierto
Se realizan sin realimentación, observando cómo reacciona la planta a una entrada. El modelo resultante suele tener la forma:

$$G(s)=\frac{ke^{st_{0}}}{\tau s+1}$$

Donde:

k : ganancia estatica del sistema.

$\tau$: constante de tiempo (relacionada con la rapidez de respuesta).

$t_{0}$: retardo (tiempo muerto).

Requisitos:
El sistema debe ser estable sin control.
La respuesta al escalón debe ser suave, sin oscilaciones bruscas.
Estos métodos permiten calcular un modelo de primer orden con retardo, muy útil para controladores PID.

### Metodo Ziegler-Nichols
### Metodo Miller
### Metodo de dos puntos

## Sistemas inestables en lazo abierto
Hay sistemas que no se pueden operar sin retroalimentación, porque divergen o no regresan al equilibrio. Sin embargo, con precaución, se pueden identificar usando curvas de reacción y aproximaciones matemáticas.

Ejemplo típico: un motor DC en control de posición.

Este modelo incluye una acción integradora (el sistema acumula errores), lo que refleja mejor su comportamiento real.

## Aproximacion IPDT
IPDT (Integrating Plus Dead Time) se usa cuando la planta tiene un comportamiento netamente integrador: la salida sigue creciendo mientras la entrada se mantiene constante. Ejemplo: llenado de un tanque.

Modelo:

Identificación:

Se eligen 3 puntos temporales y se miden los valores correspondientes de entrada y salida.

Se aplican las fórmulas para obtener  y .

Esto permite diseñar controladores incluso en procesos lentos o acumulativos.

## Conclusiones
La identificación de sistemas es una herramienta esencial en el diseño de sistemas de control automático. Permite obtener modelos matemáticos que, aunque aproximados, resultan suficientes para lograr un control eficiente de procesos reales. A través de metodologías empíricas y técnicas de lazo abierto, es posible caracterizar dinámicamente una planta sin necesidad de conocer todas sus ecuaciones internas.

Los métodos como Ziegler-Nichols, Miller o los de dos puntos han demostrado ser eficaces en la práctica, especialmente en la industria, donde se prioriza la rapidez y la facilidad de implementación. Además, el uso de modelos como FOPDTI e IPDT amplía la aplicabilidad de estas técnicas a sistemas que presentan comportamientos integradores o inestables.

Por tanto, la correcta aplicación de estas metodologías no solo mejora la precisión del modelo, sino que facilita la selección adecuada de los parámetros de un controlador, lo cual se traduce en una respuesta más estable, rápida y eficiente del sistema ante perturbaciones o cambios en su entorno. Así, se concluye que dominar la identificación de sistemas es un paso fundamental en la formación de cualquier ingeniero de control.


