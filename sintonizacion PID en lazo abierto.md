
# INTRODUCCIÓN
La sintonización de controladores PID en lazo abierto representa uno de los pilares fundamentales del control clásico. Este tipo de controladores, compuesto por tres acciones (proporcional, integral y derivativa), ha sido utilizado ampliamente desde sus primeras aplicaciones en el gobierno de buques en 1922 por Minorsky. El desarrollo de sus formas comerciales en la década de 1930 por Taylor Instrument Company marcó el inicio del control industrial automático.
Los controladores PID pueden configurarse bajo diferentes arquitecturas y deben sintonizarse para garantizar el rendimiento deseado del sistema. Existen diversos métodos de sintonización, desde los empíricos como Ziegler-Nichols, hasta los basados en criterios de optimización y funciones de costo.
## CONCEPTOS CLAVE

PID: Controlador con acciones proporcional, integral y derivativa.

Ganancia proporcional (): Intensidad de la acción frente al error actual.

Constante de tiempo integral (): Tiempo que tarda en corregir errores acumulados.

Constante derivativa (): Reacción frente a cambios bruscos del error.

Arquitectura paralela: Implementación clásica con suma directa de las tres acciones.

Ziegler-Nichols: Método empírico basado en la curva de reacción.

FOPDT: Modelo de primer orden con retardo ().

Función de costo: Medida para evaluar el error del sistema.

Caída de 1/4: Patrón buscado en respuestas oscilatorias controladas.

Prueba y error: Ajuste secuencial de las ganancias hasta lograr respuesta deseada.

## CONTROLADORES PID
Un controlador PID combina tres acciones fundamentales:

Proporcional (P): Amplifica el error en tiempo real para responder rápidamente.

Integral (I): Acumula el error para eliminar el error en estado estacionario.

Derivativa (D): Predice el comportamiento del error y reduce oscilaciones.

La acción de control se define como:
Cada término afecta de forma distinta la respuesta del sistema, y su combinación permite una regulación más fina y estable.

## ARQUITECTURAS PID

Se reconocen varias configuraciones clásicas:

Paralela: suma directa de las acciones P, I y D.

Ideal: expresada en términos de tiempo integral  y derivativo .

Serie: las acciones se concatenan en cascada.

Cada arquitectura tiene ventajas según el tipo de planta y facilidad de implementación.

## EFECTOS DE LAS ACCIONES DE CONTROL

Proporcional: Aumenta la rapidez pero puede generar sobreimpulso.

Integral: Elimina el error permanente pero puede ralentizar la respuesta.

Derivativa: Suaviza la respuesta, disminuyendo el sobreimpulso, pero puede generar ruido si se exagera.

## MÉTODOS DE SINTONIZACIÓN EN LAZO ABIERTO

### 4.1. Prueba y error:
Metodología más usada en la industria por su simplicidad:
Fijar , .
Ajustar  hasta lograr tiempo de establecimiento razonable.
Incrementar  hasta reducir error permanente.
Agregar  para reducir oscilaciones.
Ajustar nuevamente todos los parámetros de forma fina.
### 4.2. Ziegler & Nichols (curva de reacción):
Usa modelo tipo FOPDT identificado previamente:
Tablas permiten calcular los parámetros PID según el tipo de controlador:
P: 

PI: 

PID: 

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


