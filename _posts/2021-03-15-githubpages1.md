---
title: Crear un blog personal con github pages y jekyll.
header:
  overlay_image: assets/images/githubpages.gif
  caption: "debateops"
categories:
  - github
tags:
  - github
  - blog
  - jekyll
---

# Usamos github pages y jekyll para crear documentación estática tanto personal como de proyectos.

## Por qué crear un blog

Queremos crear un blog personal, donde almacenar todas esas notas, esas cosas a recordar que luego nunca recordamos.
<br>
En internet hay un montón de páginas que te dicen cómo se hacen las cosas, pero siempre es buena idea, si ya has realizado algo, anotarlo, porque dentro de unos días, cuando te lo pida algún compañero, o cuando lo vuelvas a necesitar, poder recordarlo y que cueste poco tiempo resolverlo, o simplemente, no tener que volver a buscar en internet lo que ya has buscado antes.
<br>
Lo más importante que queremos almacenar es código, scripts o en todo caso queremos manejarlos como si fuera código, y como ya tenemos proyectos almacenados en github, nuestra idea es aprovechar github y la oportunidad que nos ofrece con giyhub pages para tener una web estática.

### Alternativas

El punto más importante es la elección de las herramientas, porque queremos hacer poco esfuerzo (raṕido, fácil y sencillo), reaprovechar y/o utilizar markdown que es lo que ya usamos para la documentación de proyectos.
<br>
Lo primero es saber qué repositorio se va a utilizar. Las alternativas

- Google Cloud Source Repositories es de Google y conviene si quieres integrarte con otras herramientas de google o si quieres acceder a varios diferentes repositorios (incluidos bitbucket y github)
- Bitbucket es de Altassian, y conviene si quieres integrarte con Jira, Trello u otros productos de Altassian.
- GitHub es el lider del mercado, llevo varios años teniendo proyectos en github sin problemas, por lo que no tengo motivos para cambiar.

Queremos que la documentación esté junto al código, todo en el mismo sitio, pero que sea accesible desde la web de una manera fácil. La opción más evidentee s usar github pages y usar jekyll, pero vemos alternativas.

- Hugo hecho en go, se anuncia como el más rápido.
- Hexo es node, creciente comunidad, muy popular en China.
- jekyll  es Ruby creado por  Github, para webs grandes se puede volver lento.

Como hemos apostado por github, la web no va a ser muy grande y queremos sencillez, fácil de usar, nos quedaamos con jekyll y github pages.Si crecieramos mucho y viesemos problemas, [pasaríamos a Hugo y Netlify](https://pawelgrzybek.com/from-jekyll-to-hugo-from-github-pages-to-netlify/).

## Empezamos con github
Lo primero es crearse una cuenta personal donde alojar el blog.
<br>
Debes de tener un usuario de github o crearte uno.
v
Es necesario crearse un repositorio con el nomnbre <ususario>.github.io que mmostrará los documentos bajo el enlace http://usuario.github.io
ahí es donde se van a alojar las páginas, como queremos varios idiomas, creamos otro repositorio llamado es, para contener los documentos en español y su enlace será http://usuario.github.io/es
<br>
Esta parte se puede configurar en github /settings
![settings github](/assets/images/github_settings.png)


## Empezamos con jekyll

### Instalamos jekyll

Usamos un ordenador con ubuntu y para instalar ruby 
```script
sudo apt-get install ruby-full build-essential zlib1g-dev
```
después ya se puede instalar jekyll
```script
gem install jekyll bundler

```
comprobamos la versión instalada
```bash
$ jekyll -v
jekyll 4.2.0

```
[Información para windows](https://www.kiltandcode.com/2020/04/30/how-to-create-a-blog-using-jekyll-and-github-pages-on-windows/) 

### Creamos el primer blog básico

En un directorio vacío hacemos:
```bash
jekyll new jekyll-site
```
Nos crea un directorio llamado jekyll-site con los siguients ficheros con uma estructura
```
jekyll-site/
  _posts/
  index.markdown
  about.markdown
  _config.yml
  Gemfile
  404.html
```
- _posts es el sitio donde se van a dejar los post /en markdown)
- index.markdown es la página inicial, se puede modificar, pero mejor más tarde
- about.markdown es la documentación sobre e l blog, o si es un blog personal detalles del creador.
- _config.yml fichero de configuracion, en el que indicamos título del blog, email, cuetna de github de twitter los datos ficjos que se mostrarán en a web básica
<br>
Modificamos los datos de _config.yml y levantamos el servidor

```bash
cd jekyll-site/
$ bundle exec jekyll serve
Generating... 
       Jekyll Feed: Generating feed for posts
   Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.       
```
Nos conectamos a http://127.0.0.1:4000/
![Initial Start in jekyll](/assets/images/initial_jekyll.png)

Una vez creado basta con ir añadiendo nuevos post, un nuevo markdown en la carpeta _post

### Escogemos aspecto y tema de la web
Ahora que sabemos como funciona, vamos a crear el blog de verdad, para ello lo primero es escoger el tema, definir que aspecto, navegación va a tener la web, defiir los aspectos gráficos, para luego solo dedicarnos a crear markdown con post.
<br>
Podemos ver los [temas por defecto que soporta github pages](https://pages.github.com/themes/)
Pero añadieron la posibilidad de añadir temas en remoto, [posibles temas](https://jekyllthemes.io/github-pages-themes)
<br>
Miramos temas con fotos, compatibilidad con github, gratuito y buscamos ejemplos de blogs creados con ese tema, que se vean las páginas en github y github pages.
<br>
Nos gustan varios pero que se vean con ejempo reales en uso hay menos, al final, nos quedamos con https://github.com/mmistakes/minimal-mistakes
<br>
ejemplo de páginas web
- https://zenglix.github.io en [github](https://github.com/zengliX/zengliX.github.io)
- https://yxtay.github.io en [github](https://github.com/yxtay/yxtay.github.io)

como información para añadir cosas más atrayente a los [posts](https://github.com/mmistakes/minimal-mistakes/tree/gh-pages-3.1.6/_posts)
<br>
Como navegación queremos crear un enlace y página especial para un proyecto (añadir enlace en el menú y página fija con el indice general), y añadir fotos a los posts(no sean solo texto), cada post debe tener una foto en el head y esa misma foto se usará en el listado de post. Para facilitar esto y no tener que estar haciendo fotos continuamnete, habrá al menos una foto por categoría, y definiremos las categorías básicas que vamos a tener, así por defecto se le pondrá la foto de la categoría.

### Modificaciones sobre la web
Creamos dos páginas fijas aparte de los posts
en la carpeta _pages
- about.md  incorporamos el Curriculum Vitae y alguna información más.
- [debateops.md](https://github.com/jarigita/jarigita.github.io/blob/main/_pages/debateops.md) explicación del proyecto e indice
<br>
También queremos tener un enlace externo para redirigir a la web personal pero en otro idioma, basta con añadir en la navegación e enlace externo.
<br>
para añadirlas en cada post se indica el enlace  **permalink: /DebateOps/** y se añaden al indice de navegación
en **_data/navigation.yml** hay que poner 

```html
main:
  - title: "About"
    url: /about/
  - title: "DebateOps"
    url: /DebateOps/
  - title: "english"
    url: https://jarigita.github.io/

```
Probamos en local vemos que salen los enlaces y nos redirige a la página estática.
<br>
Ahora queremos sacar el listado de posts junto con una foto.
<br>
Para ello hay que crear otra página con el listado de post
en _pages creamos otra página **blog_page.md**
```html
---
title:  "Blogs"
layout: archive
permalink: /Blogs/
author_profile: true
comments: true
---

  % for post in site.posts %
    <figure>
      <a href="{{post.url}}"><img src="/{{post.header.overlay_image}}" alt="{{post.title}}"></a>
    </figure>
    % include archive-single.html %
  % endfor %
```
En permalink indicamos el enlace que va a tener
<br>
Realizamos un bucle a traves de todos los posts de la web poniendo una figura(imagen) y el archivo sencillo básico de cada post (el mismo que crea por defecto)
<br>
Falta por enlazar la navegación
en **_data/navigation.yml** hay que poner 
```
main:
  - title: "Blogs"
    url: /Blogs/
```

Para que se muestre la imagen cada post debe tener en su cabecera un título (title) y una imagen de cabecera que vamos a alargar todo el ancho de la página.
<br>
Es decir, es obligatorio que cada post tenga de cabecera
```
---
title: Debateops. Por qué este blog.
header:
  overlay_image: assets/images/debateops.gif
  caption: "debateops"
categories:
  - debateops
tags:
  - debateops
  - agile
  - devops
---

```
- **title** es el titulo del post (se sobreecribira en la imagen)
- **header** con una imagen alargada y un caption (en cada post saldrá en la cabecera y en el listado de posts también)
- **categories** al menos indicarle una categoría la post, y si no tiene imagen poner la de la categoria
- **tags** especificar al menso un tag (la categoría) para faclitar la búsqueda del post

### Varios idiomas
La opción escogida para tener varios idiomas ha sido crear dos web estáticas totalmente similares.
<br>
Esto nos permite tener la web de cada idioma independiente, no es obligatorio subir a la vez los post en ambas ni que sean los mismos exactamente. Nos permite no mezclar busquedas en varios idiomas, personalmente si busco en español prefiero que me salgan las cosas en español a duplicarse la misma información en varios idiomas.
<br>
Al ser la url en español la misa que en inglés solo añadiendo /es eso nos permite compartir fotos y recursos, de manera que no se duplica contenido entre las dos webs sino solo los post o recursos específicos de ese idioma. 
<br>
Tampoco hace falta indicar traducciones y tener listados de multiples idiomas.

## Conclusión
Para ver el resultado de todo este posts es mi web personal [jarigita](https://jarigita.github.io/)
<br>
Me ha parecido muy útil y conveniente mostrar los mismos documentos que ya se creaban en markdown de una manera más amigable como web, es como tener una vista técnica (código) y una vista tutorial (web).
Como facilidad para subir post y mantenerla, al ser igual que el código, markdown y usando git y sus versiones, es muy fácil.
<br>
De aspecto gráfico, para mí es suficiente, no es un blog profesional, solo un conjunto de notas técnicas, por lo que prefiero sencillez e ir al grano, se ve bien y se maneja rápido.
<br>
Respecto a las subidas de cambios, el tiempo entre despliegues y que se vea efectivamente en la web varia de unas veces a otras, de manera que es mejor desplegar, ponerse a hacer otra cosa y luego comprobar, es un pero, como es gratis tampoco nos vamos a quejar.
<br>
Lo que si no he visto tan sencillo es modificar el aspecto, el funcionamiento básico va muy bien, pero si empiezas a cambiar aspecto o entrar en más bajo detalle, ya no es tan sencillo ni tan fácil. Si te equivocas, github pages manda un correo en el que solo indica la línea

```
The page build failed for the `main` branch with the following error:

You have an error on line 16 of your `_config.yml` file. For more information, see https://docs.github.com/github/working-with-github-pages/troubleshooting-jekyll-build-errors-for-github-pages-sites#config-file-error.

For information on troubleshooting Jekyll see:

  https://docs.github.com/articles/troubleshooting-jekyll-builds
```
Para mí que quiero algo rápido y sencillo, mejor adaptarse a lo básico, si quieres algo más llamativo quizás explorar otras alternativas.
<br>
Lo recomiendo y me parece miy útil github page con jekyll.

## Para más información

[Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/) como instalar jekyll en ubuntu

[jekyll-docs](http://jekyllrb.com/docs/home) documentos oficiales de jekyll
[jekyll-gh](https://github.com/jekyll/jekyll) proyecto github de jekyll
[jekyll-talk](https://talk.jekyllrb.com/) 

[minimal-mistakes jekyll theme](https://jekyllthemes.io/theme/minimal-mistakes)

[examples of posts ](https://github.com/mmistakes/minimal-mistakes/tree/gh-pages-3.1.6/_posts)

[Best Git Repositories: Google vs. Bitbucket vs. GitHub](https://www.upwork.com/resources/best-git-repository-google-github-bitbucket)

[From Jekyll to Hugo! From GitHub Pages to Netlify!](https://pawelgrzybek.com/from-jekyll-to-hugo-from-github-pages-to-netlify/)

[Jekyll vs. Hugo vs. Hexo](https://www.techiediaries.com/jekyll-hugo-hexo/)
