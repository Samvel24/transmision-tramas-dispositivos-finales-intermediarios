# Simulación para observar la transmisión de las tramas a través de los distintos dispositivos intermediarios y finales que estén presentes en una red
En esta simulación se va a ver cómo las tramas viajan a través de los distintos dispositivos intermediarios y finales que estén presentes en la red, además se va a ver como se genera el encabezado y como va a ir cambiando en función de los dispositivos por los cuales vaya atravesando.

En esta simulación se van a colocar 4 computadoras, 2 routers y un switch y se van a realizar las conexiones respectivas, dispositivos de capas distintas se conectan con cable directo y dispositivos de la misma capa con cable cruzado, además, recordemos que una pc es similar a un router, entonces podemos considerarlos de la misma capa, por tanto podemos conectar estos dispositivos con un cable cruzado.
En packet tracer se tiene los siguientes tipos de cableados:
* Copper straight-through – cobre directo (este se muestra con una linea recta)
* Copper cross-over – cobre cruzado (este se muestra con una linea punteada)

![Dispositivos agregados al espacio de trabajo para la simulación de una red](/img/fig1.png)

Se puede observar en el espacio de trabajo que las conexiones de las computadoras con el switch, en específico en los leds, estos pasan de un estado naranja a verde de manera automática porque los switch por defecto no necesitan una configuración adicional para empezar a conmutar, en cambio los routers tienen por defecto apagados sus puertos, por tanto hay que encenderlos. Además, a diferencia de los switches, los routers necesitan una dirección IP en sus interfaces para poder empezar a funcionar, es decir, para poder levantar el servicio de red.

Vamos a colocar las etiquetas de los puertos en el espacio de trabajo, para esto vamos a dirigirnos a la pestaña opciones y después vamos a elegir preferencias.

![Elección de la opción de preferencias para mostrar las etiquetas de los puertos en los dispositivos](/img/fig2.png)

Ahora, vamos a dar clic en la opción Mostrar siempre las etiquetas de los puertos en el espacio de trabajo lógico.

![Elección de la opción de la opción para mostrar las etiquetas](/img/fig3.png)

En la red se va a colocar una dirección IP fija para cada subred, para esto vamos a usar la opción de Colocar nota. Se van a colocar 3 direcciones.

![Colocación de etiquetas con las direcciones IP para cada subred](/img/fig4.png)

Las direcciones IP son:
* 192.168.0.0/255.255.255.0
* 10.0.0.0/255.255.255.0
* 172.16.0.0/255.255.255.0

Estas direcciones se asignaron porque en un router cada uno de sus puertos tiene que estar conectado a redes distintas. Estas redes se muestran con colores diferentes en la siguiente imagen.

![Separación de las redes LAN por color para visualizar mejor cada una de ellas](/img/fig5.png)

Una vez definidas las direcciones IP de cada LAN, vamos a configurar las IP de cada computadora para la red 192.168.0.0, estas direcciones son las siguientes:
* 192.168.0.10 (PC0)
* 192.168.0.20 (PC1)
* 192.168.0.30 (PC2)

También vamos a configurar una dirección IP que va a estar asociada a un dispositivo de capa 3 que nos va a permitir ser la puerta de enlace de salida hacia otras redes, en este caso las otras redes son 10.0.0.0 y 172.16.0.0. El router conectado a la red 192.168.0.0 es el que nos va permitir conectarnos a esas otras redes. La dirección IP de la puerta de enlace es 192.168.0.1, esta dirección se establece en la sección Default Gateway de todas las computadoras.

![Configuración de la dirección IP para la puerta de enlace en la red 192.168.0.0](/img/fig6.png)

Ya que hemos configurado la dirección IP para la puerta de enlace, vamos a configurar esta dirección en el router, para esto tenemos que activar el estado del puerto Ethernet del router y luego vamos a colocar la dirección IP que hemos definido.

![Configuración de la dirección IP para la puerta de enlace en el enrutador](/img/fig7.png)

Una vez que hayamos hecho esto, se va a levantar el enlace faltante en la red 192.168.0.0, en el enlace se mostraba el led en naranja y ahora se va a mostrar en verde.

![Enlace activado entre el conmutador y el enrutador](/img/fig8.png)

Existe la posibilidad de que no se levante el enlace del router de inmediato, es decir el enlace empieza a negociar, para que este proceso sea más rápido podemos alternar entre los modos simulación y tiempo real que nos ofrece Packet tracer.

![Modo simulación y tiempo real en Packet tracer](/img/fig9.png)

El proceso descrito anteriormente, se va a realizar en la red con dirección 172.16.0.0.

En el caso del rango de red 10.0.0.0 vamos a usar las direcciones 10.0.0.1 y 10.0.0.2 para las interfaces faltantes de los routers, además debemos colocar la mascara respectiva que es 255.255.255.0.

Ya que hemos configurado todo lo relacionado a las direcciones IP, vamos a elegir la sección de simulación y vamos a editar los filtros, vamos a seleccionar ICMP y ARP, el protocolo ARP (Address Resolution Protocol) nos sirve para conseguir las direcciones MAC destino.

![Selección de los protocolos ARP e ICMP en los filtros del programa](/img/fig10.png)

Ahora, vamos a elegir la opción Inspeccionar y con ella vamos a dar clic en una computadora para que se muestre la opción de mostrar tabla ARP.

![Opción para abrir la tabla ARP de una computadora de la red](/img/fig11.png)

La tabla ARP es una cache que tienen todos los dispositivos finales, esta tabla ARP almacena una dirección IP destino, una dirección MAC y la interfaz a través de la cual llega a ese destino, esto quiere decir que si hacemos un ping desde PC0 hacia PC2, lo que va a pasar dentro del proceso de encapsulación es que la dirección MAC destino no la tiene el dispositivo, es decir, la cache ARP está vacia, entonces ocurre un tráfico de brodcast que anuncia algo a todos los dispositivos porque está buscando un destino, esto es, el origen busca la dirección MAC destino de la dirección IP a la que se desea comunicar.

Si por ejemplo, en la simulación, apuntamos a PC2 desde PC0 con un ping. Cuando se ejecuta el ping se crean 2 paquetes, el primero es el paquete ICMP que es el ping en si mismo y el segundo es un paquete ARP, estos paquetes se muestran sobre la computadora PC0, cuando damos clic sobre el paquete ARP se muestran más detalles respecto al proceso de encapsulación, los detalles que se muestran solo están en la capa 2 porque ARP es un protocolo de capa 2 y no trabaja con protocolos de capas superiores, su único fin es encontrar la dirección MAC de la dirección IP a la cual nos queremos comunicar.

![Detalles del proceso ARP trabajando en la capa 2](/img/fig12.png)

Cuando se ejecuta un ping, el paquete ICMP está pausado y solo sale el paquete ARP (este paquete se va a enviar al switch), el paquete ICMP no sale porque no tenemos la dirección MAC destino, entonces el proceso de encapsulación no se puede concluir, tenemos que esperar a que ARP vaya en búsqueda de la dirección MAC del destino, cuando tengamos esa información, entonces el paquete ICMP va a salir al destino al que queremos llegar.

Después que se haya enviado el paquete ARP al switch, se va a ejecutar un broadcast para “preguntar" si alguna de las computadoras tiene la dirección 192.168.0.30 (dirección de PC2).

![Ejecución de un broadcast para encontrar la dirección 192.168.0.30](/img/fig13.png)

Una vez enviados los paquetes, la simulación nos va a mostrar aquellas computadoras que no tienen la dirección IP que se está buscando, esto se muestra mediante un tache en aquellas computadoras que no tienen la dirección buscada. Aquellas computadoras que no tengan la dirección que se busca, van a descartar la trama que les llego.

![Las computadoras que no tienen la IP buscada avisan que no tienen esa dirección](/img/fig14.png)

En el caso de la PC2 que si es la que tiene la dirección que deseamos, se hace un proceso de desencapsulación y checa que están buscando la dirección 192.168.0.30, además esta PC observa que hay una fuente que es 192.168.0.10 y  luego desencapsula hasta la capa 2, después va a encapsular una respuesta para enviarla al dispositivo desde el que llego el ping. En la respuesta va a enviar a  192.168.0.10 que el dispositivo actual tiene la dirección MAC 00E0.A3A3.A81B (la dirección MAC de PC2) que es la que estamos buscando.

![La trama de respuesta hacia PC0 envia la dirección MAC de PC2](/img/fig15.png)

En PC2 podemos ver la cache ARP, para esto seleccionamos el botón de Inspect y luego damos clic en la PC2, con esto se va a mostrar que esta PC va a almacenar la dirección MAC y la IP de la fuente que le mando un ping, es decir, esta PC aprovecha para guardar esta información, estos datos se obtienen del encabezado de la trama que ha recibido la computadora actual.

![Caché ARP de PC2 que guarda la dirección MAC e IP desde donde se envio un ping](/img/fig16.png)

Vale la pena recordar que las direcciones MAC son direcciones físicas grabadas en las tarjetas de red, lo ideal es no cambiar estas direcciones a pesar de que sea posible, en comparación con las direcciones IP, estas últimas si se pueden cambiar en función de la necesidad que tengamos.

Cuando la información respondida por PC2 llega a PC0, podemos ver en la tabla ARP de esta última computadora que se han registrado las direcciones de la fuente (PC2), es decir, también ha almacenado datos en su caché.

![Caché ARP de PC0 que gurda las direcciones de PC2](/img/fig17.png)

Después de lo anterior, ya que PC0 tiene la dirección MAC del destino, ya se van a mandar los paquetes ICMP, estos paquetes se van a enviar a PC2 y luego se van a regresar a PC0 para confirmar que se han recibido en la computadora 2, en este proceso de envíos los datos van a pasar por el switch, sabemos que en este dispositivo los datos se desencapsulan hasta capa 2. Cuando la respuesta ha llegado a PC0, entonces va a haber un mensaje en la terminal mencionando que la computadora 2 ha respondido correctamente.

![Transmisión correcta del primer ping enviado a PC2](/img/fig18.png)

En la imagen, en los detalles de la simulación, donde se muestra el listado de paquetes, se puede observar que los paquetes ICMP han viajado desde PC0 hasta PC2 y de regreso, con lo cual se genera un mensaje en la terminal: Reply from 192.168.0.30: bytes=32 time=8ms TTL=128. Este proceso se realiza 4 veces hasta que por fin se termina el envio total del pings, cuando se ha completado el envío la terminal nos avisa de esta situación.

![Envío total de pings hacia PC2](/img/fig19.png)

La generación de la difusión ocurre cuando la primer trama sale desde PC0 para encontrar la dirección MAC destino, esto se puede comenzar a observar en el PDU del switch, el PDU de entrada tiene como dirección destino *FFFF.FFFF.FFFF*, es decir, se está generando un tráfico de difusión y la información se está enviando a todos los dispositivos, **esta información la ha puesto el protocolo ARP, este protocolo no se necesita encender, está al servicio de nuestro dispositivo.**

![Generación de una difusión por el protocolo ARP para encontrar una dirección MAC destino](/img/fig20.png)

Es importante mencionar que todos los dispositivos finales tienen una caché ARP. 

Si ejecutamos el comando ping desde PC2 y apuntamos hacia PC0 se van a enviar puros paquetes ICMP y los ARP ya no se van a enviar porque la caché ARP ya tiene las direcciones MAC entre las 2 computadoras que se están comunicando. Por cada ping que se envía hacia PC0 se van a marcar con determinado color los paquetes ICMP enviados durante la transmisión del ping, esto se puede ver en la lista de eventos.

![Paquetes ICMP del primer ping](/img/fig21.png)

![Paquetes ICMP del segundo ping](/img/fig22.png)

![Paquetes ICMP del tercer ping](/img/fig23.png)

![Paquetes ICMP del cuarto ping](/img/fig24.png)

Con todo esto, podemos observar que ya no es necesario salir a buscar las MAC destino porque el protocolo ARP ya las encontró por nosotros.

Cabe recalcar que podemos usar el botón Reset Simulation para borrar la lista de eventos de un proceso determinado para así tener limpia esa ventana de eventos y poder visualizar de mejor manera los eventos de otro proceso, en este caso para observar los eventos en los que se manda cada ping desde PC2 hasta PC0.

Cuando generamos un tráfico (ping) desde PC0 hacia PC3 que está fuera de la red, entonces de nuevo se genera un proceso ARP, esto ocurre porque sabemos que la comunicación dentro de la LAN es a través de direcciones MAC pero para dirigirnos hacia dispositivos que están fuera de la red se necesita del gateway por defecto y en la caché de PC0 no tenemos la dirección MAC del gateway. Con esto, ARP va a generar un broadcast y a quien está buscando es a 192.168.0.1 (la dirección por defecto del gateway), además, con esto se va a obtener la dirección MAC del gateway y se va a guardar en la caché de PC0.

![Generación de un broadcast para encontrar la MAC de la puerta de enlace](/img/fig25.png)

Para que la trama salga de la red LAN tenemos que ejecutar algunos comandos en la interfaz de línea de comandos de los enrutadores 0 y 1. Estos comandos se deben colocar en el modo de configuración del router, para entrar en este modo primero se debe entrar en el modo privilegiado con el comando enable y luego de ahí ya podemos entrar en el modo configuración con configure terminal, en este modo la terminal muestra el prompt como Router(config)#. Los comandos a ingresar son los siguientes.
* En el router cero vamos a colocar: *ip route 0.0.0.0 0.0.0.0 g0/0/1*
* En el router uno vamos a ejecutar: *ip route 0.0.0.0 0.0.0.0 g0/0/0*

Cuando PC3 contesta a PC0 también se va a generar un proceso ARP porque se va a enviar información a un dispositivo que está fuera de la red, entonces esta pc tiene que conocer la MAC del gateway, recordemos que la dirección MAC tiene importancia local. En el proceso descrito previamente es donde entra en juego el protocolo ARP.

A nivel de LAN los dispositivos se tienen que comunicar mediante direcciones MAC pero a nivel de red ya estamos hablando de direcciones IP, en la simulación se puede observar que cuando la información viaja desde el router hacia PC3, los detalles del PDU describen que la dirección IP fuente es la de PC0 y la dirección IP destino es la de PC3, además, en los encabezados podemos ver que están presentes las direcciones MAC para que los dispositivos se comuniquen a nivel local.

![Detalles de PDU que muestran la información en la trama, las direcciones IP se usan para comunicarse entre redes y las MAC para comunicarse a nivel local](/img/fig26.png)

Cuando el router recibe la información desde PC3, la desencapsula y la manda hacia la capa 3 en donde se va a revisar cual es la IP destino para que en función a una tabla de enrutamiento IP, pueda llegar a la dirección 192.168.0.10 (PC0). Para abrir la tabla de enrutamiento, vamos a usar el botón Inspect de Packet Tracer y vamos a dar clic en el enrutador para poder elegir la opción Routing table.

![Opción para mostrar la tabla de enrutamiento](/img/fig27.png)

En la tabla podemos ver la dirección 0.0.0.0 que se utiliza como un comodín, es decir, todas las redes que no conozca el enrutador las va enviar por el puerto gigabit 0/0/0.

![Tabla de enrutamiento del enrutador 1](/img/fig28.png)

Es importante mencionar que en la simulación se puede observar que debido a que ha habido un tiempo de demora, la información de los pings se pierde, esto se puede observar en la terminal cuando se ejecuta el comando ping, sin embargo, no todos los pings se van a perder, algunos si van a ser transmitidos correctamente.

![El tiempo de demora hace que se pierdan algunos pings](/img/fig29.png)

En resumen, el viaje que realiza la información desde PC0 hasta PC3 se va desencapsulando y encapsulando en cada dispositivo intermediario por el que va pasando, en caso de los routers esto sucede hasta la capa 3 y en el caso de los conmutadores ocurre hasta la capa 2. Además, todo el tiempo se van modificando las direcciones MAC en el encabezado de la trama, esto nos permite transmitir la información de manera correcta y de manera local en cada LAN, por último, para que una LAN pueda comunicarse con el exterior, tenemos que utilizar los routers para que estos agreguen un encabezado IP en la capa 3 y con esto la información puede llegar a diferentes redes LAN.

