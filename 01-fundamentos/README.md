# Fundamentos

Este curso está pensado para utilizar Sass en la práctica, por lo tanto comencemos con los básico de Sass:

## Instalaciones

Existen varias formas, una es con VSC:

- [https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass)
- [https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)

Con `npm` Dart Sass (últimas mejoras):

- [https://nodejs.org/es/](https://nodejs.org/es/)
- [https://sass-lang.com/install](https://sass-lang.com/install)

```
npm install -g sass
```

## Compilar

```
sass --watch input.scss output.css
```

```
sass --watch scss/estilos.scss css/estilos.css
```

## En nuestro proyecto

\*[https://necolas.github.io/normalize.css/](https://necolas.github.io/normalize.css/)

Crear los siguientes directorios:

```
css
    normalize.css
scss
    _variables.scss
    estilos.scss
index.html
```

## Box-sizing

[https://css-tricks.com/box-sizing/#universal-box-sizing-with-inheritance](https://css-tricks.com/box-sizing/#universal-box-sizing-with-inheritance)

```scss
@import "variables";

html {
  box-sizing: border-box;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}

h1 {
  color: $primary;
}
```

```scss
// _variables
$primary: #00b8a9;
$secondary: #ff8c08;
$light: #eaeaea;
$danger: #f6416c;
$dark: #252a34;
```

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Sass Hola!</title>

    <link rel="stylesheet" href="css/normalize.css" />
    <link rel="stylesheet" href="css/estilos.css" />
  </head>
  <body>
    <div class="container mx-auto mt-2">
      <a href="#" class="btn-primary">primary</a>
      <a href="#" class="btn-secondary">secondary</a>
      <a href="#" class="btn-light">light</a>
      <a href="#" class="btn-danger">danger</a>
      <a href="#" class="btn-dark">dark</a>
    </div>
  </body>
</html>
```

## Botones

Comencemos a construir nuestros primeros componentes:

- [https://thoughtbot.com/blog/controlling-color-with-sass-color-functions](https://thoughtbot.com/blog/controlling-color-with-sass-color-functions)
- [https://sass-lang.com/documentation/style-rules/parent-selector](https://sass-lang.com/documentation/style-rules/parent-selector)

:::tip
Los mixins le permiten definir estilos que se pueden reutilizar en toda su hoja de estilo
[https://sass-lang.com/documentation/at-rules/mixin](https://sass-lang.com/documentation/at-rules/mixin)
:::

```scss
// _botones.scss
@mixin btn-boton($color) {
  display: inline-block;
  border-radius: 10px;
  padding: 10px 20px;
  color: if($color == $light, #000, #fff);
  text-decoration: none;
  background-color: $color;
  &:hover {
    background-color: darken($color, 20%);
  }
}

// Alternativa #1
.btn {
  &-primary {
    @include btn-boton($primary);
  }
  &-secondary {
    @include btn-boton($secondary);
  }
  &-light {
    @include btn-boton($light);
  }
  &-danger {
    @include btn-boton($danger);
  }
  &-dark {
    @include btn-boton($dark);
  }
}

// Alternativa #2
.btn-primary {
  @include btn-boton($primary);
}
.btn-secondary {
  @include btn-boton($secondary);
}
.btn-light {
  @include btn-boton($light);
}
.btn-danger {
  @include btn-boton($danger);
}
.btn-dark {
  @include btn-boton($dark);
}
```

## Espaciados @each

[https://sass-lang.com/documentation/at-rules/control/each](https://sass-lang.com/documentation/at-rules/control/each)

```scss
// estilos.scss
$valor-espaciado: (1, 2, 3, 4, 5);

@each $item in $valor-espaciado {
  .m-#{$item} {
    margin: #{$item / 2}rem;
  }
  .mx-#{$item} {
    margin-left: #{$item / 2}rem;
    margin-right: #{$item / 2}rem;
  }
  .my-#{$item} {
    margin-top: #{$item / 2}rem;
    margin-bottom: #{$item / 2}rem;
  }
  .p-#{$item} {
    padding: #{$item / 2}rem;
  }
  .px-#{$item} {
    padding-left: #{$item / 2}rem;
    padding-right: #{$item / 2}rem;
  }
  .py-#{$item} {
    padding-top: #{$item / 2}rem;
    padding-bottom: #{$item / 2}rem;
  }
}
.mx-auto {
  margin-right: auto;
  margin-left: auto;
}
```
