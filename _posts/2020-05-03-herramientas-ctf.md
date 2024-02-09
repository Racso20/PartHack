---
title: "Kit de Herramientas CTF"
author: "PartyHack"
header: 
  teaser: "/assets/images/ctf.png"
categories:
  - WriteUp
---



Para poder llevar a cabo el CTF de PartyHack es necesario tener algunas herramientas instaladas, la gran mayoría se encuentra disponible en Kali, aunque algunas es necesario instalarlas, a continuación veremos cada herramienta por categoría, descripción y cómo se usa.

## Herramientas de detección generales
Son herramientas pensadas para ejecutar al principio de cualquier reto, esto permite obtener una idea amplia de lo que está tratando de resolver.

| Herramienta | Descripción                                                                     | Cómo utilizar      |
| ----------- | ------------------------------------------------------------------------------- | -----------------  |
| file        | Muestra información sobre el tipo de archivo                                    | file stego.jpg     |
| exiftool    | Echa un vistazo a los metadatos de los archivos multimedia                      | exiftool stego.jpg |
| binwalk     | Verifica si otros archivos están incrustados y/o anexados                       | binwalk stego.jpg  |
| strings     | Verifica si hay caracteres legibles interesantes en el archivo                  | strings stego.jpg  |
| foremost    | Recortar archivos incrustados / adjuntos                                        | foremost stego.jpg |
| pngcheck    | Obtenga detalles sobre un archivo PNG (o descubra que es realmente otra cosa)   | pngcheck stego.png |
| identify    | Herramienta GraphicMagick para verificar qué tipo de imagen es un archivo. Comprueba también si la imagen está dañada. | identify -verbose stego.jpg |
| ffmpeg      | ffmpeg se puede utilizar para verificar la integridad de los archivos de audio. | ffmpeg -v info -i stego.mp3 -f null |

### Herramientas que detectan Esteganografía
Herramientas diseñadas para detectar esteganografía en archivos. En su mayoría realiza pruebas estadísticas. Revelarán mensajes ocultos solo en casos simples. Sin embargo, pueden dar pistas sobre qué buscar si encuentran irregularidades interesantes.

| Herramienta   | Tipos de archivo                    | Descripción | Cómo utilizar |
| ------------- | ----------------------------------- | ----------- | ------------- |
| stegoVeritas  | Imágenes (JPG, PNG, GIF, TIFF, BMP) | Una amplia variedad de controles simples y avanzados. Echa un vistazo stegoveritas.py -h. Comprueba los metadatos, crea muchas imágenes transformadas y las guarda en un directorio, Brute force LSB, … | stegoveritas.py stego.jpg |
| zsteg         | Imágenes (PNG, BMP)                 | Detecta varios LSB stego, también openstego y la herramienta de camuflaje | zsteg -a stego.jpg |
| stegdetect    | Imágenes (JPG)                      | Realiza pruebas estadísticas para encontrar si se utilizó una herramienta stego (jsteg, outguess, jphide, …). Consulte man stegdetect para obtener más detalles. | stegdetect stego.jpg |
| stegbreak     | Imágenes (JPG)                      | Brute force cracker para imágenes JPG. Afirma que se puede romper outguess, jphidey jsteg. | stegbreak -t o -f wordlist.txt stego.jpg |

### Herramientas que sirven para otros formatos de estenografía 

Si tiene una pista sobre qué tipo de herramienta se utilizó o qué contraseña podría ser la adecuada, pruebe estas herramientas. Algunas herramientas son compatibles con los scripts de fuerza bruta disponibles en el set de herramientas que aparece en el siguiente link: https://github.com/zardus/ctf-tools

| Herramienta   | Archivo                | Descripción | Cómo esconderse | Cómo recuperarse |
| ------------- | ---------------------- | ----------- | --------------- | ---------------- |
| AudioStego    | Audio (MP3 / WAV)      | Los detalles sobre cómo funciona están en esta publicación de blog | hideme cover.mp3 secret.txt && mv ./output.mp3 stego.mp3 | hideme stego.mp3 -f && cat output.txt |
| jsteg         | Imagen (JPG)           | Herramienta LSB stego. No encripta el mensaje. | jsteg hide cover.jpg secret.txt stego.jpg | jsteg reveal cover.jpg output.txt |
| mp3stego      | Audio (MP3)            | Viejo programa. Cifra y luego oculta un mensaje (cifrado 3DES). Herramienta de Windows ejecutándose en Wine. Requiere entrada WAV (puede arrojar errores para ciertos archivos WAV. Lo que funciona para mí es, por ejemplo:) ffmpeg -i audio.mp3 -flags bitexact audio.wav. Importante: ¡use la ruta absoluta solamente! | mp3stego-encode -E secret.txt -P password /path/to/cover.wav /path/to/stego.mp3 | mp3stego-decode -X -P password /path/to/stego.mp3 /path/to/out.pcm /path/to/out.txt |
| openstego     | Imágenes (PNG)         | Varios algoritmos LSB stego. Aún mantenido. | openstego embed -mf secret.txt -cf cover.png -p password -sf stego.png | openstego extract -sf openstego.png -p abcd -xf output.txt (¡omita -xf para crear un archivo con el nombre original!) |
| outguess      | Imágenes (JPG)         | Utiliza “bits redundantes” para ocultar datos. | outguess -k password -d secret.txt cover.jpg stego.jpg | outguess -r -k password stego.jpg output.txt |
| Stegano       | Imágenes (PNG)         | Oculta datos con varios métodos (basados ​​en LSB). Proporciona también algunas herramientas de detección. | stegano-lsb hide –input cover.jpg -f secret.txt -e UTF-8 –output stego.png o stegano-red hide –input cover.png -m «secret msg» –output stego.pngo stegano-lsb-set hide –input cover.png -f secret.txt -e UTF-8 -g $GENERATOR –output stego.png para varios generadores ( stegano-lsb-set list-generators) | stegano-lsb reveal -i stego.png -e UTF-8 -o output.txto stegano-red reveal -i stego.pngostegano-lsb-set reveal -i stego.png -e UTF-8 -g $GENERATOR -o output.txt |
| Steghide      | Imágenes (JPG, BMP)    | y audio (WAV, AU)	Herramienta versátil y madura para encriptar y ocultar datos. | steghide embed -f -ef secret.txt -cf cover.jpg -p password -sf stego.jpg | steghide extract -sf stego.jpg -p password -xf output.txt |
| cloackedpixel | Imágenes (PNG)         | LSB Stego Tool para imágenes | cloackedpixel hide cover.jpg secret.txt password crea cover.jpg-stego.png | cloackedpixel extract cover.jpg-stego.png output.txt password |
| LSBSteg       | Imágenes (PNG, BMP, …) | en formatos sin comprimir	Herramientas LSB simples con un código Python muy agradable y legible | LSBSteg encode -i cover.png -o stego.png -f secret.txt | LSBSteg decode -i stego.png -o output.txt |

### Herramientas GUI ( Interfaz gráfica de usuario) para esteganografía 

Todas las herramientas a continuación tienen interfaces gráficas de usuario y no se pueden usar a través de la línea de comando.

| Herramienta          | Tipos de archivo                         | Descripción | Cómo empezar |
| -------------------- | ---------------------------------------- | ----------- | ------------ |
Steg                   | Imágenes (JPG, TIFF, PNG, BMP)           | Maneja muchos tipos de archivos e implementa diferentes métodos | steg |
Stegsolve              | Imágenes                                 | Transformar imágenes interactivamente, ver esquemas de color por separado | stegsolve |
SonicVisualiser        | Audio                                    | Visualizar archivos de audio en forma de onda, mostrar espectrogramas | sonic-visualiser |
Stegosuite             | Imágenes (JPG, GIF, BMP)                 | Puede cifrar y ocultar datos en imágenes. Desarrollado activamente. | stegosuite |
OpenPuff               | Imágenes, audio, video (muchos formatos) | Herramienta sofisticada con larga historia. Aún mantenido. Herramienta de Windows que se ejecuta en vino. | openpuff |
DeepSound              | Audio (MP3, WAV)                         | Herramienta de Audio Stego utilizada por  Mr. Robot | DeepSound |
cloackedpixel-analizar | Imágenes (PNG)                           | Visualización LSG stego para PNG: utilícela para detectar valores LSB sospechosamente aleatorios en las imágenes (los valores cercanos a 0.5 pueden indicar que los datos cifrados están incrustados) | cloackedpixel-analyse image.png |

### Scripts de detección
Muchas de las herramientas anteriores no requieren interacción con la interfaz grafica. Por lo tanto, puede automatizar fácilmente algunos flujos de trabajo para realizar una exploración básica de los archivos que potencialmente contienen mensajes ocultos. Dado que las herramientas aplicables difieren según el tipo de archivo, cada tipo de archivo tiene diferentes scripts.
Para cada tipo de archivo, hay dos tipos de scripts:

- XXX_check.sh <stego-file>: ejecuta herramientas básicas de detección y crea un informe (+ posiblemente un directorio con informes en archivos)
- XXX_brute.sh <stego-file> <wordlist>: intenta extraer un mensaje oculto de un archivo stego con varias herramientas usando una lista de palabras ( cewl, john ycrunch se instalan para generar listas, mantenerlas pequeñas).
Los siguientes tipos de archivos son compatibles:
- JPG: *check_jpg.h y/obrute_jpg.sh*(en ejecución bruta steghide, outguess, outguess-0.13, stegbreak, stegoveritas.py -bruteLSB)
- PNG: *check_png.h y/o brute_png.sh* (ejecución bruta openstego y stegoveritas.py -bruteLSB)

### Creación de diccionarios

Las secuencias de comandos de fuerza bruta anteriormente descritas necesitan listas de palabras o diccionarios, el más común de todos es el rockyou, pero en ocasiones debemos realizar un diccionario a medida, para ello utilizaremos las siguientes herramientas.

- John : la versión mejorada de John the Ripper puede expandir tus listas de palabras. Cree una lista de palabras y úsela para crear muchas variantes.

	*uso* john -wordlist:/path/to/your/wordlist -rules:Single -stdout > /path/to/expanded/wordlist  para aplicar reglas extensas (~ x1000) john -wordlist:/path/to/your/wordlist -rules:Wordlist -stdout > /path/to/expanded/wordlist para un conjunto de reglas reducido (~ x50).
- Crunch : puede generar listas de palabras pequeñas si tiene un patrón en mente.

	Por ejemplo, si sabe que la contraseña termina en 1984 y tiene 6 letras, el uso crunch 6 6 abcdefghijklmnopqrstuvwxyz -t @@1984generará las 26 * 26 = 676 contraseñas aa1984, ab1984, … hasta zz1984.
	
	El formato es crunch <min-length> <max-length> <charset> <options> y usamos la opción de plantillas. Echa un vistazo less /usr/share/crunch/charset.lstpara ver los charsets de crunch para ver las plantillas.

- CeWL : puede generar listas de palabras si sabe que un sitio web está relacionado con una contraseña.

	Por ejemplo, ejecute cewl -d 0 -m 8 https://en.wikipedia.org/wiki/Donald_Trumpsi sospecha que una imagen de Donald Trump contiene un mensaje oculto encriptado.

	El comando raspa el sitio y extrae una lista de palabras de al menos 8 caracteres para formar un diccionario.

### Referencias

Los siguientes archivos multimedia de ejemplo están incluidos en este repositorio:
- Imagen de demostración (JPG, PNG): https://pixabay.com/p-1685092
- Archivo de sonido de demostración (MP3), WAV): https://upload.wikimedia.org/wikipedia/commons/c/c5/Auphonic-wikimedia-test-stereo.ogg — Por debuglevel (Trabajo propio) [CC BY-SA 3.0 ( https://creativecommons.org/licenses/by-sa/3.0) ], a través de Wikimedia Commons
