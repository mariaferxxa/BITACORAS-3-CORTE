# Identificacion de sistemas por curvas de reaccion
## Introduccion
En el diseño y sintonización de controladores, particularmente de los controladores PID, resulta indispensable conocer con suficiente precisión el comportamiento dinámico de la planta que se desea regular. Esta necesidad es clave para garantizar el rendimiento esperado del sistema en condiciones reales de operación. Debido a que en entornos industriales muchas veces no se dispone de un modelo matemático detallado o exacto del sistema, se recurre a diversas metodologías de identificación que permiten obtener modelos aproximados a partir de la observación de la respuesta del sistema ante entradas específicas. Estas técnicas de identificación pueden ser empíricas, de lazo abierto o cerrado, y permiten caracterizar de forma adecuada la dinámica de la planta, facilitando así la correcta elección de los parámetros del controlador.
## Conceptos claves
> 🔑 **Modelo de sistema: representación matemática de un proceso físico.**

> 🔑 **Curva de reacción: respuesta temporal del sistema a un escalón.**

> 🔑 **Tiempo muerto (to): retardo antes de que el sistema responda.**

> 🔑 **Constante de tiempo ($\tau$): mide qué tan rápido responde el sistema.**

> 🔑 **Ganancia estática (k): relación entre el cambio de salida y entrada.**

> 🔑 **Identificación empírica: obtención de modelos a partir de datos.**

> 🔑 **Sistema inestable: aquel que no regresa al equilibrio sin control.**

> 🔑 **Integrador: sistema cuya salida se acumula con el tiempo.**

> 🔑 **FOPDTI: modelo de primer orden con retardo y factor integrador.**

> 🔑 **IPDT: modelo de sistema integrador con tiempo muerto.**

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
![image](https://github.com/user-attachments/assets/18bf41a4-0f81-4d2d-a6a5-df1bce774eac)

Este es uno de los primeros métodos empíricos de identificación de sistemas, desarrollado por Ziegler y Nichols en los años 40. Su objetivo es modelar sistemas de tipo entrada escalón – salida sin necesidad de derivar un modelo matemático riguroso.
Funciona aplicando una entrada escalon al sistema y se registra la respuesta del sistema, luego de esto se traza una recta tangente en el punto de inflexion de esa curva. el punto donde esta recta intersecta el eje tiempo es el tiempo muerto $t_{m}$ 
El momento donde la curva alcanza un valor cercano al 100% de su cambio es $\tau'$ y la constante de tiempo se calcula como:

$$\tau=\tau' - t_{m}$$

y la ganancia estatica es:

$$K=\frac{\Delta y}{\Delta u}$$

el problema de este metodo es que no es repetible ante una misma prueba lo cual no es deseable

### Metodo Miller
![image](https://github.com/user-attachments/assets/5b1707c2-f092-48ed-828f-356a02109939)

El método de Miller es una mejora del método de Ziegler & Nichols para hacerlo más repetible y menos subjetivo.
A comparacion de Ziegler-Nichols, en lugar de estimar la contante de tiempo observando el 100% de la respuesta, miller usa el 63.2% del valor final

Estos metodos surgieron cuando no existian herramientas computacionales modernas y modelar un sistema requeria resolver ecuaciones diferenciales complejas a mano. 
Permitia hacer control sin conocer el modelo exacto del sistema

### Metodo de dos puntos
![image](https://github.com/user-attachments/assets/953ba115-df1d-4752-b8db-adb77f27d7df)

Aparece como una evolución del método de Ziegler & Nichols, ya que los métodos basados en la recta tangente (de un solo punto) pueden ser inexactos debido a la dificultad para identificar el punto de inflexión de forma precisa.

#### paso a paso:
- se aplica un escalon al sistema
- se registra la respuesta del sistema
- se identifican dos instantes de tiempo $t_{1}$ y $t_{2}$ , en donde la salida alcanza ciertos porcentajes de cambio total (estos porcentajes dependen del autor del metodo)
- A partir de estos dos tiempos, se usan las siguientes formulas para hallar: el tiempo muerto, constante de tiempo y la ganancia estatica
  
  $$\tau =At_{1}+Bt_{2}$$

$$t_{o} =Ct_{1}+Dt_{2}$$

$$K=\frac{\Delta y}{\Delta u}$$

##### Constantes

![image](https://github.com/user-attachments/assets/6b524145-6400-4d08-9ff4-8d05849026ed)

### Ejemplos
#### Ejemplo 1
¿Qué metodo tiene los porcentajes de 28.3% y 63.2%?
Se observan dos puntos de la curva escalon: al 28.3% del valor final en $t_{1}=2s$ y al 63.2% en $t_{2}=4s$. Aplicando el método y sus constantes halle la funcion de transferencia

$$\tau = (-1.5)(2)+(1.5)(4)=3 segundos$$

$$t_{0}=(1.5)(2)+(-0.5)(4)=1 segundos$$

$$K=\frac{\Delta y}{\Delta u}=\frac{5-0}{2-0}=2.5$$


### Metodo de 2 puntos Segundo orden
con este mismo metodo tambien es posible obtener funciones de transferencia de segundo mas el tiempo muerto, lo que cambian son las constantes y el modelo de la funcion de transferencia

$$G(s)=\frac{k*e^{-t_{o}s}}{(\tau s+1)(\tau s+1)}$$

![image](https://github.com/user-attachments/assets/43a1fe02-70f0-42be-9bd3-d8b2f0f45cd6)

#### EJEMPLO------------------------------------------------------------------

## Sistemas inestables en lazo abierto
Hay sistemas que no se pueden operar sin retroalimentación, porque divergen o no regresan al equilibrio. Sin embargo, con precaución, se pueden identificar usando curvas de reacción y aproximaciones matemáticas.

Ejemplo típico: un motor DC en control de posición.

$$G(s)=\frac{ke^{-t_{o}s}}{(\tau s+1)s}$$

Este modelo incluye una acción integradora (el sistema acumula errores), lo que refleja mejor su comportamiento real. El uso de modelos tipo FOPDTI permite representar adecuadamente estos procesos y diseñar controladores robustos que compensen dicha inestabilidad.

## Aproximacion IPDT
IPDT (Integrating Plus Dead Time) se usa cuando la planta tiene un comportamiento netamente integrador: la salida sigue creciendo mientras la entrada se mantiene constante. Ejemplo: llenado de un tanque.

Modelo:

$$G(s)=\frac{ke^{-t_{o}s}}{s}$$

Identificación:

-Se eligen 3 puntos temporales y se miden los valores correspondientes de entrada y salida.

-Se aplican las fórmulas para obtener K y $t_{o}$

$$K=\frac{O_{2}-O_{1}}{(I_{2}-I_{1})(T_{3}-T_{2})}$$

$$t_{0}=T_{2}-T_{1}$$

Esto permite diseñar controladores incluso en procesos lentos o acumulativos.

## Ejercicios
### Ejercicio 1
![image](https://github.com/user-attachments/assets/c75a16f8-e5f9-4924-bdd9-d029003c7143)

Dada la siguiente grafica, hallar las constantes por el método de Alfaro

El valor final es 4 por lo tanto:
$P2=4 * 0.75=3$

$P1=4 * 0.25 =1$

En la grafica los tiempos son
t1= 0.553 y t2=2.76

Ahora vamos a hallar los parametros

$$\tau = (-0.910)(0.553)+(0.910)(2.76)=2 $$

$$t_{0}=(1.262)(0.553)+(-0.262)(2.76)=-0.025$$

$$K=\frac{4-0}{1-0}=4$$

$$G(s)=4*\frac{e^{0.025s}}{2s+1}$$

### Ejercicio 2
![image](https://github.com/user-attachments/assets/abebc9d4-ece3-46ec-b7ea-451dae218028)

Obtener la funcion de tranferencia de segundo orden por el método de Ho

El valor final es 1.33 por lo tanto:
$P2=1.33 * 0.85=1.130$

$P1=1.33 * 0.35 =0.47$

En la grafica los tiempos son
t1= 1.23 y t2=4.7

Ahora vamos a hallar los parametros

$$\tau = (-0.463)(1.23)+(0.463)4.7)=1.606 $$

$$t_{0}=(1.574)(1.23)+(-0.574)(4.7)=-0.761$$

$$K=\frac{1.33-0}{1-0}=1.33$$

$$G(s)=\frac{1.33*e^{0.765s}}{2.58s^{2}+3.21s+1}$$

## Conclusiones
La identificación de sistemas es una herramienta esencial en el diseño de sistemas de control automático. Permite obtener modelos matemáticos que, aunque aproximados, resultan suficientes para lograr un control eficiente de procesos reales. A través de metodologías empíricas y técnicas de lazo abierto, es posible caracterizar dinámicamente una planta sin necesidad de conocer todas sus ecuaciones internas.

Los métodos como Ziegler-Nichols, Miller o los de dos puntos han demostrado ser eficaces en la práctica, especialmente en la industria, donde se prioriza la rapidez y la facilidad de implementación. Además, el uso de modelos como FOPDTI e IPDT amplía la aplicabilidad de estas técnicas a sistemas que presentan comportamientos integradores o inestables.

Por tanto, la correcta aplicación de estas metodologías no solo mejora la precisión del modelo, sino que facilita la selección adecuada de los parámetros de un controlador, lo cual se traduce en una respuesta más estable, rápida y eficiente del sistema ante perturbaciones o cambios en su entorno. Así, se concluye que dominar la identificación de sistemas es un paso fundamental en la formación de cualquier ingeniero de control.


