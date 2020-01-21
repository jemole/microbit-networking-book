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

**Descripción:** En esta tarea vais a elegir un ID único para vuestro grupo (un número entre 0 y 255), y luego tendréis que configurar las radios de vuestras placas con este ID de grupo. Para ello se usa el bloque "radio establecer grupo" en el editor de bloques de JavaScript. Al elegir vuestro ID de grupo tenéis que lograr que sea un número único. **Ojo: ¿Qué pasaría si dos grupos eligen el mismo número? ¿cómo podríamos asegurarnos de que esto no ocurre?** **Además, ¿Por qué crees que el ID va de 0 a 255? ¿Cuántos bits tiene la dirección de grupo en micro:bit?**

**Instrucciones:** Usad la pizarra para apuntar el ID de grupo que habéis elegido y aseguraos de que es único.

### Tarea 2: Envío y recepción de mensajes

**Descripción:** Podéis reutilizar los programas del capítulo anterior para enviar y recibir mensajes dentro de vuestro grupo. Tendréis que actualizarlos para contar el número de mensajes enviados y recibidos, de manera que podáis estar seguros de que solo estáis recibiendo los mensajes enviados desde vuestro grupo. 

**Instrucciones:** Cada pareja programa su micro:bit para enviar un número aleatorio del 0 al 9 al presionar el botón A. Las placas, además, cuando reciben un número por radio lo muestran durante 2 segundos. Al presionar el botón B muestran el número de mensajes recibidos. Y al presionar los dos botones A y B a la vez, muestran el número de mensajes enviados desde esa placa. Tras jugar a enviar mensajes desde las tres placas del grupo, comprobad que estáis recibiendo correctamente todos los mensajes del grupo y que no habéis recibido mensajes de otros grupos.


Actividades de reflexión
------------------------

!!! attention "Ejercicio 1"
	¿Sería sencillo que las placas micro:bits pudieran crear los grupos automáticamente? ¿Cómo escogerían el ID de grupo? ¿Cómo podrían asegurarse de que nadie más tiene ese númer? ¿Sería útil utilizar broadcast? Debatidlo en grupo.

!!! attention "Ejercicio 2"
	¿Podría una micro:bit formar parte de más de un grupo? ¿Cómo habría que programar la placa para lograrlo?

Problemas
---------

1. Supongamos que el ID de grupo fuera de 3 bits. Por ejemplo, sería un ID de grupo 010. ¿Cuál sería el número máximo de grupos que podríamos tener en este caso?

2. Si el ID grupo fuera de 6 bits, ¿cuál sería el ID más grande que podríamos escoger para el grupo de nuestra micro:bit?

3. “En comparación con broadcast, en la comunicación por grupos se reciben más mensajes.” ¿Verdadero o falso?
