---
title: "Transacciones por internet en Chile"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/transacciones.jpg"
---

Los últimos acontecimientos que han afectado a la banca chilena han puesto el tema de la ciberseguridad como una prioridad, con la filtración de las [14 mil tarjetas de crédito](https://www.biobiochile.cl/noticias/nacional/chile/2018/07/25/hackers-filtran-documento-con-14-mil-tarjetas-de-credito-de-clientes-de-bancos-chilenos.shtml){:target="_blank"} las personas comunes entraron en pánico y comprendieron que los cibercriminales no discriminan entre los clientes y los bancos.

A continuación se expone una investigación realizada al principalesSistema de pago electrónico de Chile, para que cada cliente se informe que tan protegido o expuesto esta a la hora de comprar por internet.

### Compras con tarjeta de Crédito y Débito.

Realizaremos una prueba de concepto (PoC), donde comparamos las exigencias del banco B y el banco C al momento de aprobar una transacción con Tarjeta de Crédito y el mismo ejercicio con una tarjeta de Débito ambas pruebas 100% reales con mis propias tarjetas como cliente.
Su banco puede que cuente con un dispositivo Token RSA SecurID al que en nuestra prueba llamaremos Xpass de manera genérica. O es posible que cuente con una tarjeta de coordenadas o peor aun ninguno de los dos métodos para una segunda clave.

PoC 1 Transacción con Tarjeta de Crédito.

### Banco “B”

PASO 1 Seleccionar Tarjeta de Crédito

![Transaccion 1](/assets/images/post/2018/transacciones-B1.png)

PASO 2 Ingresar Numero de Tarjeta, Vencimiento, Código Verificación . Click en PAGAR

![Transaccion 2](/assets/images/post/2018/transacciones-B2.png)

PASO 3 El Banco pide ingresar Banca, Rut y Clave de Internet. Click en PAGAR

![Transaccion 3](/assets/images/post/2018/transacciones-B3.png)

PASO 4 El Banco pide ingresar los 6 dígitos del XPass

![Transaccion 5](/assets/images/post/2018/transacciones-B4.png)

PASO 5 Transacción Aprobada !

### Banco “C”

PASO 1 Seleccionar Tarjeta de Crédito

![Transaccion 5](/assets/images/post/2018/transacciones-B1.png)

PASO 2 Ingresar Numero de Tarjeta, Vencimiento, Código Verificación . Click en PAGAR

![Transaccion 6](/assets/images/post/2018/transacciones-C2.png)

PASO 3 Transacción Aprobada !

**Como podrá apreciar, el Banco “C” tiene menos requisitos para aprobar la transacción, solo pide los datos de la Tarjeta, pese a que sus clientes cuentan con un XPass.**

PoC 2: Transacción con Tarjeta de Débito.

Transacción con Tarjeta de **Débito Banco “B”**

PASO 1 Seleccionar Tarjeta de Débito

![Transaccion 7](/assets/images/post/2018/transacciones-B1.png)

PASO 2 Ingresar RUT y Numero de Tarjeta Click en PAGAR

![Transaccion 8](/assets/images/post/2018/transacciones-D2.png)

PASO 3 El Banco “B” pide ingresar Banca, Rut y Clave de Internet. Click en PAGAR

![Transaccion 9](/assets/images/post/2018/transacciones-D3.png)

PASO 4 El Banco “B” pide ingresar los 6 dígitos del XPass

![Transaccion 10](/assets/images/post/2018/transacciones-D4.png)

PASO 5 Transacción Aprobada !

Transacción con Tarjeta de **Débito Banco “C”**

PASO 1 Seleccionar Tarjeta de Débito

![Transaccion 11](/assets/images/post/2018/transacciones-B1.png)

PASO 2 Ingresar RUT Click en PAGAR

![Transaccion 12](/assets/images/post/2018/transacciones-E2.png)

PASO 3 El Banco “C” pide ingresar Clave de Internet. Click en PAGAR

![Transaccion 13](/assets/images/post/2018/transacciones-E3.png)

PASO 4 El Banco “C” pide ingresar los 6 dígitos del XPass

![Transaccion 14](/assets/images/post/2018/transacciones-E4.png)

PASO 5 Transacción Aprobada !

**Esta vez el Banco“C” si solicita el uso del Xpass, pero solo pide ingresar el RUT. En otros pruebas observe bancos que solo piden el numero de Tarjeta, el cual es mas difícil de obtener. Aun así el ideal es solicitar ambos.**

En esta prueba de concepto no se trata de decir cual banco es mejor o peor, se trata de identificar las mejores practicas para saber que pedir como clientes y el comercio electrónico pueda continuar creciendo en Chile de manera segura.

Nota: Después de la filtración de las 14mil tarjetas, el Banco C incorporo el uso de Xpass, lo cual mejora sustancialmente la seguridad y muestra que existe preocupación de mejorar los servicios a sus clientes.

**Y tu banco usa segunda clave siempre?**
