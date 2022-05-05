Este programa nos permite indexar paginas web
#Crawler
#Descripción

web = {'https://ucsp.edu.pe/cs111/index.html': """<html>
<body>
<h1>Algoritmo CS111</h1>
<p>
Aqui encontraremos más información al respecto:
<ul>
<li> <a href="https://ucsp.edu.pe/cs111/pseudocodigo.html">Pseudocódigo</a>
<li> <a href="https://ucsp.edu.pe/cs111/implementacion.html">Implementación del algoritmo</a>
<li> <a href="https://ucsp.edu.pe/cs111/python.html">Documentación de Python</a>
</ul>

Podemos revisar comentarios adicional al respecto: 
<a href="https://ucsp.edu.pe/cs111/guido.html">Guido van Rossum</a> 
y <a href="https://ucsp.edu.pe/cs111/peter.html">Peter Norvig</a>.
</body>
</html>
""",
   'https://ucsp.edu.pe/cs111/peter.html': """<html>
<body>
<h1>Peter Norvig</h1>
<p>
Peter Norvig es un científico estadounidense, investigador en ciencias de la computación. Actualmente 
es director de investigación de la empresa Google. Ha publicado unos cincuenta artículos científicos 
sobre informática, en particular en el campo de la inteligencia artificial, el procesamiento automático 
del lenguaje natural , la recuperación de información y el diseño de software.

Con muchos años de expiencia en el lenguaje <a href="https://ucsp.edu.pe/cs111/python.html">Python</a>, 
creado por <a href="https://ucsp.edu.pe/cs111/guido.html">Guido van Rossum</a>.

</body>
</html>






""",
   'https://ucsp.edu.pe/cs111/guido.html': """<html>
<body>
<h1>Guido van Rossum</h1>
<p>
El es el creador de 
<a href="https://ucsp.edu.pe/cs111/python.html">Python</a>

</body>
</html>


""",
   'https://ucsp.edu.pe/cs111/python.html': """<html>
<body>
<h1>
Lenguaje de Programación Python
</h1>
<p>

<ol>
<li> Python 2.
<li> Python 3.
</ol>

</body>
</html>

""",
   'https://ucsp.edu.pe/cs111/implementacion.html': """<html>
<body>
<h1>
La Implementación del algoritmo
</h1>
<p>

<ol>
<li> En el siguiente link <a href="https://ucsp.edu.pe/cs111/guido.html">Guido van Rossum</a>.
<li> Cree las variables de manera correcta, siguiendo los estandares.
</ol>

</body>
</html>

""",
   'https://ucsp.edu.pe/cs111/pseudocodigo.html': """<html>
<body>
<h1>
Pseudocódigo
</h1>
<p>

<ol>
<li> 'https://ucsp.edu.pe/cs111/implementacion.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
<li> 'https://ucsp.edu.pe/cs111/pseudocodigo.html'.
</ol>

</body>
</html>

"""}

#
# Ingrese su código debajo de esta linea
# ############################################################

Todas las claves son todos los urls: 

links_s = dict()
links_e = dict()
rank_s = dict()
rank_e = dict()
importancia = dict()
pags = list(web.keys())

for web, contenido in web.items():
    links = set()
    while contenido.find("https:") != -1:

        pos_inicial = contenido.find("https:")
        pos_final = contenido.find(".html") + len(".html")

        links.add(contenido[pos_inicial:pos_final])

        contenido = contenido[pos_final+1:]
    links_s[web] = tuple(links)

El numero de links salientes distintos (s)

for web, salientes in links_s.items():
    rank_s[web] = len(salientes)
    links_e[salientes] = web

for i in pags:
    rank_e[i] = 0

El numero de links entrantes distintos (e)

for links in links_e.keys():
    for i in pags:
        if i in links:
            rank_e[i] += 1

for i in pags:
    importancia[i] = rank_e[i]/(rank_s[i]+1)

Ranking de las paginas de acuerdo a su mayor valor obtenido:

lista = list(rank_s.items())
lista.sort(key = lambda x: x[1], reverse = True)
print("rank s")

for i in lista:
    print("Puesto {}: {} -> {}".format(lista.index(i)+1, i[0], i[1]))

lista = list(rank_e.items())
lista.sort(key = lambda x: x[1], reverse = True)
print("rank e")

for i in lista:
    print("Puesto {}: {} -> {}".format(lista.index(i)+1, i[0], i[1]))

lista = list(importancia.items())
lista.sort(key = lambda x: x[1], reverse = True)
print("rank importancia")

for i in lista:
    print("Puesto {}: {} -> {}".format(lista.index(i)+1, i[0], i[1]))