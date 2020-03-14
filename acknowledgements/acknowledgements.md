Gestionar errores: acuse de recibo
==================================

![Chapter 9 image](chapter9.png)

Introducción
------------

En el capítulo anterior usamos retransmisiones para gestionar los errores de transmisión. En este capítulo vamos a ir un paso más allá al usar acuses de recibo (acknowledgements o ACKs, en inglés). Y en el proceso vamos a aprender varios métodos y protocolos fundamentales para el control de errores en las redes de ordenadores.

Resumiendo, vas a aprender:

- El concepto de *acuse de recibo*

- El concepto de *Solicitud de repetición automática* o *Automatic Repeat Request (ARQ)*

- El protocolo *parada-y-espera*

### Necesitarás

    2 micro:bits
    1 colega

Antecedentes
------------

En el capítulo anterior, un mensaje se transmitía varias veces sin importar si el receptor ya había recibido una copia previamente. ¡Eso es un desperdicio! El emisor podría haber transmitido nueva información en lugar de volver a enviar estos mensajes repetidos. Y también es un incordio para el receptor, que tiene que descartar mensajes duplicados.

Para evitarlo vamos a introducir un concpeto llamado *acuse de recibo*.

!!! hint "Definición 1: _Acuse de recibo (ACK)_"
	Un acuse de recibo es un mensaje breve que el receptor envía para avisar al emisor de que recibió un mensaje. El emisor entonces se da cuenta de que no es necesario retransmitir, y estaría ya listo para enviar el siguiente mensaje.
	
Si el emisor no recibe un acuse de recibo, solo entonces retransmitiría su mensaje.

Pero, claro, ¿cuánto tiempo debería esperar el emisor a que le llegue el acuse de recibo? Esto se determina mediante un *timeout*.

!!! hint "Definición 2: _Timeout_"
	Un timeout es el tiempo permitido que puede pasar antes de que el emisor deje de esperar un acuse de recibo.
	
En otras palabras, si el emisor no recibe un acuse de recibo dentro del periodo de timeout, pensará que el paquete debe haberse perdido.

Los acuses de recibo se utilizan en método de control de errores que se llama *Solicitud de repetición automática* o *Automatic Repeat Request (ARQ)*.

!!! hint "Definición 3: _Solicitud de repetición automática (ARQ)_"
	Solicitud de repetición automática es un método de control de errores. Utiliza acuses de recibo y timeouts para retransmitir paquetes. Las retransmisiones pueden continuar hasta que el emisor recibe un acuse de recibo o bien hasta que un número máximo de retransmisiones se ha alcanzado.
	
ARQ se usa tanto en internet como en redes móviles. 

En su implementación más sencilla ARQ utiliza el protocolo de *Parada-y-Espera*

!!! hint "Definición 4: _Protocolo Parada-y-Espera_"
	En el protocolo de *Parada-y-Espera* el emisor:

	1. envía un paquete
	2. espera hasta que le llega el acuse de recibo (ACK) o se rinde después de que se cumpla el timeout
	3. si se cumple el timeout, va al paso 1
	4. si le llega el ACK, prepara un nuevo paquete y va al paso 1.

En el protocolo *Parada-y-Espera* el emisor, por tanto, no puede enviar un nuevo paquete hasta que recibe el ACK del paquete anterior.

La siguiente figura muestra un ejemplo de retransmisión exitoso. El emisor envía "Hola" y el receptor responde con un ACK. El emisor recibió el ACK antes de que se cumpliera el timeout, así que sabe que el paquete se recibió bien. Por tanto, en ese momento el emisor puede empezar en enviar otro mensaje.

![Protocolo ARQ Parada-y-Espera: El receptor envía un ACK al emisor para que el emisor sepa que el mensaje "Hola" llegó correctamente.](c9_Ack1.png)

!!! note ""
	**Figura 1:** Protocolo ARQ Parada-y-Espera: El receptor envía un ACK al emisor para que el emisor sepa que el mensaje "Hola" llegó correctamente.

Ahora vamos a ver algunos casos con errores. La figura de abajo muestra que el primer mensaje se pierde. Así que el receptor no envía el ACK. Cuando se cumple el timeout el emisor no ha recibido un ACK. Por tanto, retransmite el mensaje. El segundo intento sí tiene éxito, y el emisor recibe el ACK a tiempo (antes de cumplirse el timeout).

![Protocolo ARQ Parada-y-Espera: El mensaje se pierte, así que el emisor retransmite.](c9_Ack2.png)

!!! note ""
	**Figura 2:** Protocolo ARQ Parada-y-Espera: El mensaje se pierte, así que el emisor retransmite.

La figura siguiente muestra un ejemplo en el que el mensaje enviado por el emisor se recibe correctamente, pero el ACK enviado por el receptor se pierde. De nuevo, cuando se cumple el timeout el emisor no ha recibido el ACK. Así que retransmite el mensaje. El receptor recibe mensaje duplicado y, de nuevo, envía el ACK. Esta vez el segundo ACK llega con éxito y las cosas continúan con normalidad.

![Protocolo ARQ Parada-y-Espera: El mensaje se recibe, pero el ACK se pierde, así que el emisor retransmite.](c9_Ack3.png)

!!! note ""
	**Figura 3:** Protocolo ARQ Parada-y-Espera: El mensaje se recibe, pero el ACK se pierde, así que el emisor retransmite.
	
Estos ejemplos muestran que el protocolo ARQ Parada-y-Espera maneja las pérdidas de paquetes de datos y ACKs bastante bien. Sin embargo, ¿siempre funciona? La figura de abajo muestra un problema que puede ocurrir cuando los mensajes o ACKs se retrasan. En otras palabras, los timeouts se cumplen antes de que los ACKs puedan ser recibidos. En este ejemplo cuando el emisor envía el primer "Hola" el receptor recibe el mensaje y envía un ACK de vuelta. Pero el timeout se cumple antes de que el emisor reeciba el ACK. Así que retransmite el segundo "Hola". Y justo después, el emisor recibe el ACK retrasado. Pero, ¿a qué paquete se refiere este ACK? ¿Al primer "Hola" o al segundo? ¡Y esto es confuso también para el receptor! ¿El segundo "Hola" es un nuevo paquete o un duplicado?

![Protocolo ARQ Parada-y-Espera:¿Qué ocurre si un mensaje se retrasa? No está claro qué ACK se refiere a qué mensaje.](c9_Ack4.png)

!!! note ""
	**Figura 4:** Protocolo ARQ Parada-y-Espera:¿Qué ocurre si un mensaje se retrasa? No está claro qué ACK se refiere a qué mensaje.

Para resolver esta confusión el protocolo necesita usar números de secuencia.

!!! hint "Definición 5: _Número de secuencia_"
	Un número de secuencia es un número escogido por el emisor, e incluido en la cabecera del paquete. Cuando el receptor envía un ACK incluye el número de secuencia para decirle al emisor que recibió el paquete anterior y que está listo para el siguiente.

Por ejemplo, si el emisor envía "Hola, 0", significa que es un mensaje "Hola" con un número de secuencia 0. Al recibir este paquete el receptor enviaría "ACK, 1", que significa "he recibido el paquete 0, puedes enviarme el paquete 1". No vamos a usar números de secuencia en las tareas de esta lección, pero podrías tratar de añadirlos como actividad de extensión.


Programming: Stop and Wait!
---------------------------

To program the Stop-and-Wait ARQ protocol, you will work with a
teammate. Like in [Handling Errors: Retransmisions](../retransmissions/retransmissions.md), you will use the
custom *ErrorRadio* blocks to send messages with errors. The
communication is unicast, so you will still use source and destination
addresses in your messages. like you did in the
[Unicast communication: One to One](../unicast/unicast.md). Do not forget that your receivers need
to check if the received messages are addressed to them!

### Task 1: Design your data and ACK packets

**Description:** Before you can send and receive any packets, first you
will decide what your data and ACK packets should look like.

**Instruction:** Discuss what is the minimum information you should have
in your packets. Create two string variables for data and ACK packets, using the Text blocks in the JavaScript Blocks editor.

### Task 2: Timeout and retransmission 

**Description:** To program the Stop-and-Wait, you need a timeout
mechanism. After each transmission, you need to wait for the
ACK or time out. The main decision you need to make is
how long the timeout should be.

**Instruction:** To do this task, you may either start from scratch or
change your code from [Handling Errors: Retransmisions](../retransmissions/retransmissions.md) for the
sender micro:bit. At the sender side, program how to wait for th ACK. In the *Basic* menu, the *pause* function will
be useful for the timeout mechanism. If your pause ends before you
receive an acknowledgement, then you will retransmit the packet. If you
receive the ACK before the pause ends, you will remember this information
when the pause ends and will use it to send your next message.

To test the program, you need to also program the receiver. The receiver
sends the ACK packet for each data packet it receives.

### Task 3: Testing the reliability of Stop-and-Wait

**Description:** In this task, you will experiment with the
Stop-and-Wait protocol you programmed. For this, you will add a counter
on the sender side to count the number of retransmissions. On the
receiver side, you need a counter to understand the effect
acknowledgements on retransmissions.

**Instruction:** Decide on a timeout/pause time. Send five numbers to your teammate’s
micro:bit using the Stop-and-Wait protocol. You will run the protocol
for a fixed error value (25 and 75), repeating each experiment three
times.

In the table below, retransmissions are the number of times a packet needed to
be resent. Duplicates are the number of times the receiver received
unnecessary retransmissions. So, let’s assume, at the end, the sender
sent the following:

       1 1 1 2 2 3 4 4 4 4 5 5

There were 7
retransmissions. And the receiver received the following:

       1 2 2 3 4 5 5

Two duplicates were received. The first row of the table is filled as an example. Use your experiment results to fill in the rest. By comparing retransmissions to duplicates, discuss how good the
protocol is in handling errors.

| **Error value** | **Experiment no.** | **Retransmissions** | **Duplicates** |
|-----------------|:-------------------|:--------------------|:---------------|
| 25 | (example) | 7 | 2|
| 25 | 1 | | |
| 25 | 2 | | |
| 25 | 3 | | |
| 75 | 1 | | |
| 75 | 2 | | |
| 75 | 3 | | |

Extended activity
-----------------

!!! attention "Exercise 1"
	Discuss how acknowledgements work better than using only
	retransmissions. Do you see any problems with using acknowledgements?

!!! attention "Exercise 2"
	Discuss how the duration of the timeout period affects your protocol. 
	For instance, what happens if your timer is too short or too long? 
	What happens if acknowledgements are delayed. 

!!! attention "Exercise 3"
	Research the "Alternating Bit Protocol", which uses a 1-bit sequence number 
	to help with the problems discussed in the figures.

Problems
--------

1. What does ARQ mean?

2. In the Stop-and-Wait ARQ protocol, if 10 packets are sent, how many acknowledgements are needed?

Resources
---------

Video: The Internet: Packet, Routing and Reliability -
    <https://youtu.be/AYdF7b3nMto>
