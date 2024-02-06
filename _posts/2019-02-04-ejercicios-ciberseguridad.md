---
title: "¿Como realizar ejercicios de Ciberseguridad?"
author: "PartyHack"
---

## Introducción

Esta nueva entrega va enfocada para las personas que están iniciándose en el área de la Ciberseguridad defensiva. Tengo la suerte de ser amigo de algunos especialistas, y he podido entender, que no hay fórmula mágica, certificación o camino rápido para lograr las habilidades en tecnologías y técnicas que se requieren para ser un mejor profesional de Ciberseguridad.

**¿Qué es un ejercicio de Ciberseguridad?** para este caso en particular, son ejercicios donde se vulneran maquinas reales preparadas para ello sobre entornos controlados, con técnicas de hacking ético, en un sentido amplio y quizás en otro capitulo podemos llevarlos al **Red-Team y Blue-Team**.

**¿Para que sirven los ejercicios de ciberseguridad?**

Estos ejercicios son un importante mecanismo para mantenernos alerta y preparados ante ciberamenazas, mejorar las técnicas, entender como se gestan ataques reales: [https://blogdelciso.com/2019/01/31/que-es-el-cyber-kill-chain/](https://blogdelciso.com/2019/01/31/que-es-el-cyber-kill-chain/){:target="_blank"}-

**El objetivo principal de entrenar las técnicas ofensivas, es para mejorar nuestras defensas, y proteger de mejor manera los activos de la organización**.

**¿Qué es un CTF?**  Capture The Flag (en español, Captura la Bandera), una serie de desafíos informáticos enfocados a la seguridad, cada vez más populares en este sector. Con ellos pondremos a prueba nuestros conocimientos, e incluso aprenderemos nuevas técnicas.

Los CTF se suelen dividir, generalmente, en las siguientes categorías:

- **Análisis Forense** [Forensics]: Lo más común; imágenes de memoria, de discos duros o capturas de red, las cuales almacenan diferentes tipos de información.
- **Criptografía** [Crypto]: Textos cifrados mediante un criptosistema determinado.
- **Esteganografía** [Stego]: Imágenes, sonidos o vídeos que ocultan información en su interior.
- **Explotación** [Pwn]: Descubrimiento de vulnerabilidades en un servidor.
- **Ingeniería Inversa** [Reversing]: Inferir en el funcionamiento del software. Lo más común, binarios de Windows y Linux.
- **Programación** [PPC]: También conocidos como PPC (Professional Programming & Coding), desafíos en los que se requiere desarrollar un programa o script que realice una determinada tarea.
- **Web**: Descubrimiento de vulnerabilidades en una aplicación Web.
- **Reconocimiento** [Recon]: Búsqueda de la bandera en distintos sitios de Internet. Para resolverlo se ofrecen pistas, tal como el nombre de una persona.
- **Trivial** [Trivia]: Diferentes preguntas relacionadas con la seguridad informática.
- **Misceláneo** [Misc]: Retos aleatorios que pueden pertenecer a distintas categorías sin especificar. (Incibe)


Finalmente si desea participar de un CTF, visite el sitio [CTFTime](http://ctftime.org/){:target="_blank"}

## ¡Manos a la Obra!

**Esto es película, ¡Sí, es Mr. Robot!**

Geektyper.com

**Esto es realidad, un día cotidiano de pruebas.**

OSX-Pentester

Primero es importante señalar, que no se necesitan grandes máquinas o servidores para realizar ejercicios de Ciberseguridad,  pero sí equipos que permitan la fluidez en las tareas que realizará. Acá van mis recomendaciones:

Si desea virtualizar, piense que debe tener un buen procesador y memoria RAM suficiente, recomiendo siempre usar:

**Virtualbox**: Oracle VM VirtualBox es un software de virtualización para arquitecturas x86/amd64. Actualmente es desarrollado por Oracle Corporation como parte de su familia de productos de virtualización. Puede bajarlo, seleccione la versión para su sistema operativo host desde: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads){:target="_blank"}

**Especificaciones técnicas de Hardware mínimas:**

- Cualquiera equipo Laptop o PC, con un procesador desde i5
- Un disco duro de 250 Gigas idealmente
- Memoria ram sobre 4 gigas para OS nativos, sobre 8 gigas para virtualizar.
- Una tarjeta Wireless que soporte modo monitor

### Especificaciones técnicas de Software:

En este punto hay cientos de voces distintas, según lo que he podido ver y considerar que es lo aceptable, para partir, encarecidamente sugiero alguna maquina basada en Linux o BSD, pre-cargada con herramientas que van a servir en sus tareas próximas.

- **Kali Linux**: es una distribución basada en Debian GNU/Linux diseñada principalmente para la auditoría y seguridad informática en general. Fue fundada y es mantenida por Offensive Security Ltd.
	- Pueden bajar las ISO desde acá: [https://www.kali.org/downloads/](https://www.kali.org/downloads/){:target="_blank"}
	- Y la máquina virtual preparada desde acá: [https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/){:target="_blank"}
- **Parrot Security OS**:Parrot Security OS es una distribución de Linux basada en Debian con un enfoque en la seguridad informática. Está diseñado para pruebas de penetración, evaluación y análisis de vulnerabilidades, análisis forense de computadoras, navegación web anónima, y practicar criptografía. Es desarrollado por el Frozenbox Team
	- Pueden bajar las ISO desde acá: [https://www.parrotsec.org/download-security.php](https://www.parrotsec.org/download-security.php){:target="_blank"}
	- Y la máquina virtual preparada desde acá: [https://www.osboxes.org/parrot-security-os/](https://www.osboxes.org/parrot-security-os/){:target="_blank"}
- **OSX for Hackers and Pentesters**: Es una distribución basada en macOS de HighSierra totalmente personalizado para hackers y pentesters, este es un macOS personalizado único y gratuito para la comunidad de hackers. ¡Este macOS fue hecho para por airwolfx86 de Chile!
	- Pueden bajar la timemachine desde acá: **pendiente**

Si llegó hasta acá ahora ahora decida como va configurar sus herramientas, [crear una maquina virtual](https://www.youtube.com/watch?v=Ctlmi_WWUDI){:target="_blank"} o va **instalar el sistema para ciberseguridad de [forma nativa](https://www.youtube.com/watch?v=kBgST-NkmrI){:target="_blank"}** o va **[Dockerizar una distribución basada en Linux](https://www.youtube.com/watch?v=4vimsqDwcEE){:target="_blank"}**.

Ya tiene los materiales necesarios para partir, es necesario si sus conocimientos sobre ethical hacking, no están tan actualizados, los nivele antes de comenzar con las técnicas.

### Conocimiento minimo necesario:

Recomiendo tomar algunas lecciones sobre:

- [Fundamentos y comandos de Linux](https://www.udemy.com/courses/search/?src=ukw&q=linux){:target="_blank"}
- [Fundamentos de Networking](https://www.udemy.com/courses/search/?src=ukw&q=networking){:target="_blank"}

Luego de esos pasos, podría considerar en invertir un poco en UD, unos pocos dólares, mejoraran sus conocimiento teórico sobre lo que deberá poner en practica:

- [https://cybrary.it](https://cybrary.it/){:target="_blank"}
- [https://backtrackacademy.com/](https://backtrackacademy.com/){:target="_blank"}
- [https://www.pentesteracademy.com/](https://www.pentesteracademy.com/){:target="_blank"}
- [https://ethicalhackersacademy.com/](Geektyper.com){:target="_blank"}
- Y también en Udemy puede buscar [cursos](https://www.udemy.com/courses/search/?src=ukw&q=hacking+ethico)(:target="_blank"} con buena puntación.
- También puede ver el webinar de nuestro amigo Agustin Salas: [https://www.youtube.com/watch?v=kuuB0te91mo](https://www.youtube.com/watch?v=kuuB0te91mo){:target="_blank"}

Planteare dos escenarios posibles para realizar estos ejercicios de manera OFF-LINE a través de sistemas preparado para ello como son:

### Plataformas OFF-Line para ejercicios de Ciberseguridad

- **Metasploitable**: Es un entorno de prueba, proporciona un lugar seguro para realizar pruebas de penetración e investigación de seguridad.
	- Descarga: [https://github.com/rapid7/metasploitable3](https://github.com/rapid7/metasploitable3){:target="_blank"}
- **Web Security Dojo**: El Web Security Dojo es para aprender y practicar técnicas de prueba de seguridad de aplicaciones web. Es ideal para la autoaprendizaje y la evaluación de habilidades, así como para clases de capacitación y conferencias, ya que no necesita una conexión de red. El Dojo contiene todo lo necesario para comenzar: herramientas, objetivos y documentación.
	- Descarga: [https://sourceforge.net/projects/websecuritydojo/](https://sourceforge.net/projects/websecuritydojo/){:target="_blank"}
- **DVWA Damn Vulnerable Web Application**: Es una aplicación web PHP / MySQL que es muy vulnerable. Sus objetivos principales son ser una ayuda para que los profesionales de la seguridad, para que prueben sus habilidades y herramientas en un entorno legal, ayuden a los desarrolladores web a comprender mejor los procesos de protección de las aplicaciones web y ayuden a los maestros / alumnos a enseñar / aprender la seguridad de las aplicaciones web en un entorno de clase. .
	- Descarga: [https://github.com/ethicalhack3r/DVWA](https://github.com/ethicalhack3r/DVWA){:target="_blank"}
- **OWASP Mutillidae II**: Es una aplicación web gratuita, de código abierto y deliberadamente vulnerable que proporciona un objetivo para los entusiastas de la seguridad web. Mutillidae se puede instalar en Linux y Windows usando LAMP, WAMP y XAMMP. Está preinstalado en SamuraiWTF y OWASP BWA.
	- Descarga: [https://sourceforge.net/projects/mutillidae/](https://sourceforge.net/projects/mutillidae/){:target="_blank"}
- **VulnHub**: Es otra plataforma para encontrar maquinas con las cuales practicar, tiene cientos de maquinas listas para ese fin.
	- Url: [https://www.vulnhub.com/](https://www.vulnhub.com/){:target="_blank"}
- **Pentester Labs**: Proporciona sistemas vulnerables que se pueden usar para probar y comprender vulnerabilidades. Si quieres acelerar tu curva de aprendizaje
	- Url: [https://pentesterlab.com/](https://pentesterlab.com/){:target="_blank"}

### Plataformas ON-Line para ejercicios de Ciberseguridad

También plataformas para realizar desafios de forma ON-LINE, algunas de ellas son:

- **Hack The Box**: es una plataforma en línea que le permite probar sus habilidades de prueba de penetración e intercambiar ideas y metodologías con miles de personas en el campo de la seguridad. Haga clic a continuación para atacar nuestro desafío de invitaciones, luego comience con una de nuestras muchas máquinas o desafíos en vivo.
	- URL: https://www.hackthebox.eu/
	- Nota: debes hackear el registro de usuario para ser invitado.
- AttackDefense:Es una  plataforma en linea que permite el acceso gratuito a su laboratorio de ciberseguridad. Y para esto simplemente tenemos que contar con una cuenta de correo electrónico gmail.
	- Url: https://public.attackdefense.com
	
	```
	Fuente:  https://blogdelciso.com/2019/02/03/como-realizar-ejercicios-de-ciberseguridad/
	```

	**Continuará…**
