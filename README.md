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




