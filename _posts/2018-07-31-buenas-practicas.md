---
title: "Primeros Pasos Utilizando Buenas Practicas"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/buenas-practicas.png"
---

Administradores de Red, Encargados de Sistemas, Técnicos de Soporte, Web Masters, Desarrolladores, han sido mis colegas durante 9 años. Partí como un técnico de soporte reparando fierros viejos, pero todo el tiempo tuve la inquietud de saber que hacían mis colegas para que todo estuviera relativamente bien y si estaban consientes que solo bastaba que alguien intruso sacara información de su hábitat de trabajo sin que se dieran cuenta para utilizarla para explotar algún cavo suelto olvidado por las presiones de sacar el trabajo adelante o con el clásico **“mañana lo arreglo”**. Hace algún tiempo entiendo que la seguridad operacional debe ser proceso nativo de todos los que trabajamos en infraestructura y desarrollo.

![BUENAS PRACTICAS 1](/assets/images/post/2018/buenas-practicas.png)

## CONTRASEÑAS

Es recurrente encontrar papelitos en las oficinas, con los nombres de los servidores, direcciones de los files server, pero uno de los clásicos temas que he tenido que lidiar es mantener la misma contraseña para los usuarios especiales o también enviar por correo el password de algún sistema.

![BUENAS PRACTICAS 2](/assets/images/post/2018/contrasenas.jpg)

**Este es mi breve compilado de Contraseñas…**

En mi opinión es una buena práctica es educar al usuario extrapolando la situación a sus cuentas de Facebook, Emails, el Banco diciéndoles “Usted dejaría su cuenta y contraseña del Banco o de la Facebook anotada en un Post-it?” o Usted podría dejar la misma contraseña para todos sus acceso personales?. Hacer entender a los usuarios es crear conciencia de la seguridad de la información, crear hábitos de escritorio limpio, son conceptos que pocos grupos de TI lo tienen y que ayudarían considerablemente a subir su nivel de seguridad de la información.

## SEGURIDAD EN SERVIDORES WEB

Hoy en día, cualquier organización, independientemente del tamaño que sea, tiene su página web en un wordpress, un sistema de tickets o algún sitio de formularios para divulgar por Internet su negocio, su identidad, su imagen, etc; desde la página más estática sin ningún tipo contenido, hasta la que cuenta con capacidad para realizar operaciones dentro de ella y dar un servicio directo a los usuarios de la misma.

Por ejemplo, hace un par de días estuve en una reunión donde X empresa mostró su sistema de tickets y consulta de sus máquinas y argumentaron que era de simple el acceso al sitio, pero al primer momento noté que era una consulta a una DB y sin SSL. En base a lo aprendido todos los sitios deben tener un certificado (incluso [cloudflare](https://www.cloudflare.com/integrations/wordpress/free-ssl-certificate-wordpress/){:target="_blank"} te ayuda en esto) aun mas si tienen un formulario expuesto al menos debería tener un SSL. Luego de esto probé algo rápido del [OWASP Top-Ten](https://www.owasp.org/index.php/Top_10-2017_Top_10){:target="_blank"} y sin mayor esfuerzo listé todos sus tickets.

Primero busque y encontré el sitio…

![BUENAS PRACTICAS 3](/assets/images/post/2018/url.png)

Probé algunas cosas rápidas… y pude listar los ticket generados, encontrar ademas información que podría ocuparse en una investigación lateral.

![BUENAS PRACTICAS 4](/assets/images/post/2018/list.png)

Si solo nos detuviéramos antes de publicar los sitios y agregar tips de SecDevOps antes de exponer los sistemas se evitarían estas brechas que ademas exponen a sus clientes.

## RPD EXPUESTOS

Exponer RPD en estos días es dejar la puerta semi abierta a los ingeniosos, con el problema CredSSP, que afecta a todas las versiones de Windows a partir de Vista. El problema es crítico ya que DCE / RPC permanece activado por defecto. Ya en contexto, esto fue lo que me paso.

![BUENAS PRACTICAS 5](/assets/images/post/2018/enc.png)

Como se ve en la imagen, me llego una encuesta a mi cuenta de correo, como cualquier usuario hice clic y me llevo a la URL con la dirección publica de la empresa y después, abrí el terminal server y probé con la dirección que aparecía en la encuesta.

![BUENAS PRACTICAS 5](/assets/images/post/2018/terminal.png)

*Así es como llegue al escritorio remoto. Mala práctica entendiendo el riesgo que se tiene con esto.*

Finalmente, existen varios factores que pueden restar valor a nuestra gestión diaria como SysAdmin pero al menos debemos tener conciencia de los errores que se comenten al no tener un poco de educación en estos temas.

Reflexion…**«Al final del día, estoy aceptando una cierta cantidad de riesgo. No voy a deshacerme de todo; No voy a eliminar todos los riesgos, pero será menor la brecha que tengo».**

Nosotros somos parte de las mejoras que podamos hacer y la clave de una buena conciencia de ciberseguridad. Hoy día decir mientras más avancemos más problemas encontramos es cerrarse al comportamiento **legacy** de algunos colegas, es por eso que los problemas son los ciberdelincuentes, no la tecnología, ellos están llevando a cabo los ataques y si no ponemos en práctica y se resisten a los cambios ellos mismos serán los afectados al caer en un incidente de seguridad

**«No tienes que preocuparte solo por la tecnología; no compre los últimos dispositivos, no compre el último software, debe preocuparse por su gente, porque la gente va a romper cosas y la gente puede arreglarlas «.**
