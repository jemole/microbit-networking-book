Unicast de ida y vuelta: ping-pong
==================================

![Chapter 6 image](chapter6.png)

Introducción
------------

En este capítulo vas a aprender sobre *comunicación bidireccional*: enviar un mensaje a una micro:bit y recibir una respuesta a tu mensaje. También aprenderemos sobre el programa Ping, que es una herramienta muy utilizada para comprobar si dos ordenadores tienen conectividad.

Este capítulo se basa en los aprendizajes de [Comunicación unicast: de una a una](../unicast/unicast.md). Las nuevas ideas son:

- La comunicación de ida y vuelta (*comunicación bidireccional*)

- El programa Ping

- El concepto de tiempo de viaje (o tiempo de ida y vuelta)

### Qué necesitas

    2 micro:bits
    1 pizarra
    rotuladores/notas adhesivas
    1 colega

Antecedentes
------------

La *comunicación bidireccional* permite comunicación de ida y vuelta entre dos ordenadores.

!!! hint "Definición 1: _Comunicación bidireccional_"
	Es un modo de comunicación en el que la información se transmite en ambas direcciones pero no al mismo tiempo.

Con la comunicación bidireccional, por tanto, las micro:bits podrán tanto enviar como recibir mensajes. Y de este modo es posible crear protocolos en los que, cuando un equipo envía un mensaje, espera a recibir una respuesta determinada a su mensaje.

!!! hint "Definición 2: _Ping_"
	Ping es un ejemplo de un protocolo bidireccional. Se usa habitualmente en Internet para comprobar si un dispositivo de una red está encendido y conectado correctamente. 

El programa Ping envía un mensaje *ping* para comprobar si otro ordenador está bien. Y espera que este mensaje sea respondido con un mensaje *pong*. Es como jugar al ping-pong pero con ordenadores y a través de redes. Si el emisor no recibe una respuesta a su *ping* podemos suponer que hay algún tipo de problema, bien en la red, bien en el receptor. También es problemático si la respuesta *pong* llega al emisor pero tarda mucho en hacerlo.

Así que el programa Ping mide el *tiempo de viaje* (o tiempo de ida y vuelta, o round-trip-time) entre dos ordenadores para detectar este tipo de problemas.

!!! hint "Definición 3: _Round-trip-time (RTT)_"
	Round-trip-time es el tiempo que tarda un mensaje en ir desde el emisor hasta el receptor y de vuelta al emisor.
	
En otras palabras, el emisor mide la diferencia de tiempo entre el momento en que envió el *ping* y en que recibió el *pong*.

RTT = Tiempo\_recepción\_pong - Tiempo\_envío\_ping  

La siguiente figura muestra la relación entre *ping*, *pong*, y round-trip-time.

![Round-trip-time. Micro:bit 1 envía un mensaje *ping* a Micro:bit 2 en el momento *Tiempo\_envío*. Micro:bit 2 responde con un mensaje *pong*. Micro:bit 1 recibe el mensaje *pong* en el momento *Tiempo\_recepción*. La diferencia entre estos dos tiempos, *Tiempo\_envío* y *Tiempo\_recepción*, es el round-trip-time.](Ping-rtt.png)

!!! note ""
	**Figura 1:** Round-trip-time. Micro:bit 1 envía un mensaje *ping* a Micro:bit 2 en el momento *Tiempo\_envío*. Micro:bit 2 responde con un mensaje *pong*. Micro:bit 1 recibe el mensaje *pong* en el momento *Tiempo\_recepción*. La diferencia entre estos dos tiempos, *Tiempo\_envío* y *Tiempo\_recepción*, es el round-trip-time.

Además del round-trip-time (RTT), el programa Ping aporta otra información estadística. La figura siguiente muestra un ejemplo de salida como resultado de usar la orden:

    ping www.google.com

en la web <http://ping.eu/ping>. En este ejemplo se enviaron cuatro mensajes a *www.google.com*. El RTT para cada mensaje se muestra con el valor *time* en cada línea. Por ejemplo, para el primer ping el RTT es 10.2 ms (milisegundos). El programa también informa de estadísticas del ping. Por ejemplo, se muestra que se han enviado 4 mensajes y se han recibido 4 mensajes. Este significa que se han perdido el 0% de los mensajes. La media del RTT (que aparece como *avg*) es 10.184 ms.

![The output of running ping to send four messages to *www.google.com*. The <http://ping.eu/ping> online program reports round-trip time and a statistical summary of the results.](PingGoogle.png)

!!! note ""
	**Figura 2:** La salida de ejecutar ping para enviar cuantro mensajes a *www.google.com*. El programa online <http://ping.eu/ping> muestra el round-trip time e información estadística.
	
Con tu micro:bit, de cara a calcular el round-trip-time tendrás que usar el bloque *tiempo de ejecución (ms)*.

!!! hint "Definición 3: _tiempo de ejecución micro:bit_"
	Una variable que mantiene el tiempo que ha pasado desde que la micro:bit se encendió o se reseteó (medido en milisegundos).

![PXT running time](PXTRunningTime.png)

!!! note ""
	**Figura 3:** Tiempo de ejecución en MakeCode

En el resto de este capítulo usarás el tiempo de ejecución para calcular el RTT. Será muy útil para guardar el tiempo en el que enviaste un mensaje y también en el que recibiste un mensaje. **Ojo: guardar el tiempo significa establecer el valor de una variable para que sea igual al tiempo de ejecución actual. 


Programming: Ping
-----------------

This activity is best done with a team of two. You will together program
your micro:bits to run the Ping program. For this, you will need to
complete four tasks.

### Task 1: Prepare for unicast

**Description:** Ping uses unicast between the sender and the receiver
micro:bits. Look at your notes for [Unicast Communication: One to One](../unicast/unicast.md)  and your
unicast program to remember how to do unicast.

**Instruction:** Start with using the unicast program you have written for
[Unicast Communication: One to One](../unicast/unicast.md) as a basis. In this program, decide which
micro:bit is going send the *Pings*, and which micro:bit is going to
respond with *Pongs*. Set the address variables based on your decision.
Design your message header, *Ping* packet, and *Pong* packet.

### Task 2: Send a Ping

**Description:** The ping sender records the time before it sends out a
*Ping* packet. It unicasts the *Ping* packet.

**Instruction:** Use *running time* to record the *Ping* sending time.
Send a *Ping* packet to the receiver micro:bit.

### Task 3: Receive a Ping

**Description:** The receiver micro:bit responds a *Ping* message with a
*Pong*.

**Instruction:** Program the receiver micro:bit to unicast a *Pong*
packet when a *Ping* packet is received.

### Task 4: Receive a Pong and calculate round-trip-time

**Description:** When the sender micro:bit receives the *Pong*, it
calculates the round-trip-time. 

**Instruction:** Program the sender to
receive a *Pong* packet. When the *Pong* is received, record the time
using the running time variable. Show the difference between receiving
and sending times on your display. Run your program 5 times, and write
down the send times that you see in your display. Answer these two
questions:

1. What is the minimum and maximum round-trip-time (RTT)?

2. What is the average RTT?

Exercises
---------

!!! attention "Exercise 1"
	Extend your Ping program to send automatically more than one *Ping* message. 
	Test it with 10 *Pings*. Calculate the average round-trip time of these Ping messages.

!!! attention "Exercise 2"
	The Ping program reports the round-trip-time. What if you wanted to calculate 
	the time the message took one-way? Is it possible to calculate one-way times? 
	In other words, is it possible to calculate how long it takes to send a message 
	from the sender to the receiver? How long the messages take from the receiver to the sender?

Problems
--------

1. In the example ping figure from the <http://ping.eu/ping> site, what is 172.217.23.228?

2. What is round-trip-time, and how is it calculated?

3. Think about the following scenario: micro:bit 1 sends a *Ping* to micro:bit 2 at time *5*. If the round-trip-time is *10*, at what time did the micro:bit 1 receive the *Pong* message?

4. In the example ping figure from the <http://ping.eu/ping> site, what are the minimum and maximum round-trip-times (RTTs)?

5. In the example ping figure from the <http://ping.eu/ping> site, the packet loss 0% loss. What is the loss percentage, if 2 *Ping* messages were lost out of 5?

Resources
---------

Video: What is a Ping? - <https://youtu.be/N8uT7LNVJv4>
