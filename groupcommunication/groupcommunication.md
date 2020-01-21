Multicast: De una a muchas
==========================

![Chapter 3 image](chapter3.png)

Introducción
------------

En el capítulo anterior experimentamos con la comunicación broadcast,o de difusión, enviando mensajes a todo el mundo. En este capítulo vamos a aprender a enviar mensajes de forma que lleguen a un grupo más pequeño de gente. Para que la actividad fluya mejor vamos a organizarnos en grupos de tres parejas. 

La comunicación multicast (que también se conoce como multidifusión o comunicación de grupo) es un concepto interesante, y se usa por muchas tecnologías de Internet. Por ejemplo, permite enviar vídeos de forma muy rápida a través de Internet. En este capítulo vamos a aprender sobre:

- El concepto de *comunicación multicast* y *grupo* o *dirección multicast*

- Situaciones en las que este tipo de comunicación es útil y situaciones en las que no lo es

### ¿Qué vas a necesitar?

    3 micro:bits
    1 pizarra
    tizas o rotuladores o adhesivos para notas
    varios colegas

Antecedentes
------------

En el capítulo anterior todas las micro:bits recibían los mensajes que enviaban todas las demás micro:bits. Como experimentaste, esta situación puede ser algo confusa (¡aunque también divertida!). Hoy vamos a intentar limitar a quién puede enviar mensajes cada placa y de quién puede recibir mensajes. Esto se llama comunicación por grupos o multicast. La comunicación por grupos se usa en Internet para enviar tráfico a muchas personas al mismo tiempo. Por ejemplo, la televisión por Internet y la videoconferencia utilizan la comunicación por grupos.

!!! hint "Definición 1: _Comunicación por grupos_"
	En la comunicación por grupos o multicast un mensaje es enviado solo a los ordenadores que forman parte del grupo. 

Para ello es necesario que los mensajes lleven una etiqueta con una *dirección de grupo* o *dirección multicast*.

!!! hint "Definición 2: _Dirección de grupo_"
	Una dirección de grupo o multicast es una dirección especial que especifica que todos los dispositivos que pertenecen al grupo deberían recibir ese mensaje. 

Para establecer una dirección de grupo (o ID del grupo) vamos a utilizar de nuevo el bloque “radio establecer grupo” que está en la categoría Radio, tal como hicimos en la práctica [Broadcast: de una a todos](../broadcast/broadcast.md). El mayor reto de este capítulo es crear los grupos de comunicación correctamente. ¿Cómo aprenden los ordenadores que existe un grupo? ¿Cómo se unen a ellos? ¿Qué ocurre cuando abandonan un grupo? A lo largo de este capítulo tendrás la oportunidad de pensar sobre estas cuestiones mientras experimentas con la creación de grupos.


A programar: Creación de grupos y envío de mensajes dentro del grupo
--------------------------------------------------------------------

En primer lugar tenemos que decidir quiénes van a formar parte de cada grupo. Para ello, vamos a crear grupos de tres parejas, y cada pareja tendrá que programar una micro:bit. 

### Tarea 1: Creación de grupos

**Descripción:** En esta tarea vais a elegir un ID único para vuestro grupo, y luego tendréis que configurar las radios de de vuestras placas con este ID de grupo. Para ello se usa el bloque "radio establecer grupo" en el editor de bloques de JavaScript. Al elegir vuestro ID de grupo tenéis que lograr que sea un número único. **Ojo: ¿Qué pasaría is dos grupos eligen el mismo número? ¿cómo podríamos asegurarnos de que esto no ocurre?**

**Instrucciones:** Usad la pizarra para apuntar el ID de grupo que habéis elegido y aseguraos de que es único.

### Tarea 2: Envío y recepción de mensajes

**Descripción:** Podéis reutilizar los programas del capítulo anterior para enviar y recibir mensajes dentro de vuestro grupo. Tendréis que actualizarlos para contar el número de mensajes enviados y recibidos, de manera que podáis estar seguros de que solo estáis recibiendo los mensajes enviados desde vuestro grupo. 

**Instrucciones:** Cada pareja programa su micro:bit para enviar un número aleatorio del 0 al 9 al presionar el botón A. Las placas, además, cuando reciben un número por radio lo muestran durante 2 segundos. Al presionar el botón B muestran el número de mensajes recibidos. Y al presionar los dos botones A y B a la vez, muestran el número de mensajes enviados desde esa placa. Tras jugar a enviar mensajes desde las tres placas del grupo, comprobad que estáis recibiendo correctamente todos los mensajes del grupo y que no habéis recibido mensajes de otros grupos.


Extended activity
-----------------

!!! attention "Exercise 1"
	How easy or difficult would it be if micro:bits could create groups automatically themselves? How would they pick a group ID? How would they make sure nobody else had that number? Would broadcast be useful? Discuss with your teammates.

!!! attention "Exercise 2"
	Can a micro:bit be part of two groups or more? How would you program your micro:bit to do that?

Problems
--------

1. Fill in the blank in this sentence: “A one-to-may communication between one sender and a group of receivers is *---* communication.”

    1. unicast

    2. multicast

    3. broadcast

    4. none of the above

2. Let’s assume the group ID is 3 bits. For example, 010 is a group ID. What is the maximum number of groups can you have in a network?

3. If the group ID were 6 bits,  what is the largest group ID you could choose for your micro:bit?

4. “Compared to broadcast, the receivers in group communication receive more messages.” True or False?

Resources
---------

BBC Bitesize, Binary revision -
<http://www.bbc.co.uk/education/guides/z26rcdm/revision>
