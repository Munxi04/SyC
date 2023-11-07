---
description: >-
  Esto es lo más importante de la configuración, aquí se configura todo el
  escenario de red SIP.
cover: ../.gitbook/assets/image (7).png
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

# Freepbx

## Extensiones

Para crear una extensión, y que se pueda conectar un usuario, las direcciones son:

Applications -> Extensions -> Add Extension -> Add New SIP Extension

Una vez aquí solo se edita la pestaña "General". Los campos que hemos editado son:

* User Extension: El "número de teléfono" del usuario.
* Display Name y Outbound CID: El nombre con el que identificaremos el softphone.
* Secret: Campo contraseña para la posterior conexión desde[ 3CX](softphones.md).&#x20;

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>

Dependiendo de la sede en la que te encuentres según el guión de la práctica conectarás una extensión u otra. Es necesario cambiar la clave (campo Secret) para poder conectar el softphone de manera sencilla, en un sistema real habría que dejarla puesta para añadir seguridad al servicio.

## Trunks

Para crear un trunk (camino de interconexión), y que se puedan hacer llamadas entre sedes, las direcciones son:

Connectivity -> Trunks -> Add Trunk -> Add SIP Trunk

Aquí se editarán dos pestañas.

{% tabs %}
{% tab title="General" %}
<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>

En esta solo se necesita cambiar el nombre del trunk (campo trunk name)
{% endtab %}

{% tab title="pjsip Settings" %}
<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>

* SIP Server: dirección de la freepbx a la que quiero llamar (192.168.2.70)
* SIP Server Port: puerto conectado con el servidor físico (5060)
{% endtab %}
{% endtabs %}

Los trunks finales que deben quedar son:&#x20;

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>

Un trunk que conecta mi sede con la sede de mi misma ciudad y un trunk que me conecta con la sede de mi mismo lado (Este) que está detrás de mi.

## Outbound Routes

Las rutas se utilizan para, mediante los trunks creados, llegar a otros lugares.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>1: Madrid, 2: Valencia, 3: Sevilla, 4: Bilbao. .6: Oeste, .70: Este.</p></figcaption></figure>

{% tabs %}
{% tab title="Route Settings" %}
<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>

* Route Name: nombre identificador de la ruta.
* Trunk Sequence for Matched Routes: el trunk por el que va a pasar la llamada.
{% endtab %}

{% tab title="Dial Patterns" %}
<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>

Se añadirán las extensiones necesarias para la conexión. (914. -> extensión madrid oeste, 92. -> extensiones valencia, 93. -> extensiones sevilla, 94. -> extensiones bilbao)
{% endtab %}
{% endtabs %}

Para poder llamar a todas las extensiones de nuestro escenario necesitamos las siguientes rutas:

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>Captura hecha desde ordenador Madrid Este</p></figcaption></figure>
