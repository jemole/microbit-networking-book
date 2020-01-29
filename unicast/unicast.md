Comunicación unicast: de una a una
==================================

![Chapter 5 image](chapter5.png)

Introducción
------------

La comunicación unicast, enviar mensajes a un único receptor, es la forma habitual de comunicación en Intenet. Por ejemplo, para ver una página web enviamos mensajes unicast a un servidor, que a su vez nos envía la página que hay que mostrar en el navegador.

En este capítulo vamos a enviar mensajes unicast a la placa micro:bit de otro compañero. Y en el proceso vamos a aprender ideas y conceptos fundamentales de las redes de ordenadores, incluyendo:

- el concepto de *unicast*

- el concepto de *protocolo*

- el concepto de *dirección* y *dirección IP*

- el concepto de *paquete de datos* y de *cabecera*

### Qué vas a necesitar:

    2 micro:bits
    1 pizarra
    rotuladores/notas adhesivas
    1 colega

Antecedentes
------------

Este capítulo trata de la comunicación unicast. Así que, ¿qué es unicast?

!!! hint "Definición 1: _Unicast_"
	Transmisión de un mensaje a un único receptor.

Para transmitir mensajes de unos a otros, los ordenadores usan *protocolos*.

!!! hint "Definición 2: _Protocolo_"
	Un conjunto de reglas que establece cómo se envían mensajes a través de una red.

Es decir, que los protocolos definen la forma en que los ordenadores deberían enviar los mensajes y lo que deberían hacer cuando reciben un mensaje. En Internet, todos los ordenadores o dispositivos siguen el protocolo IP: Internet Protocol.

De acuerdo al protocolo IP, cada dispositivo recibe una *dirección* que debe ser única y que se llama *dirección IP*. Las *direcciones IP* se usan para implementar la comunicación unicast en Internet.

!!! hint "Definición 3: _dirección IP_"
	Un texto único que identifica ordenadores que usan el protocolo IP para comunicarse en una red. Este texto se compone de cuatro números entre 0 y 255 y separados por puntos. Por ejemplo, 213.248.234.11 es una dirección IP.

Las placas micro:bit también tienen direcciones (pero son un poco diferentes). Y en prácticas anteriores ya hemos modificado parcialmente la dirección de nuestras placas al cambiar el ID de grupo de radio.

Cuando dos ordenadores se comunican, el emisor envía un paquete de datos al receptor.

!!! hint "Definición 4: _Paquete de datos_" 
	Un paquete de datos es un conjunto de datos que se envía por una red. Este conjunto de datos se compone de una parte de mensaje real (por ejemplo, una imagen o un texto) y de una o más cabeceras. Una cabecera, o encabezado, contiene información necesaria definida por el protocolo, como por ejemplo, las direcciones IP origen y destino.
	

![Un paquete de datos contiene un mensaje y una cabecera. Una cabecera contiene información de ayuda definida por el protocolo, como las direcciones del origen o del destino, o el tipo de información que viaja en el paquete. Cada protocolo añade diferentes tipos de cabeceras a los mensajes.](Datapacket_ES.png)

!!! note ""
	**Figura 1:** Un paquete de datos contiene un mensaje y una cabecera. Una cabecera contiene información de ayuda definida por el protocolo, como las direcciones del origen o del destino, o el tipo de información que viaja en el paquete. Cada protocolo añade diferentes tipos de cabeceras a los mensajes.

La figura anterior muestra como los datos y una cabecera forman un paquete de datos. En esta figura además de las direcciones origen y destino, la cabecera de ejemplo también incluye el tipo de mensaje. El tipo de mensaje le dice al receptor si está recibiendo, por ejemplo, un texto o una imagen. Si te acuerdas, en los capítulos anteriores programábamos nuestra placa para recibir un tipo específico de mensaje (texto o número). Si los paquetes contienen una cabecera con información del tipo de mensaje sería ms fácil escribir el programa del receptor.

En cualquier caso, en esta práctica vas a crear paquetes de datos añadiendo una cabecera que contendrá tan solo las direcciones origen y destino, para lograr comunicación unicast entre micro:bits.

A programar: enviar y recibir mensajes unicast
----------------------------------------------

En esta práctica vamos a aprender a crear paquetes de datos que contengan una dirección origen y otra destino, de manera que podamos enviar mensajes unicast a otras micro:bits. Es decir, nuestras placas recibirán todos los mensajes, pero solamente leerán los que sean para nosotros. Es como cuando llegas al buzón de tu piso y puede que haya cartas de varios vecinos, pero solamente abres las tuyas.

### Tarea 1: Configura tu radio

**Descripción:** Para recibir cualquier paquete, sin importar quién lo envíe, hay que usar broadcast como modo de comunicación. 

**Instrucciones:** Establece el ID de radio de grupo a 0, como hicimos en la práctica 
[Broadcast](../broadcast/broadcast.md).

### Tarea 2: Diseña tu cabecera

**Descripción:** La micro:bit emisora tiene que añadir una cabecera a cada paquete antes de enviarlo. La cabecera incluirá:

- dirección origen

- dirección destino

Para crear las cabeceras vamos a trabajar con un string (texto) algo especial. 

**Instrucciones:** En primer lugar hay que elegir la dirección de cada placa. Podemos usar dos letras, como nuestras iniciales (por ejemplo, JM). Como tienen que ser únicas, las escribimos en la pizarra para que nadie se ponga la misma que tú. Por tanto, en la pizarra escribiríamos algo como "Jesús Moreno -> JM".

A continuación elige a qué persona de la clase vas a enviar un mensaje, y toma nota de su dirección. Para preparar la cabecera de cada mensaje a enviar hay que unir las direcciones origen y destino en un único texto. Para ello usaremos el bloque unir, de la categoría texto. 

### Tarea 3: Crea el paquete y envíalo

**Descripción:** Ha llegado el momento de crear el paquete. Como hemos visto antes el paquete se forma con la unión de las cabeceras y el mensaje. Así que tu paquete debe contener la siguiente información:

- dirección origen

- dirección destino

- tu mensaje

**Instrucciones:** Elige el texto que quieres enviar como tu mensaje. Por ejemplo "Hola, figura". Usa los bloques de texto para unir tu mensaje a la cabecera. 

Con esto tu micro:bit estaría lista para enviar paquetes unicast. 

### Tarea 4: Recibir un paquete

**Descripción:** Cuando la micro:bit recibe un paquete tiene que decidir si lo procesa o si lo ignora. Ten en cuenta que la micro:bit recibe un único texto, pero como conocemos el protocolo que estamos utilizando sabemos que:

- dirección origen: las primeras 2 letras

- dirección destino: las siguientes 2 letras

- mensaje: el resto

El receptor utilizará esta información para decidir qué paquetes de los recibidos van efectivamente dirigidos a ella. 


**Instrucciones:** Divide el texto recibido en variables: *dirección origen*, *dirección destino* y *mensaje*. Para ello puedes usar los bloques *subcadena* de la categoría texto.

Comprueba si la dirección destino es igual a la dirección que elegiste para tu placa. Si es así, esto significa que tu micro:bit es la destinataria correcta. Si tu micro:bit no es la destinataria, sé un buen ciudadano e ignora el mensaje. ¡Hay que ser buenos!

### Challenge: Filter senders

**Description:** Sometimes, you may not want to receive messages just
from anybody. For this, you will write a program so that you only
receive messages from two people you know. We will call this your
*allow-list* (often referred to as a *whitelist*).

**Instruction:** Extend the receiver program to also check the *sender
address* field in the header. Check whether this address is in your allow-list. If yes, display the sender address and the message. If not,
ignore the message. Test your program with addresses in and out of your
whitelist.

Extended activity
-----------------

!!! attention "Exercise 1"
	You may have written two separate programs: one for the receiver and one for the sender. Change your program so that both micro:bits can send and receive.

!!! attention "Exercise 2"
	Did you try listening out for messages sent from other micro:bits in your class? How could your program achieve this? Is this the right thing to do? How might you protect your messages from others snooping?

!!! attention "Exercise 3"
	In this chapter, we have covered one way to do a unicast: Putting sender and receiver addresses in a data packet header. But there is another way. Remember [Group communication: one to many](../groupcommunication/groupcommunication.md). If you set your group to be
	only for your pair of micro:bits, then this is like you are unicasting. To unicast like this, choose a unique group ID, like you did for group communication. Announce it on the board so that no one else uses it. Write programs for your pair of micro:bits that send and receive using this radio group ID. What are the limitations of doing unicast like this? **Hint: Think about how many possible group IDs there are. Would this be enough for everyone in the world who has a micro:bit?**

Problems
--------

1. In what ways is unicast like broadcast and group communication? In what ways is it different?

2. Which ones are not IP addresses?

    1. -1.0.0.1

    2. 278.0.10.0

    3. 104.20.14.61

    4. 127.0.0.1

    5. 161.23.84;18

    6. 161.73.246.13

    7. 104.20.14.61.15

3. In this chapter, you used two-letter strings for your addresses. How many different people can you unicast using this address size?

4. When selecting an address size for your message header, can you pick any size you like? In your program, what happens if you increase your address size to 10 letters? Do you see any benefits? Or are there any limitations?

5. How does the size of a data packet header affect the actual packet size? If your data packet size were 100 Bytes, and your header size were 10 Bytes, how big could your messages be? What happens if the header size increases to 50 Bytes?

Resources
---------

- Video: IP addresses and DNS (code.org) -
    <https://youtu.be/5o8CwafCxnU>

- Video: IP addresses (CommonCraft) -
    <https://www.commoncraft.com/video/ip-addresses>

- BBC bitesize networks -
    <http://www.bbc.co.uk/education/topics/zjxtyrd>
