Juego 3: Hudir la flota por radio
=================================

![Chapter 10 image](chapter10.png)

Introducción
------------

En esta actividad vamos a programar una versión para micro:bt del famoso juego Hundir la flota, al que ya se jugaba desde la Primera Guerra Mundial, aunque con papel y lápiz [^1]. En 1967 se publicó una versión con tablero de plástico, y hoy en día existen multitud de versiones electrónicas y apps [^2].

![Tablero del Hundir la flota](Battleship_game_board.png)

!!! note ""
	**Figura 1:** Tablero del Hundir la flota

Para repasar cómo funcioa el juego vamos a usar el tablero de ejemplo de la figura de arriba. En el ejemplo, cada jugador usa un tablero de 10x10 casillas, y la flota de cada jugador incluye 10 barcos de diferentes tamaños (los rectángulos grises). La figura muestra cómo están colocados los de un jugador: con 4 barcos de tamaño 2, 3 barcos de tamaño 3, 2 barcos de tamaño 4, y 1 barco de tamaño 6. Por supuesto, el sitio donde se han colocado los barcos es secreto y no lo conoce el oponente. Cuando ambos jugadores han colocado sus barcos comienzan a tratar de adivinar dónde están los barcos del oponente, para lo que disparan misiles que caen en la casilla escogida. En el ejemplo, las cruces muestran los disparos que ha realizado el oponente. Fíjate en que algunas de estas cruces han caído en el agua, mientras que otras han alcanzado a barcos. El oponente ha hundido el barco de las casillas 8A-8B. El barco de las casillas 6J-7J-8J ha sido alcanzado dos veces; otro disparo lo hundiría. Los jugadores van escribiendo en otro tablero los disparos que ya han realizado, donde apuntan cada acierto y cada fallo para decidir a qué casilla disparar a continuación.

Para programar Hundir la flota con las micro:bits vas a tener que poner en práctica todos tus conocimientos de redes. El juego requiere comunicación unicast bidirecciónal, algo que hemos trabajado en los temas [Comunicación unicast: De una a una](../unicast/unicast.md) y [Unicast de ida y vuelta:ping-pong](../twowayunicast/twowayunicast.md). Además, si te animas con las extensiones propuestas en los ejercicios, tendrás que hacer uso de lo aprendido en los capítulos [Gestionar errores: Retransmisiones](../retransmissions/retransmissions.md) y [Gestionar errores: Acuse de recibo](../acknowledgements/acknowledgements.md). 

En resumen, vas a practicar con:

- El concpeto de *comunicación unicast*, *unicast de ida y vuelta* y *retransmisiones*

- Envío y recepción de mensajes

- Botones de entrada

- La pantalla y sus coordenadas

- Variables y números aleatorios

- Arrays

- Bucles

### Vas a necesitar

    2 micro:bits
    1 colega

Diseñar un Hundir la flota para micro:bit {#sec:design}
-----------------------------------------

### Cómo funciona el juego

Vamos a repasar las diferentes partes que necesitamos para programar el Hundir la flota.

**Usar la pantalla de micro:bit como tablero:** Como las micro:bits tienen una pantalla de 5x5, el tablero tendrá que ser más pequeño que el del ejemplo de la introducción. Y esto no nos va a dejar espacio para muchos barcos. Así que la flota va a tener 5 barcos, todos de tamaño 1.

Cuando dispares un misil, hay que saber si ha alcanzado a un barco o ha caído al agua. Así que hay que resevar la fila de arriba para mostrar si se trata de un acierto o de un fallo. Si la micro:bit del oponente nos dice que es un acierto, tu placa encenderá el LED de la izquierda de la fila superor. Por el contrario si es "agua", se encenderá el LED de la derecha.

Otra limitación de nuestro juego será que no podremos mostrar en pantalla un registro de las posiciones de nuestros aciertos y fallos. Quizás lo más fácil sea ir apuntándolo en papel y lápiz como se hacía en el siglo XX ;-) 

**Disparar misiles:** Para disparar misiles vamos a usar los botones, seleccionando un número de fila y de columna. Ten en cuenta que cuando las coordenadas LED se muestran como *(x,y)*, x es el número de columna, mientras que y es el número de fila. Para más información puedes echar un ojo a [https://microbit.org/guide/hardware/leds/](https://microbit.org/guide/hardware/leds/).

![Hundir la flota en micro:bit.](Battleship_microbit_ES.png)

!!! note ""
	**Figura 2:** Hundir la flota en micro:bit

El botón A se usará para seleccionar el número de columna y el botón B para seleccionar el número de fila. Por tanto, para disparar a la posición (2,3) tendrás que presionar el botón A dos veces y el botón B 3 veces, y luego presionar los botones A y B a la vez. Para ver si lo has entendido, debatid en parejas qué secuencia de botones habría que presionar para disparar a la posición (0,4).

Cuando presiones los botones tu micro:bit enviará un mensaje a la placa del oponente. Así, por ejemplo, si quieres disparar a la posición (4,4), tu programa enviará las coordenadas (4,4). Cuando la micro:bit del oponente recibe un disparo, comprueba si ha "tocado" un barco o si ha caído al "agua", y enviará consecuentemente un mensaje por radio indicando "tocado" o "agua".

En tu micro:bit, cuando recibas "tocado" encenderás el LED de la esquina superior izquierda de la pantalla. Cuando recibas "agua", encenderás el de la esquina superior derecha.


### Una partida de ejemplo

Veamos cómo se verá una partida en las micro:bits. Al principio tus barcos se colocarán aleatoriamente en las cuatro filas inferiores de la pantalla, como en la figura de abajo. La figura muestra los 5 barcos de cada jugador colocados en la zona de batalla.

![Una partida de Hundir la flota: Escenario inicial con los barcos colocados aleatoriamente.](Initial.jpg)

!!! note ""
	**Figura 3:** Una partida de Hundir la flota: Escenario inicial con los barcos colocados aleatoriamente

El atacante (a la izquierda) presiona el botón A 3 veces, y el botón B 1 vez. Al presionar luego los dos botones a la vez dispara y envía un mensaje a través de la radio con la coordenada (3,1). Como hay un barco en esa posición, se trata de un disparo "tocado". En la figura de abajo el LED de la posición más a la izquierda de la fila superior del atacante se enciende. Y, en la placa del oponente, el LED de la posición (3,1) se apaga, puesto que el barco ha sido hundido.

![Hundir la flota: ¡Tocado! ¡Has alcanzado un barco!](Hit_ES.jpg)

!!! note ""
	**Figura 4:** Hundir la flota: ¡Tocado! ¡Has alcanzado un barco!

Echemos un vistazo también a una situación en la que se falla con el disparo (figura de abajo). En este caso, como el disparo es "agua", en la placa del oponente no hay que cambiar nada. Pero en la del atacante, en la fila de arriba, hay que encender el LED de la derecha del todo para mostrar que se ha fallado. 

![Hundir la flota: ¡Agua! No ha habido suerte, amigo](Miss_ES.jpg)

!!! note ""
	**Figura 5:** Hundir la flota: ¡Agua! No ha habido suerte, amigo

Programming: Battleship
-----------------------

Battleship is a two-person game. Both players can run identical problems, or you can each program your own version, as long as you agree on the details of the radio messages. When writing a more complex program like this, you will find it easier if you split up into parts, and test each part as you write it. (This is a valuable skill as you learn more about programming!)

To help with this, we have split the program into four tasks: once you have completed the final task, you will be able to play with your teammate. If you find any errors
(bugs) in your program, work with your teammate to fix them until you
get the game play as described in the introduction.

### Task 1: Setting up the game

**Description:** This part needs to take place before the game starts.
You will place 5 ships on your board. Think about randomly placing 5
points in the battle area, which is a 4 x 5 matrix. Answer the following
questions:

- How will you represent the battle area in your program as a data
    structure?

- How will you select random coordinates (*column\_number*,
    *row\_number*) for 5 ships, where *column\_number* is between 0 and 5, and *row\_number* is between 1 and 5?

- How will you represent the information that there is a ship at each of these coordinates?

You will also set up your radio and packet configuration to send unicast messages.

**Instruction:** Create the necessary data structures and variables that represent the ships in the battle area. Set up your radio and packets
for unicast communication. Test whether your program displays 5 ships randomly
placed on the lower 4 rows of the display, like in the example figures.

### Task 2: Firing a shot

**Description:** When button A is pressed, it indicates the
*column\_number* for a shot. So, you need to count how many times this
button was pressed to get the *column\_number*. When button B is
pressed, it defines the *row\_number* for the same shot. Again,
count the number of times to get the *row\_number*.

**Important:** If you do not press either button A or button B, the
*column\_number=0* and *row\_number=0*. A shot with *row\_number=0* is a
wasted shot because there cannot be any ships on that row.
Also, make sure if either button is pressed more than four times, it shoud start counting again from 0. In other words, the button counters should
increment  with each button press like this: 0, 1, 2, 3, 4, 0, 1, 2,
3, 4.

Pressing both buttons together will send *column\_number* and
*row\_number* over the radio to your opponent. Decide how to send this
message in a packet, and agree on this with your teammate if you are writing separate programs.

**Instruction:** Program the button presses for A, B, and A+B. The
program piece for buttons A+B will send a radio message.

Test the correctness of your code. Add a little test code so that when you fire, as well as sending a radio message,  it also lights up the LED at
*column\_number* and *row\_number*. Use this to check that aiming is working correctly. This is just test code, so remove it once you're confident that it works.

### Task 3: Receiving a shot

**Description:** When you receive a shot, you will check whether you
have a ship on the (*column\_number*, *row\_number*) of the shot.
If you have a ship there, then it was hit and sunk. You will send a
“Hit” message to your opponent, and remove the ship from the display. If it is a miss, send a
“Miss” message too your opponent.

**Instruction:** Depending on how the packet was formatted, decode
(*column\_number*, *row\_number*) from the received packet. If you have
a ship on (*column\_number*, *row\_number*), it is a hit: Turn off the
LED in that position. If you have a separate data structure as a variable to represent your ships, update that too. Send your opponent a “Hit” message. If it is a miss, send a “Miss” message to your opponent.

### Task 4: Receiving the shot result: “Hit” or “Miss”

**Description:** Turn on LEDs in top row depending on the result.
If it is a “Hit”, check if you reached 5 hits. Then you won! Display a
smile!

**Instruction:** If you receive a “Hit”, light the leftmost LED of the top row (the LED in (0,0) position). Update the count of your hits,
and if you reached 5, display a smile! If the result was a “Miss”, light the rightmost LED of the top row (the LED in (4,0) position).

Test your program(s) with your opponent. To start with, it'll be easier if you can see each other's screens. You might find it helpful to put in some test code, like you did for the previous task. For example, you could print out "hit" or "miss" when you receive and decode a shot. You might even find it helpful to print out the coordinates of the show when you receive the packet.

Extended Activity
-----------------

Battleship game has many variations. See the Wikipedia site in Resources
to read about the variations.

!!! attention "Exercise 1"
	One variation allows players to keep it secret that a ship has been sunk. So, their opponent has to take further shots to confirm that an area is clear. This is like having a packet loss! Remember how you dealt with packet losses in [Handling errors: Retransmissions](../retransmissions/retransmissions.md) and [Handling errors: Acknowledgements](../acknowledgements/acknowledgements.md). How would you apply those concepts to this case? Discuss possible solutions with your friend. Then, program and test your new solution.

!!! attention "Exercise 2"
	Imagine a variant when it takes 3 hits to sink a ship instead of 1 hit. How would your program change? Do you need to make changes on the sender side or the receiver side? How similar is this to using default retransmissions in [Handling errors: Retransmissions](../retransmissions/retransmissions.md)?

Problems
--------

![Battleship game: A random battle area](Example_init.png)

!!! note ""
	**Figure 6:** Battleship game: A random battle area

**Problem 1:** The figure above shows randomly placed ships in a battle area. Which coordinates do you need to send to hit all the ships?

![Battleship game: Two players](Two_microbits_sidebyside.png)

!!! note ""
	**Figure 7:** Battleship game: Two players

**Problem 2:** The figure above shows randomly placed ships in the battle areas of two micro:bits. Table below lists all the shots that are fired from the micro:bit 1 (left/red micro:bit) and micro:bit 2
(right/yellow micro:bit). Who wins?

| **Rounds** | **Micro:bit 1** | **Micro:bit2** | **Result** |
|------------|:----------------|:---------------|:-----------|
| 1 | (3,1) | (2,1) | |
| 2 | (0,3) | (0,1) | |
| 3 | (1,1) | (3,2) | |
| 4 | (4,1) | (3,3) | |
| 5 | (0,3) | (4,3) | |
| 6 | (2,2) | (0,3) | |
| 7 | (3,2) | (1,4) | |

If you wanted to play this game with another opponent, what do you need
to change in your program?

[^1]: Battleship in Wikipedia: [https://en.wikipedia.org/wiki/Battleship_(game)](https://en.wikipedia.org/wiki/Battleship_(game))

[^2]: Online Battleship game 1: [https://battleship-game.org](https://battleship-game.org) and Online Battleship game 2: [http://www.mathplayground.com/battleship.html](http://www.mathplayground.com/battleship.html)
