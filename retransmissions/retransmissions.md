Gestionar errores: retransmisiones
==================================

![Chapter 8 image](chapter8.png)

Introducción
------------

En los capítulos anteriores es probable que hayas notado que la comunicación inalámbrica no es siempre fiable. En otras palabras, puede que no todos los mensajes que se envían sean recibidos por el otro extremo. En este capítulo aprenderemos a incrementar la probabilidad de que nuestros mensajes sean recibidos. ¿Qué podríamos hacer si un mensaje se pierde? En esta práctica veremos un método simple pero efectivo: las retransmisiones.

En resumen, aprenderás sobre:

- Errores en comunicaciones inalámbricas

- *Retransmisiones* como un método de fiabilidad.

### Qué necesitas

    2 micro:bits
    1 colega

Antecedentes
------------

En las comunicaciones inalámbricas un error se puede producir por varios motivos. Por ejemplo, si hay obstáculos físicos como muros, puertas o incluso personas. Las señales inalámbricas pierden fuerza al atravesar estos obstáculos y a veces incluso rebotan en ellos.

Cuantos más obstáculos haya entre emisor y receptor mayor es la probabilidad de que ocurra un error. Además si emisor y receptor están muy alejados puede que no sean capaces de comunicarse. Imagina que hay un montón de obstáculos entre dos personas que se estén hablando; puede que no siempre puedan escuchar lo que el otro está diciendo.

Otra causa de errores inalámbricos pueden ser las *interferencias de radio*. Esto se debe a que la comunicación inalámbrica es broadcast (acuérdate de lo que vimos en el capítulo de [Comunicación broadcast](../broadcast/broadcast.md)). Esto significa que pueda haber mucha gente enviando mensajes, y sus transmisiones puede colisionar en los receptores. Es decir, que los emisores están *interfiriendo* unos con otros.

!!! hint "Definición 1: _Interferencia_"
	En comunicación inalámbrica una interferencia es cualquier otra señal que interrumpe una señal mientras viaja hacia su destino.
	
Imagina en una clase en la que todo el mundo está hablando a la vez. Seguro que no te enterás de la mitad de las cosas que esté diciendo tu compañero. Las señales de otras personas están interfiriendo con la señal de tu compañero en su camino hacia ti. En redes, esto se llama pérdida de paquetes.

!!! hint "Definición 2: _Pérdida de paquetes_"
	La pérdida de paquetes ocurre cuando uno o más paquetes que viajan en una red de ordenadores no llegan a su destino. La pérdida de paquetes se mide como la proporción de paquetes perdidos y paquetes enviados (echa un ojo a la fórmula de abajo).

*Pérdida de paquetes* = (*Paquetes perdidos*)/(*Paquetes enviados*)

Por otra parte es posible que si hay mucha interferencia se puedan recibir mensajes con errores. Por ejemplo podría ocurrir que escucharas "guapo" cuando tu compañero en realidad ha dicho "guarro". En redes esto se llama paquetes con errores. Los paquetes con errores se miden como la tasa paquetes con errores.

!!! hint "Definición 3: _Tasa de paquetes con errores_"
	La tasa de paquetes con errores es la proporción de paquetes que se han recibido con uno o más errores y los paquetes enviados.
	
*Tasa de paquetes con errores* = (*Paquetes con errores*)(*Paquetes enviados*)

In this chapter, we will cover one simple method to handle these errors, *retransmissions*, where the sender automatically retransmits messages multiple times to increase the
chance of reception.

!!! hint "Definition 4: _Retransmissions_"
	Retransmissions mean sending messages many times.

In the Figure below, let’s assume the sender knows that
the communications medium loses half of its packets. In other words, the
packet loss is 0.5 (or 50%). The sender micro:bit decides to send each packet twice to
increase the chance to get its messages through. The first packet is the
transmission, and the second packet is the retransmission. So, the
number of retransmissions is 1.

![Retransmissions may increase message success. In the example, the sender sends each message twice by default. So, even if the first “Hello” failed, the second “Hello” was received by the receiver!](Retransmissions.png)

!!! note ""
	**Figure 1:** Retransmissions may increase message success. 
	In the example, the sender sends each message twice by default. So, even if 
	the first “Hello” failed, the second “Hello” was received by the receiver!

It is common to use retransmissions combined with another method. For
instance, senders may choose retransmit only when they are sure there
has been an error. We will explore this option in the next chapter,
[Handling errors: Acknowledgements](../acknowledgements/acknowledgements.md).

Programming: Retransmissions
----------------------------

This activity is best done with a teammate. You will start with creating
packet errors in Task 1, and then test different packet error rates in
Task 2. In Task 3, you will program the retransmissions solution to
handle these errors. In this task, you will also run a series of
experiments to measure how well retransmissions works.

### Task1: Create packet errors

**Description:** In wireless communication, packets may fail randomly.
This may make the testing your code for this chapter difficult. To test
errors, you will use a custom block in the JavaScript Blocks editor to send messages with errors.

The ErrorRadio functions are like the Radio functions, but have an
extra *error* parameter. This parameter is set to 20 by default, which
means the packet error rate is 0.2 or 20%.

![Error radio custom blocks](ErrorRadio.png)

!!! note ""
	**Figure 2:** Error radio custom blocks

**Instruction** To use the custom blocks in the JavaScript Blocks editor, import the
ErrorRadio.hex file in this folder. With your teammate,
decide who will have the sender micro:bit, and who will have the
receiver micro:bit. Follow the approach in [Unicast Communication: One to One](../unicast/unicast.md)
to put sender and receiver address in your packets.
You may copy and
change one of the programs you have written for
[Unicast Communication: One to One](../unicast/unicast.md)
 to use the *ErrorRadio* blocks.

Write a small sender program that sends a number with an error. Download it
to the sender micro:bit. Write a small receiver program that receives a
number and displays it on screen. Download this program to the receiver
micro:bit.

Change the packet error rate using these error values in your program:
0, 50 and 100. Test packet errors by observing the receiver display.

### Task 2: Send a sequence of messages

**Description:** In this section, you will send a sequence of messages
to the receiver micro:bit.

**Instruction:** Extend your program in Task 1, to send this sequence:

    Start 1 2 3 4 5 6 7 8 9 10 End

You can send the *Start* and *End* using the normal Radio blocks to
send them without an error. But remember that your micro:bit’s radio may
drop messages. So, there may be errors even in sending *Start* and
*End*. No radio is perfect!

Extend the receiver program to count the number of messages it receives
in this sequence. Run experiments setting the *error* parameter to 25,
50, and 75. Calculate the packet loss using the Packet loss equation. Repeat each experiment three times. Fill
the table below with the result of your experiments. For
example, when *error* is set to 25 in experiment number 1, if you
received:

    Start 1 5 6 7 8 9 10 End

This means, you received 7 packets, and lost 3. Your packet loss is 0.3%. The first row of the table is filled based on this example. Add in the values from your own experiment Based on your experiment results, discuss with your teammate how the experiment results change as you change the value  of *error*. 

| **Error value** | **Experiment no.** | **Packets received**| **Packet loss** |
|-----------------|:-------------------|:---------------|:-----------------|
| 25 | (Example) | 7| 0.3
| 25 | 1 | | |
| 25 | 2 | | |
| 25 | 3 | | |
| 50 | 1 | | |
| 50 | 2 | | |
| 50 | 3 | | |
| 75 | 1 | | |
| 75 | 2 | | |
| 75 | 3 | | |

Task 3: Retransmit by default
-----------------------------

**Description:** In this task, you will program the automatic
retransmissions at the sender side.

**Instructions:** Change your sender code from Task 2 to send each
number in your sequence more than once. To try out your code, set
*error* to 75. For example, by setting number of retransmissions to 1,
you will send the following sequence:

    Start 1 1 2 2 3 3 4 4 5 5 6 6 7 7 8 8 9 9 10 10End

This means the sender sent 20 packets in total, including 10
retransmissions.

Change your receiver code to count the unique numbers received.  Count 
also the duplicates. Calculate the packet loss. For example,
let’s assume your receiver received, for the case of 1 retransmission:

    Start 1 1 2 3 5 5 6 8 9 9 10 End

This means, the receiver received 8 unique numbers (1, 2, 3, 5, 6, 8, 9 and 10) and 3 duplicates (1, 5 and 9). Note that the packet loss is 9 packets out of 20 (45%). But with retransmissions, the receiver only lost 2
numbers out of 9 (it did not receive 4 and 7). Let’s call this improved
packet loss *information loss*. So, the information loss with
retransmissions is 0.2. The first row of the table below is filled based on this example.

Run each experiment three times each, for different retransmission values and fill in the rest of the table.

| **Retransmissions** | **Experiment** | **Unique Packets Received**| **Duplicates** |**Packet loss** | **Information loss**|
|---------------------|:---------------|:----------------|:--------------------|-----------------|:----------------|
| 1 | (example) | 8 | 3 | 0.45 | 0.2|
| 1 | 1 |  | | | |
| 1 | 2 |  | | | |
| 1 | 3 |  | | | |
| 3 | 1 |  | | | |
| 3 | 2 |  | | | |
| 3 | 3 |  | | | |
| 5 | 1 |  | | | |
| 5 | 2 |  | | | |
| 5 | 3 |  | | | |

Extended activity
-----------------

!!! attention "Exercise 1"
	Based on your experiments, discuss with your teammate how the increase in 
	retransmissions helps. In your discussion, answer the following questions:
	
	- How does the infromation loss improve as you increase the number of retransmissions?
	- Does the method guarantee all messages are received at least once?
	- How would you improve your method?

!!! attention "Exercise 2"
	Imagine you are going to survey packet loss in different locations inside a room using two micro:bits. Write a receiver and a sender program to measure packet loss. What do you observe? How does the packet loss change in different locations?

Problems
--------

1. What is interference? Why does it happen?

2. If the sender sent 20 messages, and 11 messages were lost on the way to the destination, what is the packet loss?

3. If the packet error rate is 20% and the sender sent 40 packets, how many packets had errors?

4. Assume you do not know how many numbers that will be in the message sequence. But, you know the numbers will start from 1, and will increment by 1. For example, the sent message sequence may be: *Start 1 2 3 4 5 6 7 8 9 10 11 12 End*. What happens if you lose *Start* or *End* messages? Which one is worse: the loss of *Start* or *End* message? If the only message you receive is a 4, what can you say about the number of messages you lost?

5. Assume you do not know how many numbers that will be in the message sequence. And they do not follow any order. For example, the sent message sequence may be: *Start 3 5 10 2 End*. What happens if you lose *Start* or *End* messages in the sequence Which one is worse: the loss of *Start* or *End* message? If the only message you receive is a 5, what can you say about the number of messages you lost?

Resources
---------

Video: The Internet: Packet, Routing and Reliability -
    <https://youtu.be/AYdF7b3nMto>
