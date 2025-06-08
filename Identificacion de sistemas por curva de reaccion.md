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
