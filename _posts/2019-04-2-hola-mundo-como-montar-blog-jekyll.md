---
layout: post
title:  "¡Hola Mundo! (o cómo monté este blog en Jekyll)"
image: /assets/images/blog/2019-04-2-Hola-mundo-como-montar-blog-Jekyll.jpg
categories: Jekyll
tags: [Jekyll, SSG, Github Pages, blog, Sass, CoffeeScript, Liquid]
---

Primero de todo aclarar que esto no es un presentacion, para eso ya está la sección Sobre Mí en la página principal, así como tampoco pretende ser un tutorial acerca de como montar un sitio con [Jekyll](https://jekyllrb.com/ "Página de inicio de Jekyll"). Más bien se trata de un post narrando un poco el proceso y que puede servir para inspirar a personas que quieran animarse a hacer algo parecido o incluso utilizar mi código como base.

### ¿Qué demonios es Jekyll?

Así a *grosso modo*, es un generador de sitios web estáticos o SSG por ahorrar un poco de espacio, de código abierto y escrito en Ruby; de hecho su slogan es: *Transforma tu texto sin formato en sitios web y blogs estáticos*, es decir, puedes añadir contenido a tu web con la única ayuda de un editor de texto.

Generadores de sitios web estáticos hay muchos: Hugo, Hexo, Gastby, Next... son [algunos](https://www.staticgen.com/ "Algunos generadores de sitios web estáticos") de los más conocidos.

Estos generadores nos aportan muchísimas ventajas y en la mayoría de los casos ninguna limitación. A diferencia de los sistema de gestión de contenidos o CMS, podemos generar un sitio web completo solamente con HTML, CSS y puede que JavaScript, por lo que podremos alojarlo en prácticamente en cualquier sitio (incluso en una Raspberry Pi) y apenas consumiendo recursos. Teniendo en cuenta que la mayoría de los sitios de Internet necesitan poco más, a parte lo ya mencionado, Jekyll o cualquier otro SSG son una opción muy potente a tener en cuenta.

Jekyll trabaja con ficheros escritos en [markdown](https://daringfireball.net/projects/markdown/ "Markdown web")  (**.md**) y los convierte automáticamente a HTML. Por ejemplo, para escribir esta entrada estoy escribiendo en markdown utilizando ¡nada más que Notepad++!

#### ¿Por qué Jekyll?

Inicialmente tenía pensado utilizar [Grav](https://getgrav.org/ "Página de inicio de Grav") para construir este sitio. Ya había trabajado con Wordpress y PHP en [GeekMag](https://www.geekmag.es "GeekMag") pero necesitaba algo más liviano y que no dependiera de una pesada base de datos. Aunque probé también [Ghost](https://ghost.org/es/ "Página de inicio de Ghost"), éste, adolecía de muchas de las características de Wordpress que pretendía evitar (como la base de datos).

Grav prometía ofrecerme todo lo necesario para gestionar y añadir contenido al sitio. Incluso es posible instalar un plugin que permite administrarlo desde un panel estilo Wordpress. Sin embargo, utilizar todo un CMS para simplemente un sitio web personal y un blog me parecía y me sigue pareciendo más de lo que necesito.

Fue entonces cuando decidí utilizar Jekyll. Lo mejor, [soporte integrado para Sass y compatibilidad con CoffeeScript](https://jekyllrb.com/docs/assets/ "Assets en Jekyll").

#### GitHub Pages

La principal razón es que está totalmente integrado con [GitHub Pages](https://pages.github.com/ "GitHub Pages") (también con [GitLab Pages](https://about.gitlab.com/product/pages/ "Información GitLab Pages")) por si a alguien le interesa), un servicio gratuito de hosting que proporciona GitHub a sus usuarios. Pero es que además es de código abierto, simple, a penas requiere mantenimiento y, aunque en este caso no me interesaba, proporciona todo lo necesario para migrar tu web ya existente desde casi cualquier CMS a Jekyll. Pero sobretodo porque lo puedo alojar en GitHub Pages, que es rápido, seguro y 100% gratis.

### Diseño

Ya tenía un diseño simple pero funcional en la web (gracias a [Benjamin Sago](https://bsago.me/ "Web de Benjamin Sago")) desde el que trabajar. Sin embargo quería algo más vistoso sobre lo que trabajar. Fue así como encontré el diseño actual.

Dicho diseño ha sido concebido originalmente por [Styleshout](https://www.styleshout.com/free-templates/hola/ "Página de la plantilla de la web") pero ha sido portado a Jekyll por mí.

Cualquiera es libre de utilizar mi código para su web, la de un amigo, para un cliente o lo que quiera. Pero debéis saber que no permito redistribuir mi código y que los créditos a pie de página deben permanecer. Además se deben tener en cuenta las políticas de [Styleshout](https://www.styleshout.com/about-us/#remove-link "Licencia diseño") para sus diseños.

Dicho esto empezar a usarlo es tan simple como acceder a [éste repositorio](https://github.com/MrAnnix/MrAnnix.github.io "Repo de la web") y descargarlo.

### Cómo empezar

Una vez que ya tenía una plantilla con un diseño de mi agrado, lo primero fue crear un fichero `_config.yml` en la raíz de la web, que almacenase la opciones de configuración del sitio y cómo Jekyll debía generarlo.

Ese es el fichero que debéis editar si queréis utilizar esta o cualquier otra plantilla (incluso la plantilla por defecto de Jekyll).

#### Liquid

Una vez que ya estaba configurado lo básico, lo siguiente era hacer que se hiciera la magia. Para ello Jekyll utiliza [Liquid](https://shopify.github.io/liquid/ "Liquid"), un lenguaje para procesar plantillas escrito en Ruby, al igual que Jekyll, y con un gran potencial.

    {% for post in site.posts limit:4 %}
    <article class="col-block">
        <div class="blog-date">
            <a>{{ post.date | date: '%B %d, %Y' }}</a>
        </div>    
        <h2 class="h01"><a href="{{ post.url }}">{{ post.title }}</a></h2>
        <p>{{ post.excerpt | strip_html | truncate: 360 }}</p>   
        <div class="blog-cat">
            {% for category in post.categories %}
            <a href="{{ site.baseurl }}{{ site.category_page }}#{{ category | slugify }}">
			    {{ category }}
		    </a>
            {% endfor %}
        </div>    
    </article>
    {% endfor %}

El fragmento de arriba pertenece a la porción de código que genera la previsualización de los posts para la página principal de la web. Como podréis apreciar, la parte de Liquid es muy intuitiva y fácil de programar.

#### Plugins
Seguramente, querréis que vuestro blog haga más cosas, por ejemplo: generar páginas de etiquetas y categorías, un mapa del sitio, un feed...

Para ello Jekyll dispone de una miríada de plugins. Sin embargo, si queréis utilizar Github Pages, no os recomiendo intentar utilizar más de los justos y necesarios, ya que sólo unos pocos son compatibles. En el caso de esta plantilla solo se utilizan `jekyll-sitemap` y `jekyll-paginate` para generar el mapa del sitio y distribuir las entradas del blog en varias páginas respectivamente.

Para el resto de las funcionalidades he utilizado Liquid exclusivamente, en concreto para las páginas de categorías y etiquetas he seguido [este tutorial](http://codinfox.github.io/dev/2015/03/06/use-tags-and-categories-in-your-jekyll-based-github-pages/ "Use Tags and Categories in your Jekyll based Github Pages without plugins - Codinfox").

#### Comentarios

Lo más probable es que los propietarios de un blog deseen añadir la función de comentarios en las entradas del mismo. Para ello es necesaria la ejecución de código por parte del servidor. Pero Jekyll solo genera sitios estáticos... ¿Qué hacemos? Tranquilos, existen infinidad de soluciones para ello. Desde Facebook Comments, Disqus o incluso opciones autogestionadas.

Yo personalmente me decanté por [Commentbox](https://commentbox.io "No ads.  No Tracking.  Just Comments."), pero existen opciones geniales a tener en cuenta. Por ejemplo: [Commento](https://gitlab.com/commento/commento "A fast, bloat-free, privacy-focused commenting platform") (mi segundo candidato en la lista), [Remark42](https://remark42.com/ "self-hosted, lightweight, and simple commenting system"), [Just Comments](https://just-comments.com/ "Easy to set up, ad-free and fairly priced comment system") (no es gratis pero es bastante barato)...

___________________________________________________


Espero haber animado a más de uno a crear su propio blog con Jekyll o a migrar el que ya tiene. Si de verdad queréis empezar, podéis hacerlo [aquí](https://jekyllrb.com/docs/step-by-step/01-setup/ "Guía paso a paso de Jekyll"). Jekyll tiene documentación a raudales y cuando esta no es suficiente, en Internet hay muchísimos tutoriales que explican como realizar la mayoría de las cosas que queráis hacer.
