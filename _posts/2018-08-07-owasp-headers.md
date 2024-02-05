---
title: "OWASP Secure Headers Project aplicado a WordPress"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/owasp.jpg"
---

El OWASP Secure Headers Project se basa en la idea de que establecer cabeceras HTTP en el lado servidor es fácil y no requiere cambios en el código. Una vez establecidas, dichas cabeceras pueden restringir a los navegadores modernos de manera que no caigan en vulnerabilidades muy comunes como Cross-site scripting, Clickjacking , etc.

El OWASP Secure Headers Project busca aumentar la conciencia entre aquellos que se dedican al ámbito web y fomentar el uso de la siguiente lista de cabeceras propuestas:

1. HTTP Strict Transport Security (HSTS)
2. Public Key Pinning Extension for HTTP (HPKP)
3. X-Frame-Options
4. X-XSS-Protection
5. X-Content-Type-Options
6. Content-Security-Policy
7. X-Permitted-Cross-Domain-Policies
8. Referrer-Policy

Las cabeceras pueden ser implementadas en el servidor en archivos .htaccess, modificado archivos de configuración o directamente en el código del sitio web.   Una buena manera de evaluar la seguridad de las cabeceras es https://securityheaders.com/ donde al poner el sitio web será clasificado desde una F a una A+   Un ejercicio entretenido y muy revelador es evaluar paginas de comercio online, bancos y en especial sitios propios.   WordPress es uno de los CMS mas utilizados por lo que aplicar las recomendaciones anteriores sin usar plugins y obtener una A+ puede ser un buen ejercicio. Es posible que algunos sitios con referencias externas a otras paginas fuera del dominio presenten problemas y sea necesario ajustar agregando los enlaces de referencia permitidos. Pruebe agregando las siguientes lineas al inicio del archivo wp-config.php de su wordpress y compruebe nuevamente con https://securityheaders.com/

```
header('X-Frame-Options: SAMEORIGIN');
header( 'X-Content-Type-Options: nosniff' );
header( 'X-XSS-Protection: 1;mode=block' );
header("Strict-Transport-Security: max-age=31536000; includeSubDomains");
header("Content-Security-Policy: default-src 'self';"); // FF 23+ Chrome 25+ Safari 7+ Opera 19+
header("X-Content-Security-Policy: default-src 'self';"); // IE 10+
header("Referrer-Policy: no-referrer-when-downgrade");
header("Feature-Policy: vibrate 'self'");
```

Existen muchos parámetros y opciones de configuración de los cuales evite profundizar para abordar la idea general.

### BONUS:

Y ya que estamos tocando el archivo, les recomiendo implementar otras medidas de seguridad adicionales.

```
@ini_set('session.cookie_httponly', true);
@ini_set('session.cookie_secure', true);
@ini_set('session.use_only_cookies', true);

define('FORCE_SSL_ADMIN', true);
define('FORCE_SSL_LOGIN', true);
```
