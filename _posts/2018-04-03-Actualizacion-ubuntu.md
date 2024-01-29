---
title: "Actualización de Seguridad para Ubuntu"
author: "Felipe Castañeda"
---

Ubuntu ha liberado dos boletines de seguridad (USN-3614-1 y USN-3613-1) para corregir múltiples problemas de seguridad para las versiones de OpenJDK (versión libre de la plataforma de desarrollo Java bajo concepto de lenguaje orientado a objetos).

En ambos boletines se destacan las siguientes correcciones:

Las clases de claves de cifrado múltiples en el componente Bibliotecas de OpenJDK no sincronizaban correctamente el acceso a sus datos internos. Un atacante podría usar esto para exponer información sensible. ([CVE-2018-2579](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2579){:target="_blank"})

El componente Hotspot de OpenJDK no validaba correctamente los usos de la invocación de la interfaz de la instrucción JVM. Un atacante podría usar esto para acceder a recursos no autorizados. ([CVE-2018-2582](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2582){:target="_blank"})

La implementación de LDAP en OpenJDK no codificaba correctamente los nombres de inicio de sesión. Un atacante remoto podría usar esto para exponer información confidencial. ([CVE-2018-2588](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2588){:target="_blank"})

La implementación del cliente DNS en OpenJDK no aleatorizaba correctamente los puertos fuente. Un atacante remoto podría usar esto para suplantar respuestas a consultas DNS hechas por aplicaciones Java. ([CVE-2018-2599](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2599){:target="_blank"})

El componente de internacionalización de OpenJDK no restringía las rutas de búsqueda cuando se cargaban clases de paquetes de recursos. Un atacante local podría usar esto para engañar a un usuario para que ejecute código malicioso. ([CVE-2018-2602](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2602){:target="_blank"})

Se descubrió que OpenJDK no restringía adecuadamente las asignaciones de memoria al analizar la entrada DER. Un atacante remoto podría usar esto para causar una denegación de servicio. ([CVE-2018-2603](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2603){:target="_blank"})

La implementación de Java Cryptography Extension (JCE) en OpenJDK en algunas situaciones no garantizaba la solidez suficiente de las claves durante el acuerdo clave. Un atacante podría usar esto para exponer información sensible. ([CVE-2018-2618](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2618){:target="_blank"})

La implementación de Java GSS en OpenJDK en algunas situaciones no manejaba adecuadamente los contextos de GSS en la biblioteca GSS nativa. Un atacante podría usar esto para acceder a recursos no autorizados. ([CVE-2018-2629](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2629){:target="_blank"})

La implementación de LDAP en OpenJDK no manejaba apropiadamente las referencias de LDAP en algunas situaciones. Un atacante podría usar esto para exponer información confidencial u obtener privilegios no autorizados. ([CVE-2018-2633](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2633){:target="_blank"})

La implementación de Java GSS en OpenJDK en algunas situaciones no aplicaba adecuadamente las credenciales del sujeto. Un atacante podría usar esto para exponer información confidencial u obtener acceso a recursos no autorizados. ([CVE-2018-2634](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2634){:target="_blank"})

El componente Java Management Extensions (JMX) de OpenJDK no aplicaba adecuadamente los filtros de deserialización en algunas situaciones. Un atacante podría usar esto para eludir las restricciones de deserialización. ([CVE-2018-2637](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2637){:target="_blank"})

Se descubrió que existía una vulnerabilidad de uso después de la liberación en el componente AWT de OpenJDK al cargar la biblioteca GTK. Un atacante podría usar esto para ejecutar código arbitrario y escapar de las restricciones de la zona de pruebas de Java.([CVE-2018-2641](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2641){:target="_blank"})

Se descubrió que, en algunas situaciones, OpenJDK no validaba correctamente los objetos al realizar la deserialización. Un atacante podría usar esto para causar una denegación de servicio (bloqueo de la aplicación o consumo excesivo de memoria). ([CVE-2018-2663](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2663){:target="_blank"})

El componente AWT de OpenJDK no restringía adecuadamente la cantidad de memoria asignada al deserializar algunos objetos. Un atacante podría usar esto para causar una denegación de servicio (consumo excesivo de memoria). ([CVE-2018-2677](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2677){:target="_blank"})

El componente JNDI de OpenJDK no restringía adecuadamente la cantidad de memoria asignada al deserializar objetos en algunas situaciones. Un atacante podría usar esto para causar una denegación de servicio (consumo excesivo de memoria). ([CVE-2018-2678](https://people.canonical.com/~ubuntu-security/cve/CVE-2018-2678){:target="_blank"})

**Versiones Afectadas de OpenJDK 7**

-Ubuntu 14.04 LTS

**Versiones Afectadas de OpenJDK 8**

- Ubuntu 17.10
- Ubuntu 16.04 LTS

*Links para Descargar la Actualización*

*Ubuntu 14.04 LTS*
- icedtea-7-jre-jamvm – 7u171-2.6.13-0ubuntu0.14.04.2
- openjdk-7-jdk – 7u171-2.6.13-0ubuntu0.14.04.2
- openjdk-7-jre – 7u171-2.6.13-0ubuntu0.14.04.2
- openjdk-7-jre-headless – 7u171-2.6.13-0ubuntu0.14.04.2
- openjdk-7-jre-lib – 7u171-2.6.13-0ubuntu0.14.04.2
- openjdk-7-jre-zero – 7u171-2.6.13-0ubuntu0.14.04.2

*Ubuntu 16.04 LTS*
- openjdk-8-jdk – 8u162-b12-0ubuntu0.16.04.2
- openjdk-8-jdk-headless – 8u162-b12-0ubuntu0.16.04.2
- openjdk-8-jre – 8u162-b12-0ubuntu0.16.04.2
- openjdk-8-jre-headless – 8u162-b12-0ubuntu0.16.04.2
- openjdk-8-jre-jamvm – 8u162-b12-0ubuntu0.16.04.2
- openjdk-8-jre-zero – 8u162-b12-0ubuntu0.16.04.2

*Ubuntu 17.10*
- openjdk-8-jdk – 8u162-b12-0ubuntu0.17.10.2
- openjdk-8-jdk-headless – 8u162-b12-0ubuntu0.17.10.2
- openjdk-8-jre – 8u162-b12-0ubuntu0.17.10.2
- openjdk-8-jre-headless – 8u162-b12-0ubuntu0.17.10.2
- openjdk-8-jre-zero – 8u162-b12-0ubuntu0.17.10.2