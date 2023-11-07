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

# Conexión desde putty

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
