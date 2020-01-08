Comunicación broadcast: De uno a todos
======================================

![Chapter 2 image](chapter2.png)

Introducción
------------

La comunicación inalámbrica (radio), como por ejemplo el WiFI o los teléfonos móviles, es una forma popular de conectarse a Internet. En el capítulo [Comunicación por cables](../wiredcommunication/wiredcommunication.md), ya conectaste dos placas micro:bits usando cables. Hoy las conectaremos usando las radios.

En el proceso no solo aprenders a utilizar la radio de tu micro:bit; también aprenderás acerca de la comunicación broadcast (o difusión).  Las comunicaciones inalámbricas suelen ser broadcast; es decir, una micro:bit puede enviar mensajes a todas las micro:bits. 

Resumiendo, este capítulo nos servirá para aprender:

- comunicación *inalámbrica* y cómo configurar la radio de las placas micro:bit

- el concepto de *broadcast* y *dirección broadcast*

- envir y recibir distintos tipos de mensajes (por ejemplo, un número o un texto) utilizando broadcast

- en qué ocasiones resulta útil utilizar broadcast y en cuáles no

### Qué necesitas

    2 micro:bits
    2 soportes para pilas y 4 pilas AAA
    1 colega

Antecedentes
------------

La comunicación inalámbrica utiliza radiación electromagnética (ondas de radio y microondas) para enviar información. Las ondas de radio son esencialmente ondas electromagnéticas que se emiten desde una antena (como las antenas de un router WiFi). Por tanto, la comunicación inalámbrica es siempre broadcast, en el sentido de que las señales enviadas, por ejemplo, por un router WiFI pueden ser escuchadas por cualquier dispositivo WiFi sintonizado en la misma frecuencia de radio.

!!! hint "Definición 1: _Broadcast_"
	En redes, la comunicación broadcast (o de difusión) significa que el mensaje enviado por un remitente se transmite a todos los receptores en una red.

Pero, ¿significa esto que la comunicación broadcast solo es posible con las comunicaciones inalámbricas? No, pero es más engorroso. Por ejemplo, en la comunicación por cable la comunicación broadcast es posible repitiendo el mismo mensaje en todos los cables.

Finalmente, los receptores pueden negarse a recibir mensajes de difusión si no están etiquetados con una *dirección de broadcast*.

!!! hint "Definición 2: _Dirección broadcast_"
	Una dirección broadcast (o de difusión) es una dirección especial que indica que todos los dispositivos de la red deberían recibir este mensaje.

En estos ejercicios con las placas micro:bit la dirección broadcast se va a configurar estableciendo el ID de grupo de la radio de micro:bit. Por tanto, todas las placas micro:bits deben tener el mismo ID de grupo para que la comunicación broadcast funcione. 


Programming: Receiving and sending broadcast messages
-----------------------------------------------------

In this activity, you will learn how you can receive a message from a
broadcasting micro:bit. Also, you will send broadcast messages yourself.

If you are running this activity with your teacher in a classroom, your
teacher’s micro:bit will be the broadcast sender and you will try to
receive from this micro:bit.

If you are running this activity alone or with a friend, you can find
the example codes for the broadcasting micro:bit in this folder. You can use these examples to test your receiver
code by downloading it to a second micro:bit. These files will run on
your micro:bits, but you will not be able to display the code using
the JavaScript Blocks editor.

You will complete three tasks to experiment with broadcasting:

### Task 1: Configure your radio

**Description:** For broadcast communication, you need all your
micro:bits to have the same radio group ID. This group ID will be the
broadcast address. This is like tuning into the correct channel to
receive a TV broadcast.

**Instruction:** Program your receiver micro:bit’s group ID to 0. This
is the group ID used in the example broadcast sender programs [^2]. For
this, use the code block for setting the radio group in the MakeCode JavaScript Blocks editor. It’s under
the Radio menu, as shown in the figure below. You can
learn about the radio blocks in more detail at
<https://makecode.microbit.org/reference/radio>.

![Setting the Radio group in MakeCode.](RadioSetGroup.png)

!!! note ""
	**Figure 3:** Setting the Radio group in MakeCode


### Task 2: Receive a broadcast message

**Description:** In this task, you will program your micro:bits to
receive a message from a broadcasting micro:bit. You will use the example
broadcast sender programs to test your receiver program.

When writing your receiver programs, there are two questions you need to
think about.

1. Which blocks in the JavaScript Blocks editor do you need to use to receive a radio message?

2. Using these blocks, can you receive any type of message, for
    example, a number or a string?

**Instruction:** First, you will start by programming micro:bits to
receive a number. Download *SendNumber.hex* in this folder
into your sender micro:bit. This sender program uses the radio group 0
to broadcast and sends a number between 0 and 9, whenever button A is
pressed. Program your micro:bit to receive and display a number. Test
your program using the sender micro:bit.

Second, you will program your micro:bit to receive a string. Download
*SendString.hex* under this folder into your sender micro:bit.
This program also uses radio group 0, and sends a string,
whenever button A is pressed. Program your micro:bit to receive and
display this string. Test your program using the sender micro:bit.
What did you receive?

### Task 3: Send a broadcast message

**Description:** Now it is your turn sending broadcast messages. If you
run this exercise in a large group, with several micro:bits, you should
notice that you are receiving a lot of messages! Can you guess who is
sending which message?

**Instruction:** Program your micro:bit so that it can send a number
when you press the button A and a string if you press button B. Extend
your receiver program so that you can receive and display ten numbers.

Extended activity
-----------------

!!! attention "Exercise 1"
	Extend your program in Task 2 for receiving a string. Display a “Sad” face on your micro:bit’s display until you receive a “Hello” message. Then display a “Happy” face for 2 seconds.

!!! attention "Exercise 2"
	Discuss some issues with broadcast communication. Is it always useful or necessary to send messages to everybody? What about privacy? Is this a problem that everybody receives all messages?

Problems
--------

1. Which frequency range does your micro:bit’s radio work in?

2. What is the speed of light?

3. Using the wavelength equation, calculate the wavelength of your micro:bit’s radio.

4. Is it easier to broadcast using wired or wireless communication? Why?

Resources
---------

- BBC Bitesize, The electromagnetic spectrum -
    <https://www.bbc.com/bitesize/guides/z32f4qt/revision/1>

- BBC Bitesize, An introduction to waves -
    <https://www.bbc.com/bitesize/guides/zgf97p3/revision/1>

- Video: How does Wi-Fi Work? (Brit Lab) -
    <https://youtu.be/xmabFJUKMdg>

-   Wired, Why Everything Wireless is 2.4GHz?-\
    <https://www.wired.com/2010/09/wireless-explainer/>

[^1]: Image by Dicklyon (Richard F. Lyon) - Own work, CC BY-SA 3.0,
    <https://commons.wikimedia.org/w/index.php?curid=7184592>

[^2]: If you are using your own programs to send a broadcast, you can
    select the group ID as you like.
