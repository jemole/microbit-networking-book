Juego 2: Piedra, papel o tijera por la radio
============================================

![Chapter 7 image](chapter7.png)

Introducción
------------

¡Juguemos a Piedra, papel o tijera! Como sabes, es un juego de dos jugadores. Cada jugador, al mismo tiempo, forma con sus manos una de las opciones (piedra, papel o tijera). Se usan las siguientes reglas para decidir quién gana:

- La piedra aplasta a la tijera.

- La tijera corta el papel.

- El papel cubre la piedra.

- Si ambos jugadores escogen la misma forma, empatan.

La siguiente figura resume las reglas.

![Reglas de Piedra, papel o tijera.](Rock-paper-scissors.jpg)

!!! note ""
	**Figura 1:** Reglas de Piedra, papel o tijera.

En este capítulo vamos a progrmar este juego con nuestras placas micro:bit. Y al hacerlo practicaremos:

- *Comunicación unicast*

- Uso de variables

- Uso de condicionales

### Necesitarás

    2 micro:bits
    1 pizarra
    rotuladores/notas adhesivas
    1 colega

A programar: Piedra, papel o tijera
-----------------------------------

Para programar el juego es mejor trabajar en parejas. En la tarea 1 os vais a familiarizar con el juego y no usaréis la radio. A partir de la tarea 2 será cuando nos lancemos a usar la radio.


### Tarea 1: Empezamos con el juego base

**Descripción:** Para familiarizarnos con el juego, sigue la actividad [Piedra-papel-tijera](https://makecode.microbit.org/projects/rock-paper-scissors), que te guiará paso a paso en la construcción de una versión sencilla del juego. Fíjate en que el programa asigna un número a *piedra*, *papel* y *tijera*. Por ejemplo, piedra=1, papel=2, tijera=3.

**Instrucciones:** Programa el código mostrado en la página de la actividad y descárgalo a tu micro:bit. Juega unas partidas con tu pareja. Tendréis que agitar las placas al mismo tiempo y luego decidir quién gana en base a las reglas descritas en la introducción.


### Tarea 2: Enviamos la forma seleccionada por radio con unicast

**Descripción:** Para jugar por radio usarás el botón A para seleccionar entre piedra, papel o tijera. Usarás el botón B para confirmar la selección y enviarla por radio. Al igual que en la tarea 1, se usará: piedra=1, papel=2, tijera=3.


**Instrucciones:** Escribe un programa que haga lo siguiente:

1. Usa el botón A para seleccionar entre piedra, papel o tijera. Cada vez que pulses el botón A debería mostrar alternativamente un icono de cada una de las tres formas.

2. Usa el botón B para confirmar tu selección y enviar el número correspondiente por radior mediante comunicación unicast a la placa de tu pareja, tal como hicimos en las prácticas del capítulo [Comunicación Unicast: De una a una](../unicast/unicast.md).

3. Añade el código para recibir un número. Cuando recibas un número, muestra el icono correspondiente en la pantalla. Por ejemplos, si recibes un 2 deberías mostrar el icono del papel.

Comprobar en pareja que podéis enviar y recibir correctamente.


### Tarea 3: Rellenamos la tabla de reglas

**Descripción:** Tu programa debe decidir quién gana cuando recibes un número desde la micro:bit de tu colega.

**Instrucciones:** Para decidir quién gana, hay que comparar el número que tú escogiste con el número que has recibido por radio. La tabla de abajo puede ayudarte a decidir quién gana cada partida [^2]. Usando esta tabla puedes comparar *Mi mano* con *Mano oponente*. Por ejemplo, si los dos números significan *papel*, es un empate y el resultado es una cara de sorpresa. Pero si *Mi mano* es *papel* y *Mano oponente* es *tijera*, el resultado es una cara triste. Y si fuera al contrario el resultado sería una cara alegre. En base a las reglas del juego, termina de rellenar la tabla.


![Tabla Pedra, papel o tijera](IncompleteRockPaperScissorsTable.png)

!!! note ""
	**Figura 2:** Tabla Pedra, papel o tijera
	
### Task 4: Play the game

**Description:** Once you filled the table, you need to decide how to
program these rules in your code. Your program will:

1. play the game based on Rock-Paper-Scissors rules

2. display a *happy* face if you won, a *sad* face if you lost. And if it’s a draw, show a *surprised* face.

**Instruction:** Figure below shows a
template for programming the table using the *if* block in the JavaScript Blocks editor
*Logic* menu. Note that this is just a template and it is there to give
you an idea of the structure of your program. For instance, your *on radio received* block will have to be different to do unicast communication (see [Unicast Communication: One to One](../unicast/unicast.md)).

You will notice in the template that we used two variables: *selected* and *received*.
*selected* is set to *True* when you make the selection for your hand by pressing button B. *received* is set to *True* when you receive your opponent’s hand. In the *forever* block,
the game is only played when both *selected* and *received* are *True*. Once you enter the block to play the game, these variables are initialized to *False* for the next round.

After you program the game, play it with your teammate! Who
wins more often?

```blocks
let my_hand = 0
let selected = false
input.onButtonPressed(Button.B, function () {
    selected = true
    radio.sendNumber(my_hand)
})
```
```blocks
let opponent_hand = 0
let received = false
radio.onReceivedNumber(function (receivedNumber) {
    received = true
    opponent_hand = receivedNumber
})
```
```blocks
let my_hand = 0
let opponent_hand = 0
let received = false
let selected = false
basic.forever(function () {
    if (selected == true && received == true) {
        selected = false
        received = false
        if (opponent_hand == my_hand) {
            basic.showIcon(IconNames.Surprised)
        } else {
            if (my_hand == 0 && opponent_hand == 1) {
                basic.showIcon(IconNames.Happy)
            } else if (0 == 0) {
            	
            } else if (0 == 0) {
            	
            } else {
            	
            }
        }
    }
})
```

!!! note ""
	**Figure 3:** Rock paper scissors: A template for programming the rules
	
Exercises
---------

!!! attention "Exercise 1"
	How might you expand your program to play rock/paper/scissors/lizard/spock? 
	To learn more about this extension check the website: [http://www.samkass.com/theories/RPSSL.html](http://www.samkass.com/theories/RPSSL.html).

Problems
--------

1. How do you test a tie in your program?

2. How does the Table change, if paper=2, rock=0, and scissors=1? Redraw your table.

3. To play with a different player, what do you need to change in your program? Remember you are using unicast to send your hand shape.

4. What happens if you send your hand shape to the other player before they pick theirs? Will there be a problem? Could they cheat!?

Recursos
--------

- Wikipedia: piedra, papel o tijera - 
    <https://es.wikipedia.org/wiki/Piedra,_papel_o_tijera>
    
- Vídeo: cómo ganar siempre jugando a Piedra, papel o tijera - 
    <https://www.youtube.com/watch?v=i0_Y0ll6Z08>

