# INTRODUCCIÓN
El diseño de controladores PID en lazo cerrado representa una metodología poderosa y frecuentemente utilizada en la industria. A diferencia del enfoque en lazo abierto, este método parte de pruebas realizadas con el sistema en operación bajo retroalimentación. Esto permite capturar de forma directa el comportamiento del sistema en condiciones reales de funcionamiento, mejorando la calidad del ajuste del controlador.
El objetivo es identificar parámetros característicos como la ganancia última (Ku) y el período último (Pu), a partir de los cuales se calcula la configuración del controlador PID utilizando reglas empíricas como las de Ziegler & Nichols. Asimismo, se abordan variantes como el método del relé y estrategias de protección como el anti wind-up.

## CONCEPTOS CLAVE

> 🔑 **Lazo cerrado: Sistema con retroalimentación activa.**

> 🔑 **Marginalmente estable: Estado de oscilación sostenida sin crecimiento ni decrecimiento.**

> 🔑 **Ganancia última (): Ganancia que produce oscilación sostenida.**

> 🔑 **Periodo último (): Tiempo de un ciclo de oscilación sostenida.**

> 🔑 **Ziegler & Nichols: Método de sintonización empírica basado en oscilaciones.**

> 🔑 **Relé con histéresis: Controlador binario usado para forzar oscilaciones.**

> 🔑 **Wind-up: Acumulación de la acción integral durante saturación.**

> 🔑 **Anti wind-up: Técnicas para evitar el sobreacumulamiento de la acción integral.**

> 🔑 **Frecuencia de oscilación (): Utilizada para calcular .**

> 🔑 **Estado estacionario: Condición donde el sistema se estabiliza tras una perturbación.**

## DISEÑO EN LAZO CERRADO

En este enfoque, se realiza la sintonización directamente sobre el sistema cerrado. Esto implica:
-Forzar al sistema a oscilar de manera controlada.

-Medir las características de esa oscilación (frecuencia y amplitud).

-Calcular los parámetros del controlador a partir de esas mediciones.

Este método proporciona un diagnóstico más directo y útil de la estabilidad y comportamiento dinámico real del sistema.

## MÉTODO DE ZIEGLER & NICHOLS (CICLO ÚLTIMO)

Este método empírico consiste en:

Llevar a cero los parámetros del controlador PID (solo usar ganancia proporcional).

Aumentar $K_{p}$ hasta obtener una oscilación sostenida en la salida del sistema (estado marginalmente estable).

Medir el período de esa oscilación $P_{u}$ .

Registrar la ganancia utilizada en ese punto como $K_{u}$ .

Con esos valores se calculan los parámetros del controlador PID:

| tipo | Kp            | Ti                    | Td                  |  
|------|---------------|-----------------------|---------------------|
| P    | $$0.5K_{u}$$  | -                     | -                   |
| PI   | $$0.45K_{u}$$ | $$\frac{P_{u}}{1.2}$$ | -                   |  
| PID  | $$0.6K_{u}$$  | $$\frac{P_{u}}{2}$$   | $$\frac{P_{u}}{8}$$ |


Este método busca que la segunda oscilación de la respuesta sea aproximadamente 1/4 de la primera (criterio de caída de ¼).

## MÉTODO DEL RELÉ

Mejora el método anterior evitando forzar oscilaciones con altos valores de ganancia. Utiliza un relé con histéresis como controlador temporal. La metodología es:

-Medir el tiempo de respuesta en lazo abierto.

-Cerrar el lazo con un relé y esperar una oscilación sostenida.

-Medir el período de oscilación ($P_{u}$) y su amplitud ($A_{u}$).

-Calcular la ganancia crítica $K_{c}$ mediante la fórmula:

$$K_{c}=\frac{4d}{\pi\sqrt{A_u^{2}-\varepsilon^{2}}}$$

Permite diseñar controladores PI o PID de forma menos agresiva que con Ziegler & Nichols.

![image](https://github.com/user-attachments/assets/a8cb7da3-19a4-4f4d-8e3c-81512e13916a)

*Para un maximo sobre impulso menor al 10%

## FENÓMENO WIND-UP Y ANTI WIND-UP

El fenómeno wind-up ocurre cuando la acción integral del controlador continúa acumulando error incluso después de que el actuador ha alcanzado sus límites físicos de saturación. Esto provoca una respuesta lenta y excesiva del sistema, ya que el controlador sigue sumando error aunque ya no pueda ejercer más acción sobre el proceso.

Para evitar este efecto no deseado, se aplican diversas estrategias de anti wind-up:

### Anti wind-up por saturación de la acción integral:
Esta técnica interrumpe o bloquea la acumulación de la acción integral cuando la señal de control está fuera del rango permitido por el actuador. El integrador se "congela" temporalmente hasta que la señal vuelve a estar dentro de los límites. Es simple de implementar y evita que el error acumulado cause un sobreimpulso al recuperar el control.

### Anti wind-up por integración condicional:
En esta estrategia, la acción integral solo se activa si la salida del controlador está dentro de los límites o si su tendencia de salida se dirige hacia el interior del rango de operación. Esto evita que el integrador aumente el error acumulado durante la saturación y mejora el tiempo de recuperación. Sin embargo, puede generar discontinuidades o pulsos en la respuesta del sistema al reactivar la integración.

### Anti wind-up por recálculo y seguimiento: 
Se basa en estimar el modelo del actuador y ajustar la salida del integrador de manera proporcional a la diferencia entre la señal saturada y la deseada. Esto suaviza la transición y suspende la integración progresivamente, en lugar de hacerlo de forma abrupta. El parámetro $T_{t}=T_{i}T_{d}$ regula la velocidad de corrección del error integral. Esta es una estrategia avanzada que mejora la precisión y reduce oscilaciones en la recuperación.

Efectos del anti wind-up:

-Previene el retardo excesivo en la recuperación del sistema después de una saturación.

-Disminuye el sobreimpulso y mejora el tiempo de establecimiento.

-Protege al actuador al evitar comandos de control fuera de sus límites.

-Mejora la estabilidad del sistema en presencia de grandes perturbaciones o referencias abruptas.

Estas estrategias son esenciales en sistemas reales donde los actuadores tienen límites físicos definidos y los errores pueden ser grandes, como en válvulas, motores o fuentes de potencia.

### Ejemplo
#### ejemplo 1
- Se determina analiticamente que $-(\omega)^{2}+11$ es la parte imaginaria y $6\omega^{2}+6+k_{p}$ es la parte real. Calcular Pu, Ku, y calcular el PID resultante

  $$P_{u}=\frac{2\pi}{\omega}=\frac{2\pi}{\sqrt{11}}=1.894s$$

  $$6\omega^{2}+6+k_{p}=0$$

  $$k_{p}=6\omega^{2}-6$$

  $$k_{p}=6(11)-6=60=k_{u}$$

ahora se calcula el PID

$$k_{p}=0.6*60=36$$

$$\frac{P_{u}}{1.2}=\frac{1.894}{2}=0.947$$

$$\frac{P_{u}}{1.2}=\frac{1.894}{8}=0.236$$

#### Ejemplo 2



## CONCLUSIONES

El diseño de controladores PID en lazo cerrado permite una aproximación más realista y práctica a la sintonización de controladores, especialmente en entornos industriales. Métodos como el de Ziegler & Nichols siguen siendo vigentes por su simplicidad y efectividad.

El método del relé ofrece una alternativa segura que evita dañar componentes y permite calcular parámetros a partir de oscilaciones forzadas con controladores discontinuos. Además, es esencial considerar el fenómeno wind-up para evitar comportamientos ineficientes o peligrosos en sistemas con actuadores limitados.

La implementación de técnicas anti wind-up (ya sea por saturación, integración condicional o recálculo y seguimiento) mejora significativamente la respuesta del sistema, garantizando estabilidad, protección de los actuadores y una recuperación más eficiente ante condiciones extremas.



