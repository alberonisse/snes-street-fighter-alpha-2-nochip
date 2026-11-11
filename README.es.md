# CARTA ABIERTA A GUSTAVO FRANCO
[Português](README.md) / [English](README.en.md) / [Español](README.es.md) / [Italiano](README.it.md) / [Deutsch](README.de.md) / [简体中文](README.zh-CN.md) / [日本語](README.ja.md) / [繁體中文（香港）](README.zh-HK.md)

Solicitud de aclaración, corrección de atribución y retractación

11 de noviembre de 2026

Gustavo,

Creé este fork después de que archivaste el repositorio porque fue la única forma rápida y directa que encontré de intentar hacerte llegar esta carta lo antes posible.

Escribo para cuestionar la atribución publicada en tu repositorio, que identifica los cartuchos mencionados en la página como una comercialización de tu implementación de Street Fighter Alpha 2 sin S-DD1.

Mi declaración sobre el origen de la edición es explícita: no utilicé material de tu proyecto en la edición USA de 8 MiB con Shin Akuma y carga acelerada que proporcioné mediante mi descompresión y los parches preparados para la memoria 29LV640. Declaro que los cartuchos a los que me refiero utilizan esa edición. Cuestiono la atribución de esos cartuchos a tu proyecto sin una identificación técnica del contenido efectivamente utilizado.

Mi objetivo con esta carta es aclarar el origen de la edición en cuestión, explicar la trayectoria de mi trabajo y solicitar que la atribución pública se sustente en pruebas verificables.

## 1. LA TRAYECTORIA DE MI PROYECTO

Mi trabajo no comenzó con la puesta a disposición de los parches de 8 MiB. Hubo un proceso previo de estudio del S-DD1, desarrollo de herramientas, análisis del mapeo, montaje de placas, correcciones y pruebas en una SNES real.

El plan original incluía una PCB con CPLD, destinada a controlar el acceso a los datos y preservar los detalles de la implementación. No pretendía poner abiertamente a disposición toda esa estructura de descompresión, organización de los datos y reconstrucción.

Cuando me enteré de la publicación de tu proyecto, me sentí profundamente desmotivado. Empecé a considerar comprometido el carácter diferencial del trabajo en el que venía invirtiendo tiempo y esfuerzo. Esa fue mi percepción sobre el futuro de mi proyecto.

Fue en ese contexto cuando decidí cambiar de rumbo y poner a disposición de forma privada la descompresión y los parches de la edición de 8 MiB, para dar continuidad al trabajo ya realizado. Esa decisión no autoriza a identificar automáticamente la edición que proporcioné como una versión de tu repositorio.

## 2. CÓMO FUNCIONA MI ENFOQUE DE DESCOMPRESIÓN

En el núcleo original de sdd1_unpacker, estudié y aislé la implementación del S-DD1 existente en bsnes. Se conservaron los créditos del código: Andreas Naive por el algoritmo/implementación original y byuu por el port de bsnes. No reivindico la invención del algoritmo S-DD1.

Ese código se adaptó a una herramienta C++ independiente de la interfaz gráfica y del funcionamiento completo del emulador, con lectura validada de los datos de la ROM y tratamiento de los bancos de memoria del S-DD1.

El juego no trata toda la ROM como un único archivo comprimido. Solicita flujos específicos, normalmente durante transferencias DMA. Por eso, el trabajo implicó analizar descriptores y tablas de la ROM original, registrar solicitudes realizadas durante la ejecución y consolidar el origen, el tamaño y la configuración de los bancos de memoria.

El trace canónico de la reconstrucción histórica contiene 3.155 identidades de requests en 3.160 líneas. Las cinco líneas adicionales registran pruebas de otros puntos de llamada para solicitudes ya catalogadas. Los requests observados y las entradas inferidas estáticamente se clasifican por separado; este recuento no significa 3.155 flujos comprimidos distintos ni demuestra, por sí solo, la cobertura de todas las situaciones del juego.

La cadena del núcleo original se estructuró así: ROM original USA, análisis y traces, catálogo de requests, descompresión de los datos, organización en un nuevo layout, parches de DMA y verificaciones de la reconstrucción sin S-DD1.

Esa reconstrucción exigió distinguir la dirección de la CPU del offset en el archivo, respetar las regiones de ROM de la SNES y redirigir las rutinas tratadas hacia datos ya descomprimidos. No se reduce a aumentar el tamaño del archivo o cambiar su cabecera.

## 3. LA ADAPTACIÓN DE 8 MiB Y LA PLACA SENCILLA

La línea de 8 MiB debe distinguirse del núcleo anterior de reconstrucción de 16 MiB. Pasó por otro proceso de organización y asignación, utilizando un inventario extraído de la base de 16mb con la que realicé las pruebas y que publiqué en YouTube, además de correcciones y verificaciones posteriores. No la presento como un simple recorte del archivo de 16 MiB.

La edición se preparó para una placa sencilla, con las conexiones adecuadas y una única memoria Flash TSOP48 de 8 MiB, la 29LV640 en modo x8. Esa edición no requiere S-DD1 ni CPLD para funcionar en esa configuración y se probó en una SNES real. También se preparó la variante para una placa LoROM modificada.

Existe una diferencia objetiva con respecto a la conversión histórica de 12 MiB documentada en tu proyecto. Esa imagen de 12 MiB no puede simplemente grabarse en la 29LV640 de 8 MiB y utilizarse en la configuración que mostré. Tu propia descripción técnica detalla un mapeo específico, incluida una ventana en los bancos C0-FF:

https://github.com/snes9xgit/snes9x/issues/1081

No estoy afirmando que tu implementación nunca pueda adaptarse a un cartucho físico, ni negando las pruebas en hardware que documentaste. Estoy distinguiendo una imagen de 12 MiB y su mapeo de la edición de 8 MiB preparada para mi configuración de placa.

Si la propuesta es ampliar el acceso al juego, considero importante reconocer también este camino: permitir que las personas utilicen una placa sencilla y componentes accesibles, sin necesidad de adquirir un flashcart específico. Ya había registrado una placa de pruebas utilizada en este trabajo; el vídeo figura en la lista al final de esta carta.

## 4. CRÉDITOS Y PRECISIÓN

La presente objeción se refiere específicamente a la edición USA de 8 MiB utilizada en los cartuchos mencionados. El origen de esa edición debe examinarse a partir de los archivos efectivamente utilizados, de sus parches y de su procedencia. No debe presumirse a partir de inventarios de otra región o de revisiones de investigación separadas, ni de la simple semejanza entre las características anunciadas.

No reivindico la autoría exclusiva del algoritmo público, de rutinas de terceros ni de los datos del juego original. Reivindico el reconocimiento correcto del trabajo de integración, adaptación, corrección y validación realizado en la edición que proporcioné.

## 5. REGISTROS PÚBLICOS PARA COMPROBAR LA CRONOLOGÍA

Presento los registros siguientes para que su contenido y sus fechas de publicación puedan contrastarse con el historial de las versiones. Documentan la trayectoria que estoy relatando; no sustituyen la comparación de los archivos efectivamente usados en el cartucho.

Placa sencilla de pruebas:
https://www.youtube.com/shorts/EVQoQB8mD1A

Registro complementario 1:
https://www.youtube.com/shorts/uhzHfQFPbVw

Registro complementario 2:
https://www.youtube.com/shorts/23gS_IEGDqc

Transmisión relacionada con el proyecto:
https://www.youtube.com/live/zakojPNeGc0

Registro complementario 3:
https://www.youtube.com/shorts/PXVAKPfAO1E

Registro complementario 4:
https://www.youtube.com/shorts/y8PAzIzPz1I

Registro complementario 5:
https://www.youtube.com/shorts/bStb8AW_QzQ

Registro complementario 6:
https://www.youtube.com/shorts/if26BECUllI

Etapa con PCB y CPLD:
https://www.youtube.com/shorts/X-Hby6Vw-m4

Vídeo que publiqué antes de la preparación y de compartir de forma privada los parches de 8 MiB:
https://www.youtube.com/shorts/YZbpycbEW0w

Demostración posterior del juego en una placa sencilla con la 29LV640:
https://www.youtube.com/shorts/GKl1eOMFks0

Mi aclaración dirigida a ti:
https://youtu.be/8X8jRSXFb5I

## 6. LO QUE SOLICITO

La publicación a la que me refiero se encuentra en:
https://github.com/gufranco/snes-street-fighter-alpha-2-nochip

Solicito que aclares qué archivo se examinó, cuál es su hash, de qué cartucho se obtuvo y qué elementos técnicos sustentaron la atribución a tu implementación.

También solicito que la comparación considere el mapeo físico, las rutinas, los parches y la revisión concreta, en lugar de tomar como prueba únicamente la descripción comercial o la presencia de características como Shin Akuma y carga acelerada.

Mientras esa identificación siga siendo cuestionada y no se haya presentado una demostración técnica, pido que la publicación deje explícita esa condición y retire la atribución categórica. Si se confirma el error, solicito la corrección de las publicaciones y una retractación con una visibilidad equivalente a la de la exposición original.

Respeto tu trabajo y solicito que también respetes el mío. No pretendo promover ataques personales ni menospreciar tu dedicación.

La cuestión que planteo es objetiva: el origen de una implementación debe demostrarse. Un resultado semejante, un nombre en un anuncio o un embalaje no sustituyen el análisis del contenido efectivamente utilizado.

Atentamente,

Responsable del proyecto ALBER MULTI HOUSE
