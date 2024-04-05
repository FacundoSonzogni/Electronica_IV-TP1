# Informe de Desarrollo de una Unidad Aritmética Lógica (ALU) de 16 bits

Electrónica IV - Trabajo Práctico Nº1 - 2024 - Automatismos y Máquinas Elementales

## Introducción

Se quiere diseñar una **ALU (Unidad Aritmética Lógica)**, la cual se entiende como un elemento cuya función principal es realizar operaciones aritméticas y lógicas en datos que son enviados desde y hacia la memoria de una determinada máquina.

En particular, en este caso, se tendrán 2 entradas (A y B), cada una de 16 bits, y la ALU posee 6 modos de operación, los cuales dependen de tres señales de 1 bit que se usan como selectoras 
*invB:* Invierte la señal B, cuando toma el valor 1 y NO invierte a B si su valor es 0; 
*logico:* Si su valor es 0, se realiza una operación aritmética entre A y B, y sis u valor es 1, se realiza una operación lógica; 
*and:* Si su valor es 1 se hace una operación de AND entre A y B, y si su valor es 0, se hace una OR (siempre que *logico = 1*).

En conclusión, se debe diseñar una ALU que tenga las siguientes configuaraciones para las señales de control, que permiten ejecutar cada una de las operaciones soportadas por la ALU:

        **** (TABLA DE LA ALU)******

## Metodología de trabajo

En este caso, el diseño del esquemático es sencillo: Constará de un multiplexor (que hará las veces de un *"if"*), cuya señal de selección será la concatenación de *invB* & *logico* & *and*. Luego, la salida "*R*", tomará el valor de la suma, resta, AND u OR de las entradas, en función del valor de la señal de selección (de 3 bits), de acuerdo a la tabla expuesta en la sección anterior

Luego, simplemente, debemos diseñar los bloques que realizan las operaciones soportadas por la ALU. Sin embargo, éstas operaciones son elementales y el simulador *Digital* ya cuenta con bloques específicos para realizar dichas tareas. A continuación se comenta brevemente el diseño:

- **OPERACIONES LÓGICAS:** Simplemente constan de compuertas AND y OR, en las cuales una de las entradas (señal B) puede o no estar negada, de acuerdo al valor de *invB*.
- **BLOQUE SUMADOR:** El simulador cuenta con un sumador. La única observación que se debe hacer es que en la entrada C del mismo, se debe colocar un valor constante de 0 para que no se afecte el resultado de la suma, según se explica en la descripción del propio componente.
- **BLOQUE RESTADOR:** Para implementar el restador, consideraremos que podemos obtener A-B, sumandole a A el *Complemento a 2 de la señal B*. Luego, recordando que el complemento a 2 de un número binario puede encontrarse intercambiando todos los 1 por 0 y los 0 por 1 (es decir, una NOT) y al resulatdo sumarle 1. Así, podemos escribir lo siguiente:

                                A - B = A + C2(B) = A + (not B + 1)

De modo que podemos diseñar el restador usando el bloque sumador en el cual se ingresa la señal A, la señal B negada, y se coloca la entrada C del componente a un valor constante de 1.

## Resultados

A continuación se expone el esquemático correspondiente a las especificaciones anteriores:

         ***** (ESQUEMÁTICO DE LA ALU) ****

Notamos que el multiplexor permite como señal selectora a UNA señal de 3 bits y NO a 3 señales de 1 bit cada una (como es en este caso). Luego, para salvar esta situación, simplemente se realiza una concatenación de las 3 señales *invB*, *logico*, *and*, con el componente Divisor/Agregador proporcionado por el programa

## Conclusiones

Se realizó una simulación del esquemático de la ALU con el programa *Digital* y se comprobó que la misma funciona correctamente de acuerdo a las especificaciones.

*¿Qué tipo de Máquina es la Unidad Aritmética Lógica?*
Para responder esta pregunta, debemos tener en cuenta la siguiente:

- **AUTOMATISMO:** Un automatismo es un elemento que es capaz de ejecutar alguna secuencia de operaciones sin la necesidad de una intervención manual. Los automatismos están diseñados para realizar tareas específicas de forma repetitiva y predecible, siguiendo un conjunto de instrucciones o reglas preestablecidas.
- **MÁQUINA ELEMENTAL:** Una máquina elemental es un dispositivo mecánico simple que realiza una función básica o elemental. No necesariamente implica la automatización.Las máquinas elementales generalmente tienen una funcionalidad específica.
- **COMPUTADORA:** Una computadora es una máquina que es capaz de realizar varias tareas y puede cambiar de programa. 

Una ALU es, en realidad, una de las partes de una Máquina Elemental. Además NO permite cambiar de programa por lo que no es una Computadora. Se concluye, entonces, que se trata de un *Automatismo*, pues ejecuta instrucciones sencillas de manera automática.