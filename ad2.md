# Actividad dirigida 2


**Comentario sobre la AD2:**

Para hacer web scraping del medallero olímpicoo de la web del diario **El País** realizaremos los siguientes pasos:

### Importamos librerías   

En primer lugar empezamos la actividad importando la librería *request* y *beautifulsoup*, para importar los datos que queremos analizar. Además explicaremos las variables que van a formar parte de nuestra actividad. En este caso estamos hablando de **los 20 países que más medallas han obtenido en los JJOO de 2020**, siendo las variables país, oro, plata, bronce y total.

### Definimos URL

Proseguimos definiendo la URL de la que sacaremos la información del la web de [El País](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/) en este caso, los resultados de los JJOO.

### Petición a la web

Una vez definida la web, le **hacemos una petición**: **Si el estaus code no es 200 no se puede leer la página**. Esto significa que, si al leer la página el número es distinto a 200, se ha recibido la petición de manera incorrecta y por tanto esta no ha sido entendida ni aceptada por el servidor. En ese caso nos saldría el aviso ```Syntax Error = invalid syntax```. En caso de ser aceptada por el servidor, podría hacerse web scraping si el status code es 200.

Después pasamos el contenido HTML de la web a un objeto *BeautifulSoup*

### Definimos variables

Una vez hemos llevado a cabo los pasos anteriores pasamos a definir las variables. Ya que se trata de las medallas y clasificaciones de los distintos países que han participado en loos JJOO 2020, definimos las variables, que en este caso serían **país, oro, plata, bronce y total**.

Pongamos un ejemplo, en el caso de país: ```paises = html.find_all("th",{"class":"pais"})``` para país busca todos los class paises en el **th**, es decir , en la celda de encabezado de la tabla. En el caso de las medallas se buscarían en el **td**, es decir, encuentra todos los oros, bronces y platas en las celdas de datos que preceden al encabezado.

### Lanzamos la pregunta

Una vez definidas las variabes y con todos los datos por delante le hacemos la pregunta: *¿Quieres conocer los países que han obtenido más medallas en el año 2020?* Para este input establecemos una actuación por respuesta: si la respuesta es 'Sí', print *'Sí, vamos a ello'*.

### Bucle de datos

Una vez que hayamos respondido de manera afirmativa pasamos al bucle para obtener los datos: imprimimos la frase *'Resultados de los datos de los JJOO 2020'*. Utilizamos ```for i in range (20)``` para obtener los datos del medallero del los 20 países. Los bucles for repiten un bloque de códigos para los valores de una lista o range, en este caso el medallero de los países. Usamos **range** para simplificar la escritura del bucle **for**, pero debemos especificar los valores.

En el rango comprendido entre esos paises una vez terminado el bucle, imprimirá el tipo medallas que ha ganado cada país (reflejada con **%s**) y el número total de estas (reflejado con **%s**). La orden i+1 se utliza para que el bucle esté en constante movimiento entre **el rango de variables** que contiene, de modo que no se estanca y funciona hasta ofrecer todos los datos.


` ` `
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:z
  print('Qué lástima, y...')
