---
description: Desde el programa PuTTY accederemos a los routers a configurar.
cover: ../.gitbook/assets/image.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Conexión desde PuTTY

Se pueden tener abiertas hasta 4 ventanas de putty por router. Hay que tener abiertas la mía y las de mis compañeras de mi misma área. **Sólo deberé modificar cosas desde la mía**.

{% tabs %}
{% tab title="Ventana inicio PuTTY" %}
<figure><img src="../.gitbook/assets/Sesión putty.png" alt=""><figcaption><p>Configuración para abrir las ventanas necesarias</p></figcaption></figure>
{% endtab %}

{% tab title="Puerto correspondiente a cada Router" %}
<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption><p>Puertos de acceso mediante ssh</p></figcaption></figure>
{% endtab %}

{% tab title="Una vez dentro" %}
| login as | password |
| -------- | -------- |
| cisco    | cisco    |
{% endtab %}
{% endtabs %}

Como los routers vienen completamente limpios, lo primero que tenemos que hacer es ponerles  un host name:  `hostname PE_OESTE-A`. En la[ ventana de puertos](conexion-desde-putty.md#puerto-correspondiente-a-cada-router) se puden ver los hostnames de cada Router.

```
Router>enable
Router#configure terminal
Router(config)#hostname <hostname>
```

***

## Configuración de interfaces

Según el router que estemos configurando se generarán unas interfaces u otras. En mi caso me tocó el router PE\_OESTE-A.

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Como se puede observar este router tiene 2 interfaces que le conectan con CE-Bilbao, PE-Norte y Troncal: la GI0/1 y la GI0/0.

{% code title="Creación de las interfaces" %}
```
PE_OESTE-A(config)#interface GI0/1
PE_OESTE-A(config-if)#no shutdown
PE_OESTE-A(config-if)#exit

PE_OESTE-A(config)#interface GI0/0
PE_OESTE-A(config-if)#no shutdown
PE_OESTE-A(config-if)#exit
```
{% endcode %}

***

## Configuración de subinterfaces

Aquí hay que tener varias tablas en cuenta, dependiendo de la configuración de la red se completarán los comandos con unas cosas u otras.

{% code title="Comandos generales" %}
```
Router(config)#interface <subinterfaz>
Router(config-subif)#encapsulation dot1q <id-vlan>
Router(config-subif)#ip address <dir-ip> <máscara>
Router(config-subif)#end 
```
{% endcode %}

Para completar estos comandos usaremos las siguientes tablas:

{% tabs %}
{% tab title="<id-vlan>" %}
<figure><img src="../.gitbook/assets/image (27).png" alt="" width="563"><figcaption><p>Identificadores de VLAN</p></figcaption></figure>

Dependiendo con qué router esté conectada la subinterfaz que estamos configurando elegiremos una u otra. Para nuestro caso, nuestra subinterfaz 0/1.17 es un <mark style="color:blue;">enlace entre routers CE y PE</mark> y estamos conectadas con Bilbao, por lo que la vlan será la 17.
{% endtab %}

{% tab title="<dir-ip> <máscara> PE" %}
Al estar configurando nosotras un router PE, nos fijaremos en la siguiente tabla:

<figure><img src="../.gitbook/assets/image (28).png" alt="" width="517"><figcaption><p>Divisiones para la red troncal y para enlaces entre routers del escenario A</p></figcaption></figure>

Hay que tener en cuenta que la primera dirección es la que representa a la red y las siguientes imágenes:

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption><p>Detalle de numeración</p></figcaption></figure>

En nuesto caso:

* Subinterfaz 0/1.17 (CE-Bilbao\_PE-Oeste):&#x20;
  * Dirección ip -> 172.16.30.14: al ser un enlace punto a punto es un /30, tenemos 4 direcciones ip disponibles, 172.16.30.12 -> identificadora de la red, 172.16.30.13 -> es la más baja y según las imágenes debe ser la del router CE, 172.16.30.14 -> es la más alta y por lo tanto, la nuestra, 172.16.30.15 -> la de broadcast de esa red.
  * Máscara -> 255.255.255.252: el 252 identifica un /30 por que de 252 a 255 hay 4 direcciones ip.
* Subinterfaz 0/0.13 (PE-Oeste\_PE-Norte):
  * Dirección ip -> 172.16.30.21: por que viene indicado en la imágen.
  * Máscara -> 255.255.255.252.
* Subinterfaz 0/0.22 (Red Troncal):
  * Dirección ip -> 172.16.30.36: por que viene indicado así en la imágen.
  * Máscara -> 255.255.255.248: /29 -> 32-29=3 -> 2^3=8 -> de 248 a 255 hay 8 direcciones ip.
{% endtab %}

{% tab title="Tabla routers CE" %}
Estas tablas no las usamos en nuestro caso particular pero en caso de configurar un router CE si las necesitaríamos.

<figure><img src="../.gitbook/assets/image (31).png" alt="" width="563"><figcaption><p>Divisiones para obtener prefijos dentro de cada una de las sedes del escenario A</p></figcaption></figure>
{% endtab %}
{% endtabs %}

***

Para asegurarnos de que todas estas configuraciones funcionan correctamente hacemos unos pings de prueba:

<figure><img src="../.gitbook/assets/pings de prueba.png" alt=""><figcaption><p>Pings de prueba</p></figcaption></figure>

También observamos la tabla de rutas antes de meternos con OSPF para, más adelante, tener claras las diferencias con el comando `show ip route`:

<figure><img src="../.gitbook/assets/show ip route antes de ospf.png" alt=""><figcaption><p>Tabla de rutas antes de OSPF</p></figcaption></figure>
