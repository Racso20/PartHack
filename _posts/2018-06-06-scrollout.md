---
title: "ScrollOut F1 AntiSpam"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/scrollup.png"
categories:
  - Çiberseguridad
---
	

Hace un tiempo he estado en busca de algún antispam que sea confiable y fácil de administrar. Para el agrado de muchos, he dado con algo que hasta ahora me ha sorprendido, sin menospreciar a spamassassin, Mailscanner u OrangeAssassin. **Scrollout F1** es un antispam que tiene la característica de Gateway (Firewall) muy bueno, a mi opinión justo lo que necesitas en una contingencia de…. “aquellas”, en las que no quieres gastar un dineral para sustentar un servidor de correo, ni tampoco quieres perder tiempo.

Este antispam que es posible descargar desde la página [http://www.scrolloutf1.com/](http://www.scrolloutf1.com/){:target="_blank"}. Es una simple ISO que puede ser instalada como host físico, o virtual y su configuración es realmente un simple next.

Una de sus características es que:

- Posee configuración para múltiples dominios
- Ajustes de seguridad y reglas de Spam (Puedes simplemente eliminar spam sin que el usuario lo reciba)
- Configuración de cuarentena para cada dominio
- No posee límites de administración de dominios ni cuentas de usuarios
- Posee reportaría basada en LOG
- Posee su propio Dashboard
- A nivel más experto si deseas aplicar una mayor seguridad, tiene configuraciones para LDAP, AD, Zimbra.

Los requerimientos para que este sistema funcione son muy básicos y la verdad es que en una maquina con 1GB de memoria, 15 GB de HD, 1 Procesador, puede soportar hasta 5000 mensajes al día, lo que en mi caso está más que aceptable. Los invito a probar un sistema bueno que posee características profesionales, pero a costo 0.

La guía de instalación y configuración están a prueba “de”. Por lo que no fallaran en la configuración y puesta en marcha, recordar modificar sus reglas de relay en el firewall, ojo, que si la entrada de correos se encuentra directa a sus servidores, lo que no es recomendable, usa esto ¡Ya!

La instalación demora alrededor de 20 min. ya que levanta servicios de Postfix (Servidor de correo), ClamAV (Servidor de antivirus), Amavis (Filtro de Spam), entre otros, bueno espero este pequeño articulo les sirva a algunos para solucionar de manera rápida cualquier contingencia que puedan tener

Guía de instalación [http://www.scrolloutf1.com/deploy/install](http://www.scrolloutf1.com/deploy/install){:target="_blank"}

Guía de configuración [http://www.scrolloutf1.com/deploy/configure](http://www.scrolloutf1.com/deploy/configure){:target="_blank"}

![ScrollUP 1](/assets/images/post/2018/scrollup1.png)