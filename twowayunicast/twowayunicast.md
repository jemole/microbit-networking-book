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

![Round-trip-time. Micro:bit 1 envía un mensaje *ping* a Micro:bit 2 en el momento *Tiempo\_envío*. Micro:bit 2 responde con un mensaje *pong*. Micro:bit 1 recibe el mensaje *pong* en el momento *Tiempo\_recepción*. La diferencia entre estos dos tiempos, *Tiempo\_envío* y *Tiempo\_recepción*, es el round-trip-time.](Ping-rtt_es.png)

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

En el resto de este capítulo usarás el tiempo de ejecución para calcular el RTT. Será muy útil para guardar el tiempo en el que enviaste un mensaje y también en el que recibiste un mensaje. **Ojo: guardar el tiempo significa establecer el valor de una variable para que sea igual al tiempo de ejecución actual. 


A programar: Ping
-----------------

Esta actividad se hace en parejas. Juntos vais a programar vuestras micro:bits para implementar y probar el programa Ping. Tendréis que realizar cuatro tareas:


### Tarea 1: Prearar unicast

**Descripción:** Ping usa unicast entre las micro:bits emisora y receptora. Echa un ojo a tus notas del capítulo [Unicast : De una a una](../unicast/unicast.md) para recordar cómo se implementa la comunicación unicast.

**Intrucciones:** Puedes partir del programa que desarrollaste en el capítulo anterior. Decidid qué micro:bit va a enviar los *pings* y que micro:bit va a responder con mensajes *pong*. Estableced los valores de las direcciones en base a esta decisión. Diseñad la cabecera de vuestro mensaje, tanto para el paquete *ping* como para el *pong*. 

### Tarea 2: Envía un ping

**Descripción:** El emisor del ping tiene que almacenar el tiempo justo antes de enviar un paquete *ping*. Entonces envía el paquete *ping*.

**Instrucciones:** Usa *tiempo de ejecución* para almacenar el momento en que se envía el *ping*. Envía un paquete *ping* a la micro:bit receptora.

### Tarea 3: Recibe un ping

**Descripción:** La micro:bit receptora responde al mensaje *ping* con un mensaje *pong*.

**Instrucciones**: Programa la micro:bit receptora para que envíe un paquete *pong* unicast cuando recibe un paquete *ping*. La dirección destino del paquete *pong* debe ser la dirección de origen del paquete *ping*.

### Tarea 4: Recibe un pong y calcula el round-trip-time

**Descripción:** Cuando la micro:bit emisora recibe el *pong* calcula el round-trip-time. 

**Instrucciones:** Programa la micro:bit emisora para recibir un paquete *pong*. Cuando recibe un *pong* almacena el tiempo en el que lo ha recibido usando el tiempo de ejecución. Muestra por pantalla la diferencia entre el tiempo de envío y el de recepción. Ejecuta el programa 5 veces y escribe en un cuaderno los tiempos que se muestran en la pantalla. Contesta a las siguientes preguntas: 

1. ¿Cuál fue el RTT máximo? 

2. ¿Cuál fue el RTT mínimo? 

3. ¿Cuál fue el RTT medio?

Ejercicios
----------

!!! attention "Ejercicio 1"
	Amplía tu programa ping para que envíe automáticamente más de un mensaje *Ping*. Prueba, por ejemplo, con 10 *Pings*. Calcula la media del tiempo de viaje de los mensajes.

!!! attention "Ejercicio 2"
	El programa ping informa sobre el tiempo de viaje (RTT). Pero, ¿y si calculases el tiempo que tarda solo en la ida? ¿Es posible calcular el tiempo solo de la ida o de la vuelta? En otras palabras, ¿es posible calcular el tiempo que tarda el mensaje en llegar de el emisor al receptor?
	

Problemas
---------

1. En el ejemplo de la figura del sitio <http://ping.eu/ping>, ¿qué es 172.217.23.228?

2. ¿Qué es el tiempo de viaje (RTT) y cómo se calcula?

3. Piensa en el siguiente escenario: micro:bit 1 envía un *Ping* a micro:bit 2 en el tiempo *5*. Si el RTT es *10*, ¿en qué tiempo recibió micro:bit 1 el mensaje *Pong*?

4. En el ejemplo de la figura del sitio <http://ping.eu/ping>, ¿cuál fue el RTT mínimo? ¿Cuál fue el máximo? 

5. En el ejemplo de la figura del sitio <http://ping.eu/ping>, la pérdida de paquetes fue del 0%. ¿Cuál sería el porcentaje de pérdida de paquetes si se envían 5 mensajes *Ping* y se pierden 2? 

Recursos
--------

Vídeo: What is a Ping? - <https://youtu.be/N8uT7LNVJv4>
