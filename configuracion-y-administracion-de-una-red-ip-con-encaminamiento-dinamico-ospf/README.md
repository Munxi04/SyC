---
description: >-
  Todo el contenido está basado en el escenario A. Para el escenario B es todo
  igual solo que con otras tablas.
cover: ../.gitbook/assets/image (25).png
coverY: 0
layout:
  cover:
    visible: true
    size: full
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

# Configuración y administración de una red IP con encaminamiento dinámico: OSPF

La primera sesión no tocamos ospf. Primero hay que [configurar los routers](conexion-desde-putty.md).

Una vez todas las interfaces están configuradas, nos adentramos en OSPF.

***

## OSPF Monoárea

Antes de ponernos a trabajar en OSPF vamos a activar la visualización de los cambios de ospf según se prduzcan mediante el comando `debug ip ospf adj`, el cual funciona a modo de "notificación" en la que de repente la pantalla empieza a scrollear con la información de los coambios que se están guardando sobre la red.

{% code title="Confuración de OSPF" %}
```
Router>enable
Router#configure terminal
Router(config)#router ospf <process-id>
Router(config-router)#router-id <identificador>
Router(config-router)#network <ip-address> <wildcard-mask> area 0 
```
{% endcode %}

En `<process-id>` pondremos 1, por que así lo indica la práctica. En `<wildcard-mask>` pondremos la inversa de la máscara de red, para las /30 será 0.0.0.3 y para la /29 será 0.0.0.7

Para el resto necesitamos tener un parde tablas en cuenta.

{% tabs %}
{% tab title="<identificador>" %}
<div data-full-width="true">

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption><p>Router ID</p></figcaption></figure>

</div>

En nuestro caso, como somos el router PE-OESTE-A usaremos el 4.0.0.0
{% endtab %}

{% tab title="<ip-address>" %}
<figure><img src="../.gitbook/assets/image (28).png" alt="" width="517"><figcaption><p>Divisiones para la red troncal y para enlaces entre routers del escenario A</p></figcaption></figure>

En nuestro caso nos conectamos con las IPs 172.16.30.32 (toncal), 172.16.30.20 (Norte) y la 172.13.30.12 (Bilbao).
{% endtab %}
{% endtabs %}

Al finalizar esta configuración, se realizan varias capturas para comprobar que todo está correcto:

{% tabs %}
{% tab title="Show ip route" %}
<figure><img src="../.gitbook/assets/show ip route después de ospf.png" alt=""><figcaption><p>show ip route</p></figcaption></figure>
{% endtab %}

{% tab title="Show ip ospf neighbor" %}
<figure><img src="../.gitbook/assets/show ip ospf neighbor.png" alt=""><figcaption><p>show ip ospf neiphbor</p></figcaption></figure>

Con este comando podemos observar cuales son los DR y los BDR para ver las rutas que ha generado el OSPF.
{% endtab %}

{% tab title="Show ip ospf database" %}
<figure><img src="../.gitbook/assets/show ip ospf database.png" alt=""><figcaption><p>show ip ospf database</p></figcaption></figure>
{% endtab %}

{% tab title="Show ip ospf rib" %}
<figure><img src="../.gitbook/assets/show ip ospf rib.png" alt=""><figcaption><p>show ip ospf rib</p></figcaption></figure>
{% endtab %}
{% endtabs %}

***

## OSPF Multiárea

Para configurar en modo multiárea primero debemos borrar las configuraciones monoárea.

```
Router>enable
Router#configure terminal
Router(config)#no router ospf 1
```

Y a continuación, crearemos el perfil del OSPF multiárea.

```
Router#configure terminal
Router(config)#router ospf 1
Router(config-router)#router-id <identificador>
Royter(config-router)#network <ip-address> <wildcard-mask> area <area-id>
```

Usaremos las mismas imágenes para los comandos que en el monoárea, y añadimos el `<area-id>`.

{% tabs %}
{% tab title="<identificador>" %}
<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption><p>Router ID</p></figcaption></figure>
{% endtab %}

{% tab title="<ip-address>" %}
<figure><img src="../.gitbook/assets/image (28).png" alt="" width="517"><figcaption><p>Divisiones para la red troncal y para enlaces entre routers del escenario A</p></figcaption></figure>
{% endtab %}

{% tab title="<area-id>" %}
<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>OSPF multiárea</p></figcaption></figure>
{% endtab %}
{% endtabs %}

El stubby simplifica&#x20;
