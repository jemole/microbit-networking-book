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

RTT = Tiempo\_recibo\_pong - Tiempo\_envío\_ping  

La siguiente figura muestra la relación entre *ping*, *pong*, y round-trip-time.

![Round-trip-time. Micro:bit 1 sends a *Ping* message to Micro:bit 2 at *Time\_send*. The Micro:bit 2 responds with a *Pong* message. Micro:bit 1 receives the *Pong* message at *Time\_receive*. The difference between these two times, *Time\_receive* and *Time\_send* is the round-trip-time.](Ping-rtt.png)

!!! note ""
	**Figure 1:** Round-trip-time. Micro:bit 1 sends a *Ping* message to 
	Micro:bit 2 at *Time\_send*. The Micro:bit 2 responds with a *Pong* message. 
	Micro:bit 1 receives the *Pong* message at *Time\_receive*. The difference 
	between these two times, *Time\_receive* and *Time\_send* is the round-trip-time.

Besides round-trip-time (RTT), the Ping program reports statistical
information. Figure below shows an example output as a result of
using the command:

    ping www.google.com

on the <http://ping.eu/ping> website. In this example, four Ping messages were sent to *www.google.com*.
The round-trip-time for each message is given with the *time* value in
each line. For example, for the first ping, the RTT is 10.2 ms
(milliseconds). The program also reports ping statistics. For example, 4
packets were sent, 4 packets were received. This means 0% packet loss.
The average RTT (shown as *avg*) is 10.184 ms.

![The output of running ping to send four messages to *www.google.com*. The <http://ping.eu/ping> online program reports round-trip time and a statistical summary of the results.](PingGoogle.png)

!!! note ""
	**Figure 2:** The output of running ping to send four messages to *www.google.com*. 
	The <http://ping.eu/ping> online program reports round-trip time and a 
	statistical summary of the results.

With a micro:bit, to calculate the round-trip-time of your messages, you
will use the *running time* variable.

!!! hint "Definition 3: _micro:bit running time_"
	A variable that keeps record of how long has passed since the micro:bit was
	turned on or reset (measured in milliseconds).

![PXT running time](PXTRunningTime.png)

!!! note ""
	**Figure 3:** MakeCode running time

In the rest of this chapter, you will use the running time variable to
calculate the round-trip time. It will be very useful to record the time
when you first sent a message, and also when you received a response.
**Hint: Recording running time means setting a variable equal to the
current running time. You will need to combine the set item block in the
JavaScript Blocks editor *Variables* menu with the running time block in the *Input*
menu shown above.**

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
