Prefacio
========

![Cover image](introduction/cover.png)

About the book
------------------------------------

This book presents a series of activities to teach the basics of computer networks. While you will not
learn all aspects of computer networking, we hope that it will serve as a good starting point.

To network micro:bits, we use custom micro:bit radio to radio communication. When one hears the
word radio, what comes to mind is the radio that blasts out tunes from your favourite radio broadcasting
channel. But, a radio, or a radio transceiver (transmitter/receiver), is used in communications to
generate and receive radio waves that contain information such as audio, video or digital data. And
all micro:bits have built-in radios[^1].

Each chapter presents interesting challenges in radio communications and networking with micro:bits.
After every few chapters, there’s an exciting game to look forward to! In the programming sections, you will use the JavaScript Blocks Editor at the [Microsoft Makecode site](https://makecode.microbit.org/) to develop solutions to overcome those challenges[^2]. 

Writing this book, we have assumed no knowledge of radio communications or networking. 

However, we assume that you have written programs with a micro:bit. For example, we expect that you are familiar with variables, if-then-else statements, and loops. The activities in each chapter will provide ample opportunity to put this knowledge into practice.

Editions
--------
A PDF version is available for [download](https://microbit.nominetresearch.uk/networking-book-pdf/networking_with_the_microbit.pdf).

You can buy a printed copy from [Amazon.co.uk](https://www.amazon.co.uk/Networking-micro-bit-Anthony-Kirby/dp/1973396769) or [Amazon.com](https://www.amazon.com/Networking-micro-bit-Anthony-Kirby/dp/1973396769) (this is the cheapest & most efficient way for us to make printed copies available).




About the authors
-----------------

We are researchers, which means we work on new ideas and products. Our company Nominet runs the part of the Internet that controls how names (like
[http://www.bbc.co.uk)](http://www.bbc.co.uk)) are used when people, computers, or devices like tablets or smartphones connect to
other computers over the Internet. We’re very excited to have the opportunity to work with micro:bits
and the Micro:bit Foundation.

Understanding how computers talk to each other is something that we think is important, which is why
we wrote this book! We’ve enjoyed designing the tasks and challenges in the book, and we hope you
do too.

Anthony & Cigdem

Resumen
-------

- [**Conexión de micro:bits por cables**](wiredcommunication/wiredcommunication.md)  
    Este capítulo es una introducción y una demostración divertida de las redes de ordenadores. Las placas micro:bit se pueden comunicar al conectarse mediante cables. Y a través de estos enviars imágenes entre micro:bits.

- [**Comunicación broadcast: de una a todas**](broadcast/broadcast.md)  
    Comenzars a utilizar la comunicación por radio y aprenderás acerca de la comunicación broadast. Así, una micro:bit enviará información a todas las demás micro:bits de la clase. Pero, ojo, si todas las placas hacen lo mismo es como si todos hablésemos al mismo tiempo.

- [**Comunicación por grupos: de una a muchas**](groupcommunication/groupcommunication.md)
    Formaremos grupos pequeño para enviar y recibir información de un número limitado de micro:bits. Esto es más manejable que broadcast. El reto está en elegir un identificador que sea único para tu grupo.

- [**Juego 1: Corazones agitados**](shakeydonkey/shakeydonkey.md)
    Este juego usa la radio de la micro:bit. Tras programarlo siguiendo las instrucciones, jugarás varias partidas, entenderás el código e, incluso, tratarás de hackearlo para poder ganar siempre.

- [**Comunicación unicast: de una a una**](unicast/unicast.md)
    Las comunicaciones broadcast y multicast son divertidas. Pero a veces solo quieres hablar con una persona determinada. Esto se llama comunicación unicast. Para ello, descubriremos que es necesario que cada micro:bit tenga un identificador único.

- [**Two-way Unicast**](twowayunicast/twowayunicast.md)
    It’s no use talking with somebody if you don’t get a response back. In this chapter, you will program
    your micro:bit to send a message and to get a reply. Also, you will work out how long it takes for a
    reply to come back. Doing this, you will also program one of the most important tools used in the
    Internet: Ping.

- [**Game 2: Rock-Paper-Scissors over Radio**](rockpaperscissors/rockpaperscissors.md)  
    This is not like the traditional Rock-Paper-Scissors game. It
    works over the radio!

- [**Handling errors: Retransmissions**](retransmissions/retransmissions.md)
     Nothing is perfect, not even radio communication. What happens if
    your message gets lost on the way? In this chapter, you will test
    methods for dealing with message loss. For instance, does it help if
    you send your messages more than once?

- [**Handling errors: Acknowledgements**](acknowledgements/acknowledgements.md)
    It’s a waste to retransmit if the other side already received the message! The receiver needs a
    standard reply (or an acknowledgement) to avoid this. At the sending side, if you do not receive an
    acknowledgement, you can assume that your message wasn’t received. In this chapter, you will test
    how well acknowledgments work to improve reliability.

- [**Game 3: Battleship over Radio**](battleship/battleship.md)
    You have come far. Now you are ready for another classic game!
    You will write a version of the famous Battleship game using
    your micro:bits. Your experience with radio communication and
    networking will help you along the way.

Let’s start!

[^1]: The CPU on the micro:bit is a Nordic Semiconductor nRF51822 and contains a built-in 2.4GHz radio module. This radio can be configured to run Bluetooth Low Energy
(BLE) protocol but in this book, we will use the simpler micro:bit to micro:bit communication.

[^2]: This version of the book uses JavaScript Blocks Editor; we are also working on a MicroPython version.
