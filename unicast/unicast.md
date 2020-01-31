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

### Desafío: filtrar emisores

**Descripción:** Hay veces en las que no quieres recibir mensajes que procedan de cualquier emisor. Para ello podrías escribir un programa de forma que solo recibas mensajes de los emisores que tú escojas. A esta lista se le suele llamar *lista blanca*.

**Instrucciones:** Amplía tu programa que recibe mensajes para comprobar si la *dirección origen* que viene en la cabecera del paquete está en la lista blanca. Si es así, se muestra el mensaje; en caso contrario, no.


Para reflexionar
----------------

!!! attention "Ejercicio 1"
	¿Podríamos poner nuestras micro:bit en modo espía para escuchar mensajes que vayan a otras personas? ¿Cómo? ¿Es esto algo ético? ¿Cómo podrías proteger tus mensajes para que otras personas no pudieran espiarlos?
	
!!! attention "Ejercicio 2"
	En lugar de usar direcciones origen y destino, podríamos lograr algo equivalente al unicast como hicimos en prácticas anteriores, estableciendo un ID de grupo de radio único con cada micro:bit con la que queramos comunicarnos. ¿Qué limitaciones presenta este enfoque?


Problemas
---------

1. En este capítulo hemos usado textos de dos letras para las direcciones. ¿Cuántas direcciones diferentes podemos tener con esta solución?

2. Al seleccionar un tamaño de las direcciones para la cabecera de tus mensajes, ¿puedes elegir el tamaño que quieras? En tu programa, ¿qué sucede si aumenta el tamaño de las direcciones a 10 letras? ¿Ves algún beneficio? ¿Hay alguna limitación?

3. ¿Cómo afecta el tamaño de la cabecera de un paquete de datos al tamaño real del paquete? Si el tamaño de tu paquete de datos fuera de 100 Bytes y el tamaño de tu cabecera fuera de 10 Bytes, ¿cuántos Bytes podrían tener como máximo los mensajes? ¿Qué sucedería si el tamaño del encabezado aumenta a 50 bytes (y se mantiene el tamaño de paquete en 100 Bytes)?
