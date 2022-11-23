---
layout: post
title: Jekyll y Tailwindcss
date: 2022-11-22
categories: ["Developer", "Jekyll", "Tailwindcss"]
---

# Manos a la obra

Hay muchas personas incursionando en el desarrollo de paginas web, y actualmente hay muchas herramientas interesantes que te ayudan a construir sitios web fácil y rápido.

Hoy vamos a hablar de dos herramientas que en conjunto pueden hacer que logres un gran trabajo, con un poco de esfuerzo y dedicación.

# Que es [Jekyll](https://jekyllrb.com/)

[![image](https://img.shields.io/badge/Jekyll-CC0000?style=for-the-badge&logo=Jekyll&logoColor=white)](https://jekyllrb.com/)

Jekyll es un generador de paginas estáticas, que el termino estáticas no te haga pensar en simple o sin ningún movimiento., Jekyll esta enfocado en el desarrollo de Blogs, pero puede ser usado muy bien para la creación de sitios webs. Esta hecho con [Ruby](https://www.ruby-lang.org/es/), y fue desarrollado por Tom Preston-Werner, uno de los cofundadores de GitHub., creo que con esto ultimo ya no hay que dar mas referencias.

Jekyll es usado en la creación de las paginas que se muestran en Github Pages.

Jekyll no es un CMS o gestor de contenido, este no usa base de datos para servir el contenido del sitio web pero si dispone de un sistema de plantillas para el diseño de las paginas., el motor de plantillas esta basado en [Liquid](https://shopify.github.io/liquid/)

# Que es Tailwindcss

[![image](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

Escribir código CSS en realidad es algo tedioso, gracias a la aparición de varios framework, se nos facilito el trabajo a la hora de escribir CSS, he aquí donde cabe destacar al popular Framework CSS [Tailwindcss](https://tailwindcss.com/), aca si no voy a dar muchas explicaciones, tailwindcss es [CSS](https://es.wikipedia.org/wiki/CSS)

Bien antes de entrar en materia debo aclara que no soy un experto en el manejo de Jekyll, pero me decidí a crear este articulo debido a la poca información en mi idioma., y la información que se consigue generalmente una no coincide con la otra, aunque estoy consciente de que todos los caminos llevan a roma, debe existir un punto en común y basado en ese punto común escribo esta articulo para que les sirva como una guía inicial.

---

Lista de requerimientos:

- Ruby >= 2.7
- Bundle >= 2.3
- Jekyll >= 4.1.1
- Node.js >= 16.14.2

Asumiendo que ya tienes instaladas las dependencias, vamos comenzar con nuestro trabajo

Instalación en Ubuntu, abrimos una terminal nueva y escribimos

> **Prometo pronto actualizar este articulo con la instalación para windows**

```bash
gem install jekyll bundle
```

Ya tenemos instalado jekyll, ahora vamos a crear el proyecto, esta sera una instalación limpia de jekyll.

```bash
jekyll new PROYECTO --blank
```

ahora movamos nos a la carpeta del proyecto

```bash
cd PROYECTO
```

creemos el GemFile, que contiene la información de lo que necesita jekyll, escribiremos **_bundle init_**

```bash
~/PROYECTO$ bundle init
```

Lo anterior nos crear un archivo **GemFile**

> abrimos ese archivo **Gemfile** y pegamos lo siguiente:

```
gem "jekyll"
gem "webrick"
gem "jekyll-postcss"
```

ahora ejecutemos el comando **_bundle install_**

```bash
~/PROYECTO$ bundle install
```

posterior a la ejecución del comando anterior, ya se instalo lo necesario para comenzar a trabajar con jekyll, vamos a comprobarlo, ejecutando su servidor de desarrollo

```bash
~/PROYECTO$ bundle exec jekyll serve
```

ahora puedes abrir tu navegador, si no se abrió automáticamente con la ejecución del comando anterior y dirigirte a http://localhost:4000

detenemos el servidor usando la combinación de teclas **_Ctrl + C_** en la terminal

Necesitamos Postcss para realizar la integración de Tailwind, vamos a añadirlo a Tailwind., en la terminal vamos a escribir los siguiente

```bash
~/PROYECTO$ echo "gem 'jekyll-postcss'" >> Gemfile
```

una vez que ejecutemos la linea anterior ejecutaremos **_bundle_**

```shell
~/PROYECTO$ bundle
```

ahora abriremos el archivo **\_config.yml** que se encuentra en la raíz del proyecto y pegaremos los siguiente al final del archivo:

```
plugins:
  - jekyll-postcss

postcss:
  cache: false
```

Bien, es momento de integrar finalmente Tailwind, en la terminal vamos a introducir lo siguiente:

```shell
npm postcss@latest tailwindcss@latest autoprefixer@latest cssnano@latest -D
```

también podemos hacerlo con yarn

```shell
yarn add postcss@latest tailwindcss@latest autoprefixer@latest cssnano@latest -D
```

después de las instalación de los paquetes postcss tailwindcss autoprefixer y nano, introducimos el siguiente comando para crear unos archivos de configuración necesarios

```
npx tailwindcss init
```

esto nos creara dos archivos nuevos en la raíz del proyecto

- postcss.config.js
- tailwind.config.js
  abrimos el primero y pegamos lo siguiente

```
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
    ...(process.env.JEKYLL_ENV == 'production'
      ? [require('cssnano')({ preset: 'default' })]
      : [])
  ]
}
```

ahora abrimos **_tailwind.config.js_**

```
module.exports = {
  content: [
    './_drafts/**/*.html',
    './_includes/**/*.html',
    './_layouts/**/*.html',
    './_posts/*.md',
    './*.md',
    './*.html',
  ],
  theme: {
    theme: {
      extend: {},
    },
  },
  plugins: []
}
```

nos quedan unos pocos pasos., como mencione al principio vamos a usar **css**, localicemos en la raíz del proyecto la carpeta **_assets/css_** alli esta el archivo **_main.scss_**, este archivo vamos a renombrarlo a **_main.css_**, abrimos el archivo (main.css), suplantamos su contenido por lo siguiente:

```
---
---

@tailwind base;
@tailwind components;
@tailwind utilities;
```

incluyendo las dos lineas punteadas al principio.
Y para concluir vamos a verifica de nuevo el proyecto

```
bundle exec jekyll serve
```

Abrir el navegador, si no se abrió automáticamente con la ejecución del comando anterior y dirigirte a http://localhost:4000

Ya tienes Jekyll y Tailwindcss integrado, ahora puedes comenzar a desarrollar tu proyecto.

> **Esta guía fue elaborada a partir de la lectura de varios artículos encontrado en internet**
