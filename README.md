# Proyecto 2: Incident Investigation

![Portada](img/Portada.png)

**Alumno:** Juan Manuel Cumbrera López

**Curso:** CIBER

**Fecha:** 07/11/2023

<br/>

## Parte 1: Recolección y almacenamiento de evidencias

### Recolección de evidencias

Tenemos una máquina virtual con sistema operativo Windows 7, la cual ha sido vulnerada. Nos encargan recoger y analizar las evidencias que podamos encontrar, así que para comenzar tendremos en cuenta tres puntos clave según la metodología que seguiremos, que son la volatilidad, el valor relativo probable y el esfuerzo requerido.

Dado que disponemos de una única fuente de evidencia, que es la propia máquina virtual, eso limita los puntos a tener en cuenta a la volatilidad. Dicho esto, optaremos por comenzar la extracción de evidencias haciendo uso de un dispositivo USB 2.0 de 32 GB de espacio, donde hemos depositado las herramientas necesarias.

![Herramientas](img/Herramientas1.png)

También hemos instalado la herramienta *AccessData FTK Imager* en su versión 3.1.2 en el propio dispositivo USB, de modo que podamos realizar la imagen del disco de la máquina virtual sin alterar las evidencias.

![FTKImager](img/FT_Imager_Lite.png)

Una vez que tenemos dispuestas las herramientas, conectamos el dispositivo USB a la máquina virtual, y empezamos realizando el triage con la herramienta *IRTriage-Master*, y esto se debe a que esta herramienta es capaz de extraer, entre otras cosas, registros, por lo cual al tener el mayor nivel de volatilidad según la metología propia, resultan ser los datos más prioritarios. Primeramente, rellenamos los datos del caso que nos ocupa.

![Triage1](img/Triage1.png)

Luego elegimos los datos a extraer, y procedemos con el proceso de triage.

![Triage2](img/Triage2.png)

![Triage3](img/Triage3.png)

![Triage4](img/Triage4.png)

Cuando termina el proceso, podemos ver una carpeta con la fecha y hora de la extracción como nombre, donde tenemos todos los datos extraídos.

![Triage5](img/Triage5.png)

Dentro de dicha carpeta, vemos otra con la colección de evidencias recogidas nombrada como "*Evidence*", donde podremos hallar los registros, logs, además de otros datos importantes del sistema. También vemos unos ficheros en formato txt con información del caso, así como los hashes MD5 y SHA1.

![Triage6](img/Triage6.png)

![Triage7](img/Triage7.png)

![Triage8](img/Triage8.png)

En el orden de volatilidad, de manera inmediatamente inferior, encontraríamos la memoria RAM, cuya imagen obtendremos gracias a la herramienta *Belkasoft Live RAM Capturer*, que nos proporcionará una imagen fidedigna de la memoria RAM. Después de usar este software, hemos usado *AccessData FTK Imager*, ya que este obtiene además una imagen del archivo de paginación, así como un fichero txt con los hashes computados.

**Belkasoft Live RAM Capturer**

![RAM1](img/RAM1.png)

![RAM2](img/RAM2.png)

![RAM3](img/RAM3.png)

Debido a que esta herramienta no computa los hashes, lo hemos realizado a mano usando *PowerShell*, para guardar posteriormente estos hashes en un archivo txt.

![Hash1](img/RAM-Hash_1.png)

![Hash2](img/RAM-Hash_2.png)

**AccessData FTK Imager**

Con esta herramienta simplemente hacemos clic en la opción de capturar la RAM, y esperamos a que el proceso termine satisfactoriamente. Como mencionamos con anterioridad, este software captura también el archivo de paginación.

![RAM1.1](img/RAM_1.1.png)

![RAM1.2](img/RAM_1.2.png)

![RAM1.3](img/RAM_1.3.png)

![RAM1.4](img/RAM_1.4.png)

Antes de proceder con la captura del disco, creemos conveniente capturar también la caché, cookies e historial del navegador Internet Explorer de la máquina virtual, y para ello usamos las herramientas *IECacheView*, *IECookiesView* e *IEHistoryView*. Con ellas lograremos obtener y salvar en un fichero txt los datos ya mencionados.

***Caché***

![IECache1](img/IECache1.png)

![IECache2](img/IECache2.png)

***Cookies***

![IECookies1](img/IECookies1.png)

![IECookies2](img/IECookies2.png)

***Historial***

![IEHistory1](img/IEHistory1.png)

![IEHistory2](img/IEHistory2.png)

Finalmente, debemos dirigir nuestra atención a la obtención de una imagen del disco de la máquina virtual. Cuando tratamos de llevar a cabo este proceso, nos damos cuenta que nuestro dispositivo USB dispone sólo de 28 GB de espacio, mientras que el disco completo pesa unos 34 GB, nos damos cuenta que tenemos un problema que solucionar. Además, la máquina virtual no admite ningún dispositivo USB superior a 2.0, por lo que intentamos cambiamos la compatibilidad del hardware de la máquina, adaptándolo al USB 3.0, pero no funciona.

![USB3.0-1](img/USB3.0-1.png)

![USB3.0-2](img/USB3.0-2.png)

![USB3.0-3](img/USB3.0-3.png)

También intentamos instalar un driver que nos permita detectar dispositivos USB 3.0, pero tampoco funciona. Sumado a esto, ni falta hace mencionar que todos los dispositivos USB de los que disponemos son 3.0, por lo que no teníamos nada que hacer. 

Entonces borramos la máquina y la instalamos otra vez, para comenzar con una máquina limpia y sin alterar, y realizamos los pasos anteriores sin problemas. Finalmente, llegamos a la solución, y es usar la herramienta *AccessData FTK Imager*, dado que ésta permite aplicar un gran nivel de compresión a las imágenes, por lo que podríamos obtener la imagen del disco dentro del dispositivo USB 2.0 original soin ningún problema. 

Dicho esto, comenzamos con la extracción de la susodicha imagen.

![Disco1](img/Disco1.png)

![Disco2](img/Disco2.png)

Elegimos el formato **E01** debido a que éste permite aplicar niveles de compresión a la imagen obtenida.

![Disco3](img/Disco3.png)

Luego rellenamos los datos del caso y elegimos el nivel de compresión 9, que es el máximo, no sin antes darle un nombre a la imagen que obtendremos.

![Disco4](img/Disco4.png)

![Disco5](img/Disco5.png)

También elegiremos como carpeta de destino una que creamos dentro del dispositivo USB, con el objetivo de no alterar el disco de la máquina virtual.

![Disco6](img/Disco6.png)

Terminados estos pasos, comienza la obtención y compresión de la imagen.

![Disco7](img/Disco7.png)

![Disco8](img/Disco8.png)

Finalmente logramos adquirir la tan deseada y necesaria imagen del disco duro, con su consiguiente archivo en formato txt, con información acerca de la extracción, así como los hashes computados.

![Disco9](img/Disco9.png)

![Disco10](img/Disco10.png)

Con este método hemos conseguido una imagen de 4,8 GB de un disco duro de 34 GB, lo que nos ahorra mucho espacio.