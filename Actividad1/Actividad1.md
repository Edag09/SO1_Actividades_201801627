# Kernel, Tipos y sus diferencias

[¿Que es un Kernel?](#kernel)

[Tipos de Kernel](#tipos)

[Diferencia entre los kernel](#diferencias)

[Diferencias entre User y Kernel Mode](#ukm)

## ¿Qué es un Kernel? <a id="kernel"></a>

El **kernel** es el núcleo de un sistema operativo y, por tanto, la interfaz entre el software y el hardware. Es por ello por lo que se está usando continuamente. En pocas palabras: el kernel es el corazón de un sistema operativo.

Sin embargo, no solo es el núcleo del sistema, sino también un programa que controla todos los accesos al procesador y a la memoria, es responsable de los drivers (controladores) más importantes y puede acceder directamente al hardware. Un kernel es la base de la interacción entre el hardware y el software y gestiona sus recursos de la forma más eficiente posible.

![Kernel](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Kernel_Layout.svg/1200px-Kernel_Layout.svg.png)


**¿Cómo funciona un Kernel?**

Las cuatro funciones del kernel pueden derivarse de sus componentes:

~~~
    Gestión del almacenamiento: controla cuánta memoria se utiliza y dónde.

    Gestión de procesos: determina qué procesos puede utilizar la CPU, cuándo y durante cuánto tiempo.

    Controlador de dispositivos: comunica el hardware con los procesos.

    Llamadas al sistema y seguridad: recibe peticiones de servicio de los procesos.
~~~

Las funciones de un kernel, cuando es implementado adecuadamente, permanecen invisibles para los usuarios. Funciona en su propio mundo, en el espacio del kernel. Los archivos, programas, juegos, navegadores, etc. en definitiva, todo lo que ve el usuario tiene lugar en el espacio del usuario. La interacción de ambos mundos se realiza a través de una interfaz de llamadas al sistema, el SCI.

**El kernel en el sistema operativo**

Para entender cómo funciona el kernel del sistema operativo, lo mejor es pensar que un ordenador está dividido en tres niveles:

1. **Hardware.** La base del sistema que consiste en la memoria, el procesador y los dispositivos de entrada y salida. La CPU realiza la lectura y escritura de código al igual que los cálculos que requiere la memoria.

1. **Kernel.** El núcleo de un sistema operativo. Indica a la CPU lo que debe hacer.

1. **Procesos de usuario.** Todos los procesos en ejecución que gestiona el kernel. El kernel permite la comunicación entre procesos y servidores, también conocida como comunicación entre procesos (IPC).

## Tipos de Kernel <a id="tipos"></a>

Existen diferentes tipos de kernel para diferentes sistemas operativos y dispositivos finales. Conforme a sus características, pueden dividirse en tres grupos

### Kernel Monolítico

<img src="https://slideplayer.es/slide/4085729/13/images/6/KERNEL+MONOL%C3%8DTICO.jpg" alt="Kernel Monolítico" width="300" height="200">

<br>

~~~
Es el tipo de kernel más antiguo y simple.

Contiene todas las funciones del sistema operativo en un solo bloque de código.

Las funciones y servicios se ejecutan en el espacio del kernel, lo que puede llevar a problemas de seguridad si un componente falla.

Ejemplos: Linux con el kernel estándar, versiones antiguas de Windows.
~~~

### Microkernel

<img src="https://www.researchgate.net/publication/304348982/figure/fig2/AS:376314398822401@1466731752472/Figura-3-Estructura-de-un-sistema-basado-en-microkernel.png" alt="Microkernel" width="400" height="250">

<br>

~~~
Se diseñó para abordar las limitaciones de los kernels monolíticos, dividiendo las funciones en módulos más pequeños y ejecutándolos en el espacio del usuario siempre que sea posible.

Los servicios básicos como la gestión de memoria y la planificación de procesos residen en el núcleo mínimo o microkernel, mientras que otros servicios se ejecutan como procesos separados.

Proporciona un entorno más seguro y estable, ya que los fallos en los módulos no afectarán directamente al núcleo.

Ejemplos: GNU Hurd, Minix.
~~~

### Kernel Híbrido


<img src="https://www.researchgate.net/publication/304348886/figure/fig1/AS:376315095076867@1466731918678/Figura-14-Estructura-de-un-sistema-basado-en-kernel-hibrido-El-desarrollo-de-los.png" alt="Kernel Híbrido" width="300" height="250">

<br>

~~~
Es una combinación de características del kernel monolítico y el basado en microkernel.

Algunas partes del sistema operativo se ejecutan en el espacio del kernel, mientras que otras se ejecutan en el espacio del usuario como servicios.

Permite un equilibrio entre la eficiencia del kernel monolítico y la robustez del basado en microkernel.

Ejemplo: Windows NT, macOS (XNU kernel).
~~~

## Diferencias de los tipos de Kernel <a id="diferencias"></a>

| Tipo | Estructura | Seguridad | Flesxibilidad |
|--- |--- |--- |--- |
| Monolítico | Todas las funciones y servicios se encuentran en un solo bloque de código en el espacio del kernel. | Los fallos en cualquier componente pueden afectar a todo el sistema, lo que puede representar un riesgo de seguridad. | Menos flexible, ya que todas las funciones están integradas en el kernel y no se pueden deshabilitar fácilmente. |
| Microkernel | Divide las funciones en módulos más pequeños, ejecutando algunos servicios en el espacio del usuario. | Los fallos en los módulos no afectan directamente al núcleo, lo que aumenta la estabilidad y seguridad del sistema. | Mayor flexibilidad, ya que los servicios pueden agregarse o eliminarse como procesos independientes. |
| Híbrido | Combina características de ambos, con partes ejecutándose en el espacio del kernel y otras en el espacio del usuario. | Ofrece un equilibrio entre eficiencia y seguridad, pero aún puede estar expuesto a problemas de seguridad inherentes a los kernels monolíticos. | Proporciona cierto grado de flexibilidad, pero en menor medida que un microkernel puro. |

<br>

## User vs Kernel Mode <a id="ukm"></a>

| Tipo | Privilegios | Recursos | Control de memoria | Excepciones y Errores |
|--- |--- |--- |--- |--- |
| User | En este modo, los programas y aplicaciones se ejecutan con un nivel de privilegios restringido. No tienen acceso directo al hardware ni a ciertas instrucciones sensibles del procesador. Cualquier intento de acceso a recursos críticos o instrucciones privilegiadas resultará en una excepción o error. | Los programas en este modo solo pueden acceder a recursos de manera indirecta a través del kernel, utilizando llamadas al sistema. Estas llamadas solicitan al kernel que realice operaciones en su nombre, como leer/escribir archivos, crear procesos, etc. | Los procesos en el modo usuario operan en su propio espacio de direcciones virtuales aislado, lo que significa que no pueden acceder directamente a la memoria de otros procesos. Esto proporciona una capa de protección y seguridad entre los diferentes procesos. | Cuando un programa en modo usuario intenta ejecutar una instrucción privilegiada o acceder a recursos restringidos, se genera una excepción o error que interrumpe la ejecución normal del programa. |
| Kernel Mode | En este modo, el kernel del sistema operativo y los controladores de dispositivo se ejecutan con el nivel de privilegios más alto. Tienen acceso completo a todos los recursos del hardware y pueden ejecutar todas las instrucciones del procesador, incluidas las más privilegiadas. | El kernel tiene acceso directo a todos los recursos del sistema, como memoria, dispositivos de hardware, registros del procesador y espacio de direcciones completo. |  El kernel opera en el espacio de direcciones del kernel, lo que le permite acceder a cualquier ubicación de memoria, incluidas las direcciones de memoria de los procesos en modo usuario. | El kernel puede manejar excepciones y errores directamente, ya que tiene los privilegios necesarios para hacerlo. |