
# INTRODUCCIÓN
La sintonización de controladores PID en lazo abierto representa uno de los pilares fundamentales del control clásico. Este tipo de controladores, compuesto por tres acciones (proporcional, integral y derivativa), ha sido utilizado ampliamente desde sus primeras aplicaciones en el gobierno de buques en 1922 por Minorsky. El desarrollo de sus formas comerciales en la década de 1930 por Taylor Instrument Company marcó el inicio del control industrial automático.
Los controladores PID pueden configurarse bajo diferentes arquitecturas y deben sintonizarse para garantizar el rendimiento deseado del sistema. Existen diversos métodos de sintonización, desde los empíricos como Ziegler-Nichols, hasta los basados en criterios de optimización y funciones de costo.
## CONCEPTOS CLAVE

> 🔑 **PID: Controlador con acciones proporcional, integral y derivativa.**

> 🔑 **Ganancia proporcional (kp ): Intensidad de la acción frente al error actual.**

> 🔑 **Constante de tiempo integral (ki): Tiempo que tarda en corregir errores acumulados.**

> 🔑 **Constante derivativa (kd): Reacción frente a cambios bruscos del error.**

> 🔑 **Arquitectura paralela: Implementación clásica con suma directa de las tres acciones.**

> 🔑 **Ziegler-Nichols: Método empírico basado en la curva de reacción.**

> 🔑 **FOPDT: Modelo de primer orden con retardo ().**

> 🔑 **Caída de 1/4: Patrón buscado en respuestas oscilatorias controladas.**

> 🔑 **Prueba y error: Ajuste secuencial de las ganancias hasta lograr respuesta deseada.**

## CONTROLADORES PID
Un controlador PID combina tres acciones fundamentales:

Proporcional (P): Amplifica el error en tiempo real para responder rápidamente.

$$U(s)=k_{p}*E(s)$$

Integral (I): Acumula el error para eliminar el error en estado estacionario.

$$U(s)=k_{i}*\frac{E(s)}{s}$$

Derivativa (D): Predice el comportamiento del error y reduce oscilaciones.

$$U(s)=k_{d}*sE(s)$$

La acción de control se define como:
Cada término afecta de forma distinta la respuesta del sistema, y su combinación permite una regulación más fina y estable.

## ARQUITECTURAS PID

Se reconocen varias configuraciones clásicas:

### Paralela:
Es la suma directa de las acciones P, I y D.
![image](https://github.com/user-attachments/assets/454dbafe-9024-4438-ad13-8f11442fd61b)

#### Formula

$$U(s)=k_{p}E(s)+k_{i}\frac{E(s)}{s}+k_{d}s*E(s)$$

### Ideal:
Los bloques del PID están idealmente implementados sin ruido, sin retardo, sin saturación

![image](https://github.com/user-attachments/assets/32ef7d67-ee47-4888-afa6-bf143d3b10c6)

#### Formula

$$U(s)=k_{p}(E(s)+\frac{1}{T_{i}}\frac{E(s)}{s}+T_{d}s*E(s))$$

### Serie:
las acciones se concatenan en cascada.
![image](https://github.com/user-attachments/assets/9a756451-2e94-4220-a90b-02b0e67b0a99)

#### Formula

$$U(s)=((E(s)(1+T_{d}*s))k_{p})(1+\frac{1}{T_{i}s})$$

Cada arquitectura tiene ventajas según el tipo de planta y facilidad de implementación.

## EFECTOS DE LAS ACCIONES DE CONTROL

- Proporcional: Aumenta la rapidez pero puede generar sobreimpulso.

- Integral: Elimina el error permanente pero puede ralentizar la respuesta.
 
- Derivativa: Suaviza la respuesta, disminuyendo el sobreimpulso, pero puede generar ruido si se exagera.
  
## CRITERIOS DE DESEMPEÑO PARA DISEÑO DE PID
### Funciones de costo más utilizadas
Este es un método más técnico y matemático, ideal para usar en simulaciones o con sistemas complejos. Aquí, en lugar de ajustar a mano, se define una función de costo que mide qué tan bien está funcionando el sistema, y luego se busca minimizar esa función.

Se elige una función de costo que represente lo que se quiere optimizar. Por ejemplo:

-IE: mide el error acumulado.

-ISE: penaliza mucho los errores grandes (eleva el error al cuadrado).

-IAE: mide el total de errores sin importar su dirección.

-ITAE: penaliza más los errores que ocurren tarde en el tiempo (muy útil para mejorar estabilidad y rapidez).

Este método permite encontrar una configuración del PID más óptima y precisa, especialmente útil cuando se busca rendimiento profesional o cuando se trabaja en simulaciones donde el ajuste manual sería muy lento o ineficiente.

## MÉTODOS DE SINTONIZACIÓN EN LAZO ABIERTO

### 4.1. Prueba y error:
-Se inicia con solo la acción proporcional, se colocan las ganancias integral y derivativa en cero.

-Se ajusta la ganancia proporcional poco a poco hasta que el sistema responde con un tiempo de establecimiento aceptable, es decir, que llegue rápido al valor deseado.

-Luego, se activa la acción integral, aumentando su ganancia gradualmente hasta reducir o eliminar el error en estado estacionario (cuando la salida no llega exactamente a la referencia).

-Después, se ajusta la acción derivativa para reducir las oscilaciones y hacer el sistema más estable o menos ruidoso.

-Finalmente, se vuelven a ajustar finamente todas las ganancias hasta encontrar una respuesta equilibrada (sin mucho sobreimpulso, ni lentitud, ni oscilaciones excesivas).

Este método sirve para ajustar el comportamiento del sistema de manera práctica, sin necesidad de usar matemáticas avanzadas o simulaciones, aunque requiere experiencia y puede ser lento o impreciso.

### 4.2. Ziegler & Nichols (curva de reacción):
Usa modelo tipo FOPDT identificado previamente:
Tablas permiten calcular los parámetros PID según el tipo de controlador:

+---------------------+----------------------------+----------+----------+--+
| tipo de controlador | Kp                         | Ti       | Td       |  |
+---------------------+----------------------------+----------+----------+--+
| P                   | $\frac{\tau}{t_{o}K}$      | -        | -        |  |
+---------------------+----------------------------+----------+----------+--+
|                     | $ \frac{0.9\tau}{t_{o}K}$  | $3.3t_{o}$| -        |  |
+---------------------+----------------------------+----------+----------+--+
|                     |  $\frac{1.2\tau}{t_{o}K}$  | $2t_{o}$  | $0.5t_{o}$ |  |
+---------------------+----------------------------+----------+----------+--+




### 4.3. Cohen-Coon:
Proporciona mejor desempeño cuando el retardo no es muy dominante. Usa también parámetros  para definir:

 con expresiones que dependen de .

### 4.4. Coeficiente de ajustabilidad:
Utiliza un parámetro  para seleccionar reglas de sintonización específicas.

### 4.5. Smith y otros métodos:
Métodos adaptativos y reglas derivadas de análisis estadístico o simulación.
## CRITERIOS DE DESEMPEÑO

Para comparar respuestas y definir optimización, se utilizan funciones de costo:

IE (Integral del Error): 

ISE (Integral del Error Cuadrado): 

IAE (Integral del Error Absoluto): 

ITAE (Integral del Error Absoluto por el Tiempo): 

Estos criterios permiten cuantificar el desempeño del sistema y buscar un ajuste óptimo de los parámetros del controlador.

## CONCLUSIONES

La sintonización de controladores PID en lazo abierto es un proceso crucial para garantizar que un sistema de control tenga un desempeño adecuado frente a perturbaciones y cambios de referencia. A través de diversas metodologías, es posible ajustar los parámetros del controlador para obtener una respuesta rápida, precisa y estable.

Los métodos empíricos como Ziegler-Nichols y Cohen-Coon son de gran utilidad en ambientes industriales debido a su facilidad de implementación. Por otro lado, los criterios de optimización permiten lograr ajustes más finos, adaptados a especificaciones exigentes.

En resumen, comprender las acciones de control, elegir la arquitectura adecuada y aplicar un criterio de desempeño definido, son aspectos fundamentales para el diseño exitoso de sistemas de control automático.


