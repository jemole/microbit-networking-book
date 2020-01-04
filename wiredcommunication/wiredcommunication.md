Comunicación usando cables
==========================

![Chapter 1 image](chapter1.png)

Introducción
------------

¡Todo está conectado hoy en día! Ordenadores y dispositvos se conectan entre sí para formar redes. Y estas redes se conectan a su vez entre sí para formar la Internet. Cuando decimos *ordenadores* or *dispositivos*, nos referimos a cualquier cosa, desde un portátil o un teléfono, pasando por una lavadora o un sensor de humedad. Por supuesto, también puede ser tu micro:bit. Y es que, cada vez más, Internet se está convirtiendo en una *Internet de las Cosas* (*Internet of Things* o *IoT*).

En este capítulo vas a crear una red usando cables para conectar micro:bits. Y en el proceso trabajarás los siguientes conceptos:

- *medio de transmisión* y *señales*

- *binario* y *bit*

- *red*

### ¿Qué necesitas?

    2 micro:bits
    4 cables con conector tipo cocodrilo
    1 caja para las pilas y dos pilas AAA
    1 colega

Un poco de teoría...
--------------------

Para que dos micro:bits puedan enviarse mensajes tienen que estar conectadas de algún modo, bien mediante cables o de forma inalámbrica - a esto se le llama *medio de transmisión*.

Un mensaje puede ser un texto como “Hola”, un número como “9”, o un icono de una imagen. Las micro:bits convierten cada mensaje en una señal y la envían a través del *medio de transmisión*.

!!! hint "Definición 1: _Medio de transmisión_"
	Un medio de transmisión es el camino físico sobre el que se transmite una señal. 

!!! hint "Definición 2: _Señal_"
	Las señales son los voltajes electromagnéticos o las ondas que se transmiten en un medio físico cableado o inalámbrico. 

Por ejemplo, pensemos qué ocurre cuando decimos “Hola” a través de un teléfono fijo. El auricular del teléfono convierte los sonidos en una señal de voltaje eléctrico. Luego, esta señal se transmite al teléfono receptor por medio de cables; y en el receptor, se convierte nuevamente en sonido. 

!!! attention "Ejercicio 1"
	¿Cuál es el medio físico que hace posible la comunicación por radio?

Los ordenadores, y también la micro:bit, no pueden procesar señales sin convertirlas en datos binarios: 0s y 1s. Además, los datos binarios procesados por los ordenadores deben convertirse en señales antes de que puedan viajar por un medio de transmisión. 

!!! hint "Definición 3: _Bit_"
	Un bit es la unidad de datos más pequeña en una computadora. Es como un átomo. Un bit puede ser un 1 o un 0.

Un grupo de 8 bits es un *byte*. La Tabla \[tab:bit\] muestra otros ejemplos: 

|**Nombre** | **Tamaño**|
|---------|:--------|
|Byte (B) | 8 bits |
|Kilobyte (KB) | 1024 bytes |
|Megabyte (MB) | 1024 kilobytes |
| Gigabyte (GB) | 1024 megabytes |
| Terabyte (TB) | 1024 gigabytes |

Al conectar ordenadores o dispositivos a través de diferentes medios de transmisión se crean las redes. 

!!! hint "Definición 4: _Red_"
	Una red de ordenadores es una colección de ordenadores o dispositivos que están conectados para poder comunicarse entre sí. En una red de ordenadores hay, por tanto, al menos dos dispositivos. Ademas, dos o más redes pueden conectarse para formar una red más grande: una red de redes. ¡Internet es una red de redes gigante! 

En este capítulo vas a crear una red formada por dos micro:bits que se conectan a través de cables.

Programando mi red de micro:bits
--------------------------------

### Tarea 0: Los pines de la placa micro:bit

Antes de comenzar, como vamos a conectar nuestras micro:bits usando cables, es importante comprender bien para qué se usa cada uno de los pines de conexión. Para ello, lee el artículo [Los "pines" del BBC micro:bit](https://microbit.org/es/guide/hardware/pins/) y contesta las siguientes preguntas: 

- ¿Para qué se usan los pines 0, 1 y 2?
- ¿Para qué se usan los pines GND y 3V?


### Tarea 1: Conecta tus micro:bits y prueba a enviar datos

**Descripción:** Vas a conectar dos micro:bits usando cables, y utilizarás un programa para comprobar que la conexión funciona correctamente. 

**Instrucciones:**  Utilizando cables con conector cocodrilo, conecta el pin 3V entre las dos micro:bits, y conecta también el pin GND. Después, conecta el pin 1 de una micro:bit al pin 2 de la otra placa, y viceversa.  Ten cuidado al conectar los cables: dos de los cables van directos (3V-a-3V y GND-a-GND) pero los otros dos van cruzados (1-a-2 y 2-a-1).

En la figura se muestra un ejemplo. Mira los colores con cuidado (aunque quizá los colores que uses sean diferentes, tienen que hacer la misma conexión).

![Conectar dos micro:bits.Dos de los cabes se conectan de manera directa (3V-a-3V y GND-a-GND) pero los otros dos van cruzados (1-a-2 y 2-a-1).](Microbit_wired.png)

!!! note ""
	**Figura 1:** Conectar dos micro:bits. Dos de los cabes se conectan de manera directa (3V-a-3V y GND-a-GND) pero los otros dos van cruzados (1-a-2 y 2-a-1)


Para probar la conexión usa el programa de la figura; presiona el botón A en cada micro:bit y verifica que el LED se ilumina en la placa de tu colega. Hay que usar los bloques del menú *Pines*. Este menú está en *Avanzado*. Haz clic en el enlace *Más* para ver todas las opciones.


![Programa telégrafo: envía una señal por el Pin 1 al presionar botón A. Enciende el píxel (4,4) al recibir una señal en Pin 2](Telegrafo_base.png)
!!! note ""
	**Figura 2:** Programa para probar la conexión entre dos placas micro:bit Telegraph program. Al presionar el botón A, se envía una señal al otro lado utilizando el Pin 1. El micro:bit receptor escucha en el Pin 2 para verificar si se recibe una señal. Si hay una señal, se ilumina el píxel (4,4) en la pantalla.

### Task 1: Watch the “Simple Heart Transfer”

**Description:** We have created a video to show how your connections
and program should work in this activity.
See the video at [Simple Heart Transfer](https://microbit.nominetresearch.uk/networking-book/simple_heart_transfer.html).

**Instruction:** Watch the Simple Heart Transfer in the video.

**Important: Do not skip this
task. It will help you to test whether the files you downloaded for Task 2
work. It will also help you to write your program for this chapter.**


### Task 3: Test “Simple Heart Transfer” Hex files

**Description:** We provided two files, named [microbit1\_wired\_simpleheart\_secret.hex](microbit1_wired_simpleheart_secret.hex) and
[microbit2\_wired\_simpleheart\_secret.hex](microbit2_wired_simpleheart_secret.hex) in this folder,
for you to test how the final program should work. These files will run
on your micro:bits, but you will not be able to display the code using
the JavaScript Blocks editor.

**Instruction:** Download the *Simple Heart Transfer* code into your
micro:bits. There are two different hex files for micro:bit 1 and
micro:bit 2. Test the program by tilting your micro:bits and checking
when the heart icon is displayed.

### Task 4: Program a heart transfer

**Description:** In this task, you will program your micro:bits to get a
similar behaviour to what you observed in the Tasks 2 and 3. To do this
task, you will need to think about the following questions:

1. Which input will the micro:bits react to in your program?

2. How do the microbits send data to each other?

3. **Hint: Do you think they are sending each other an actual Heart
    icon?**

**Instruction:** For question 1, look at the options under the JavaScript Blocks editor  *Input*
menu. For question 2, use the example Telegraph program above. For question 3, here is another big hint.
**Hint: Assume micro:bit 2 knows that it will be receiving a Heart icon
from micro:bit 1.**

Program your micro:bit 1 so that:

1. It displays a heart icon until it is tilted over micro:bit 2.

2. When tilted over micro:bit 2, it sends a pulse to micro:bit 2 over
    the correct pin.

3. When micro:bit 1 receives a pulse on its correct pin, it displays a
    heart icon .

Program your micro:bit 2 so that:

1. It displays a heart icon when it receives a pulse on its
    correct pin.

2. When tilted over micro:bit 1, it sends a pulse to micro:bit 2 over
    the correct pin.

Extended activity
-----------------

!!! attention "Exercise 2"
	Watch the [Wired\_pixel\_by\_pixel\_heart.m4v](https://microbit.nominetresearch.uk/networking-book/pixel_heart_transfer.html). Based on this video, discuss with your teammate how you can send more complex data across wires. Make a proposal and discuss with others.

!!! attention "Exercise 3"
	Watch the two videos under the Resources section. How are they related to your activity? Discuss.

Problems
--------

1. What is a bit?

2. How many bits are there in a kilobyte?

3. Explain the use of Ground (GND) and 3V pins in your micro:bit.

4. How many bits did you send to the receiver in your “Simple Heart Transfer” program?

5. How are the bits in your program sent over the wire in your program?

Resources
---------

- Video: What is the Internet (Code.org) -   <https://youtu.be/Dxcc6ycZ73M>

- Video: The Internet: Wires, Cables and Wifi (Code.org) - <https://youtu.be/ZhEf7e4kopM>

- BBC Bitesize, Introducing Binary - <http://www.bbc.co.uk/education/guides/zwsbwmn/revision>

[^1]: This image is by micro:bit Educational Foundation at [www.microbit.org](https://www.microbit.org).

[^2]: Microbit telegraph activity <https://makecode.microbit.org/projects/telegraph/make>  
