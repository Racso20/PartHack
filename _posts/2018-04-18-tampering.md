---
title: "Tampering, utilización y contramedidas"
author: "Nitr0X"
---

En mi primera entrada en el blog de PartyHack! escribiré sobre esta técnica que me ha dado muy buenos resultados realizando ataques manuales a aplicativos web, si bien es cierto puede ser utilizada en distintos escenarios de pentesting, hoy solo lo enfocaré a aplicativos web. Espero sea de su interés y los ayude en sus tareas de detección y explotación de bug’s.

Como dijo el gran sabio “Lo primero, es lo primero”,  definiremos básicamente que  es un Parameter Tampering, es un técnica para manipular  un aplicativo web,  permitiendo detener conexiones http o https entre el servidor y nuestro explorador favorito, a continuación una pequeña ilustración de cómo opera esta técnica.

Bueno, ahora que ya entendemos de qué se trata esto del tampering, viene su utilización, esto aplica en cualquier aplicativo web y permite realizar modificaciones de variables que pasan por diferentes métodos HTTP, como así también modificar parámetros de cabecera XHR como user-agent, referer, cookies, etc. Dejando un gran abanico de posibilidades para el tipo de pruebas que se pueden llevar a cabo.

Una de las técnicas que podemos realizar en la vida real, es modificar un parámetro de un objeto que muestra la información de nuestro perfil de usuario [id_usuario=1] y cambiarlo por [id_usuario=2] mostrando el perfil del usuario “2” lo que nos permitiría extraer la base de datos completa de los usuarios registrados en el aplicativo web. Otro ejemplo podría ser un objeto que realiza un pago de una cuenta, en donde la variable [valor_pago=$18000] corresponde al dinero que debemos pagar y la modificamos a [valor_pago=$1] y pagamos nuestra cuenta a 1 peso, y así se te pueden ocurrir diferentes tipos según lo que se necesite.

Desde el punto de vista de las herramientas, existe una gran variedad para diferentes plataformas, como por ejemplo plugins de browser, herramientas de consola, en formatos web, para Windows, Linux, BSD o MacOS, y que tienen diversas prestaciones,  las cuales se pueden acomodar a tus necesidades puntuales o capacidad de entendimiento, incluso algunas traen Decoders automáticos para variables que puedan estar cifradas o generaciones de payload que permitan inyectar parámetros aleatorios en las variables que estamos testeando. A continuación del dejo un pequeño listado que pueden utilizar

| Nombre | URL | Plataforma | Tipo |
| ----------- | -----------   | -----------  | ----------- |
| Tamper Data | https://addons.mozilla.org/es/firefox/addon/tamper-data/ | Firefox | Add-ons |
| Tamper Chrome | https://chrome.google.com/webstore/detail/tamper-chrome-extension/hifhgpdkfodlpnlmlnmhchnkepplebkb | Chrome | Extension |
| mitmproxy | https://mitmproxy.org/ | Windows | Web/Console |
| Tamper | http://tamperdata.mozdev.org/ | TOR | Add-ons |

Les recomiendo para iniciar Tamper Chrome, es bastante intuitivo y versátil, les dejo algunos screenshot.

## Pantalla de configuración

![Tampering 1](/assets/images/ima1.png)

## Pantalla de Tampering

![Tampering 2](/assets/images/ima3.png)

## Decoder Integrado

![Tampering 3](/assets/images/ima4.png)

Finalmente, las contra medidas, uffff tarea ardua, ya que es necesario tener un DevOp que tenga la seguridad en su ADN y validen todas las variables y control de acceso a datos por usuario o funciones, algo muy complejo de encontrar hoy, pero bueno, vamos con algunos ejemplos

- En el proceso de desarrollo de software se deben implementar las políticas de desarrollo seguro que permitan controlar variables que muestren información confidencial o que permitan cambiar datos que fueron escritos en disco o db’s
- Todos los datos provenientes del usuario deben ser tratados como no confiables y deben ser analizados antes de cualquier operación con ellos.
- La validación final de los datos que ingrese el usuario deben ser ejecutados por el lado del servidor de aplicaciones
- Utilizar listas negras o librerías que validen datos maliciosos por el lado del servidor de aplicaciones
- Implementar mecanismo que no permitan al atacantes realizar ataques de fuerza bruta sobre valores de variables
- Cifrar con algoritmos confiables las variables y valores que pasan por el lado del usuario sea cual sea el método http que utilices, esto demora la tarea del atacante
- Establecer controles de acceso a información sobre los perfiles de los usuarios
- Genera logs de todas las acciones que realizan los usuarios en los aplicativos web, guardando incluso user-agent, IP, cookie, referer, métodos, URL, etc. Recuerda Quien, que, cuando y como. Sirve para el forense.
- Implementar capas de seguridad que permitan detectar tiempos prolongados de request entre la petición y la respuesta
- Molestar al atacante con funciones que verifiquen la sesión cada segundo o cada 5 segundos (Ufff que molestoso es eso)

Finalmente utiliza canales seguros para realizar las peticiones del usuario al servidor y viceversa.

Finalmente les dejo algunas referencias de controles proactivos que nos  propone el proyecto OWASP:
https://www.owasp.org/index.php/OWASP_Proactive_Controls

Saludos a todos y en especial a los miembros de la comunidad @P4rtyH4ck!

**“Quemen pestañas, aplasten los dedos, fundan el cerebro y piensen como delincuentes”**
https://www.linkedin.com/in/pramirezh/ 