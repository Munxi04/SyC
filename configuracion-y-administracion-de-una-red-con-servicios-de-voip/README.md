---
description: Configuración de servidores SIP
cover: ../.gitbook/assets/image_2023-10-16_174210169.png
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

# Configuración y administración de una red con servicios de VoIP

## Configuración de la sede

Usaremos una máquina virtual (Asterisk) mediante la plataforma FreePBX.

*   VM PBX FreePBX-Asterisk: El sistema operativo



    | Login | Password |
    | ----- | -------- |
    | root  | SYC      |
*   GUI FreePBX: Acceso a la configuración de la red desxde internet (192.168.2.6)



    | Login   | Password |
    | ------- | -------- |
    | freepbx | ECOMT    |

Menú `aplicaciones` después `extensiones` después `añadir extensión`. Toda esta configuración se hace en la [GUI FreePBX](freepbx.md).

## Capturas

Para campturar tráfico SIP: `tcpdump -s 0 -w /tmp/nombre-fichero.pcap`

Con WinSCP haremos como con Samba y pasaremos las capturas de la VM a el host.

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
