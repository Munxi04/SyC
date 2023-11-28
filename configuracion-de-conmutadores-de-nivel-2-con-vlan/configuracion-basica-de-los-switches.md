---
description: >-
  Comandos necesarios para la creación de VLAN adecuadas y configurción de las
  interfaces de cada uno de los switches.
---

# Configuración básica de los switches

{% tabs %}
{% tab title="Tabla por Departamento" %}
<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Tabla por Switches" %}
<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

En todos los switches hay que introducir los siguientes comandos ([#tabla-por-departamento](configuracion-basica-de-los-switches.md#tabla-por-departamento "mention")):

{% code title="Configuración de la VLAN" %}
```
Switch>enable
Switch#configure terminal
Switch(config)#vlan <vlan-id>
Switch(config)#name <vlan-name>
Switch(config)#end
```
{% endcode %}

A contuniación, en función de si la interfaz del switch debe estar en modo trunk o en modo access se debe configurar acorde ([#tabla-por-switches](configuracion-basica-de-los-switches.md#tabla-por-switches "mention")):

{% tabs %}
{% tab title="Access" %}
```
Switch#configure terminal
Switch(config)#interface <interface-id>
Switch(config)#switchport mode access
Switch(config)#switchport access vlan <vlan-id>
Switch(config)#end
```
{% endtab %}

{% tab title="Trunk" %}
```
Switch#configure terminal
Switch(config)#interface <interface-id>
Switch(config)#switchport trunk encapsulation dot1q
Switch(config)#switchport mode trunk
Switch(config)#switchport acess vlan <vlan-id>
Switch(config)#end
```
{% endtab %}
{% endtabs %}

***

Una vez configurados todos los Switches podemos verificar el estado nuestras interfaces con el siguiente comando:

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption><p>Estado de interfaces del SW3-DC</p></figcaption></figure>

También podemos verificar la configuración de las VLANs dentro de cada Switch:

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption><p>Configuración de VLAN en SW3-DC</p></figcaption></figure>

Y el más importante de todos, podemos observar la configuración del Spanning-Tree con el comando `Switch#show spanning-tree`:

{% tabs %}
{% tab title="VLAN 200" %}
<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption><p>Ventas en SW3-DC</p></figcaption></figure>
{% endtab %}

{% tab title="VLAN 400" %}
<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption><p>Finanzas en SW3-DC</p></figcaption></figure>
{% endtab %}

{% tab title="VLAN 800" %}
<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption><p>RRHH en SW3-DC</p></figcaption></figure>
{% endtab %}
{% endtabs %}
