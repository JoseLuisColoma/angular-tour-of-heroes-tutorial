# Angular: Tour of Heroes Tutorial en Español

<p align="center">
<img src="https://gist.github.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/38afb12bb070db660a635f7b34ae2ea3e332e87b/img-angular-logo.png" width="200" height="200">
</p>

Angular es un framework JavaScript, gratuito y Open Source, creado por Google y destinado a facilitar la creación de aplicaciones web modernas de tipo SPA (Single Page Application).

Su primera versión, AngularJS, se convirtió en muy poco tiempo en el estándar de facto para el desarrollo de aplicaciones web avanzadas.

En septiembre de 2016 Google lanzó la versión definitiva de lo que llamó en su momento Angular 2, y que ahora es simplemente Angular. Este nuevo framework se ha construido sobre años de trabajo y feedback de los usuarios usando AngularJS (la versión 1.x del framework). Su desarrollo llevó más de 2 años. No se trata de una nueva versión o una evolución de AngularJS, sino que es un nuevo producto, con sus propios conceptos y técnicas. Además, Angular utiliza como lenguaje de programación principal TypeScript, un súper-conjunto de JavaScript/ECMAScript que facilita mucho el desarrollo.

**FUENTE:** https://www.campusmvp.es/recursos/post/las-5-principales-ventajas-de-usar-angular-para-crear-aplicaciones-web.aspx

## :arrow_right: Vamos a por el tutorial
Este es el tutorial oficial de la página de Angular. Lo que haré es ir haciendo el tutorial y después intentar hacer un manual de cómo funciona Angular.

En este tutorial se creará una aplicación que ayuda a una agencia personal a administrar superhéroes.

Esta aplicación básica tiene muchas de las características que esperarás encontrar en una aplicación basada en datos. Adquiere y muestra una lista de héroes, edita los detalles de un héroe seleccionado y navega entre diferentes vistas de datos heróicos.

Al final del tutorial, aprenderemos:
- Utilizar las directivas de Angular para ver y ocultar elementos y mostrar listas de los datos de los héroes.
- Crear componentes de Angular para mostrar los detalles de los héroes y mostrar un array de héroes.
- Usar datos de una sola dirección para leer sólo datos.
- Añadir campos editables a los eventos del usuario, como pulsaciones de teclas o clicks.
- Habilitar usuarios para seleccionar un héroe de una lista maestra y editar ese héroe en la vista de detalles.
- Formatear datos con "tuberías".
- Crear un servicio compartido para armar a los héroes.
- Usar el enrutamiento para navegar entre diferentes vistas y sus componentes.

Con esto aprendereremos lo suficiente de Angular para comenzar y tener la confianza de que Angular puede hacer lo que necesitemos.

## :arrow_right: Lo que construiremos
Aquí hay una idea visual de dónde conduce este tutorial, comenzando con la vista "Tablero" (Dashboard) y un listado random de héroes.

<p align="center">
<img src="https://gist.github.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/fd6e875aded00304f4ee58823635bf5e8a767c14/images-heroes-dashboard-1.png">
</p>

Puedes hacer click en los dos enlaces sobre el Dashboard ("Tablero" y "Héroes") para navegar entre esta vista del Tablero y una vista de Héroes.

Si haces click en el héroe del tablero "Magneta", el enrutador abre una vista de "Detalles del héroe" donde puede cambiar el nombre del héroe.

<p align="center">
<img src="https://gist.github.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/fd6e875aded00304f4ee58823635bf5e8a767c14/image-hero-details-1.png">
</p>

Al hacer click en el botón "Atrás", volverá al panel. Los enlaces en la parte superior te llevan a cualquiera de las vistas principales. Si haces click en "Héroes" la aplicación muestra "Héroes" de la vista principal.

<p align="center">
<img src="https://gist.github.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/fd6e875aded00304f4ee58823635bf5e8a767c14/image-heroes-list-2.png">
</p>

Cuando haces click en un nombre de héroe diferente, el mini detalle de sólo lectura debajo de la lista refleja la nueva opción.

Puedes hacer click en el botón "Ver detalles" para explorar los detalles editables del héroe seleccionado.

El siguiente diagrama captura todas las opciones de navegación.

<p align="center">
<img src="https://gist.github.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/7886455ef2799c167dd8a18f29d8da4dcf7f0e72/img-nav-diagram.png">
</p>

Y esta es la aplicación en acción: 

<p align="center">
<img src="https://gist.github.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/7886455ef2799c167dd8a18f29d8da4dcf7f0e72/img-toh-anim.gif">
</p>

## :arrow_right: La Aplicación Shell

### Instalar Angular CLI
Instalar el CLI de Angular es muy fácil, se hace de la siguiente manera:

```shell
npm install -g @angular/cli
```

### Crear una nueva aplicación
Vamos a crear un nuevo proyecto llamado `angular-tour-of-heroes` con este comando CLI.

```shell
ng new angular-tour-of-heroes
```

El CLI de Angular ha generado un nuevo proyecto con una aplicación predeterminada y archivos de respaldo.

> Puedes agragar funcionalidades preempaquetadas a un nuevo proyecto utilizando el comando `ng add`. El comando `ng add` transforma un proyecto aplicando los esquemas en el paquete especificado. Para obtener más información, consulta la [documentación del CLI de Angular](https://github.com/angular/angular-cli/wiki/add).
> 
> Angular Material proporciona esquemas para diseños de aplicaciones típicos. Consulta la [documentación de Material Angular](https://material.angular.io/guides) para más detalles.

### Serve la aplicación (arrancar la aplicación)
Nos metemos dentro del directorio de nuestra aplicación y lanzamos el siguiente comando:

```shell
cd angular-tour-of-heroes
ng serve --open
```

> `ng serve` este comando crea la aplicación, inicia el servidor de desarrollo, mira los archivos fuente y reconstruye la aplicación a medida que se realizan cambios en estos archivos.
>
> La bandera `--open` abre un navegador con `http://localhost:4200`.

### Componentes de Angular
La pagina que puedes ver es la *application shell*. La shell está controlada por un coponente de Angular llamado `AppComponent`.

Los *Componentes* son los bloques fundamentales con las que se construyen nuestras aplicaciones con Angular. Muestran datos en la pantalla, escuchan los *input* (entradas) de los usuarios y toman medidas en función a ese *input*.

### Cambiar el título de la aplicación
Abrimos el proyecto con nuestro editor favorito o IDE y navegamos al directorio `src/app`.

Encontraremos la implementación del shell `AppComponent` distribuido en tres archivos:

1. `app.component.ts` - el código de clase del componente, escrito en TypeScript.
2. `app.component.html` - la plantilla del componente, escrito en HTML.
3. `app.component.css` -  los estilos de CSS privados del componente.

Abrimos el archivo de clase de componente (`app.component.ts`) y cambiamos el valor de `title` por la propiedad `Tour of Heroes`.

**Archivo: `app.component.ts`** (propiedad del título de la clase)
```typescript
title = 'Tour of Heroes';
```

Debería quedar de la siguiente manera:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'Tour of Heroes';
}
```

Abrimos el archivo de plantilla del componente (`app.component.html`) y borramos la plantilla generada por defecto por el CLI de Angular. Reemplaza esto con la siguiente línea de HTML.

**Archivo: `app.component.html`** (template - plantilla)
```html
<h1>{{title}}</h1>
```

Las llaves dobles son la sintaxis de unión de interpolación de Angular. Este enlace de interpolación presenta el valor de propiedad del título del componente dentro de la etiqueta del encabezado HTML.

El navegador se actualiza y muestra el nuevo título de la aplicación.

### Agregar estilos a la aplicación
La mayoría de las aplicaciones se esfuerzan por obtener un aspecto uniforme en toda la aplicación. El CLI generó un `styles.css` vacío para este propósito. Coloque allí sus estilos para toda la aplicación.

A continuación tendremos un extracto del `styles.css` para la aplicacion de muestra `Tour of Heroes`.

**Archivo: `src/styles.css`** (extracto)
```css
/* Application-wide Styles */
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}
h2, h3 {
  color: #444;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: lighter;
}
body {
  margin: 2em;
}
body, input[text], button {
  color: #888;
  font-family: Cambria, Georgia;
}
/* everywhere else */
* {
  font-family: Arial, Helvetica, sans-serif;
}
```

### Resumen
- Hemos creado una estructura para una aplicación inicial usando el CLI de Angular.
- Hemos aprendido que los componentes de Angular muestran datos.
- Hemos usado las llaves dobles `{{ }}` de interpolación para mostrar el título de la aplicación.

## :arrow_right: El editor de héroes
La aplicación ahora tiene un título básico. A continuación, crearemos un nuevo componente para mostrar la información del héroe y colocar ese componente en el shell de la aplicación.

### Crear el componente de héroes
Con el CLI de Angular, generamos un nuevo componente llamado `heroes`.

```shell
ng generate component heroes
```

El CLI crea una nueva carpeta, `src/app/heroes/`, y genera tres archivos en el `HeroesComponent`.

El archivo clase de `HeroesComponent` es el siguiente:

**Archivo: `app/heroes/heroes.component.ts`** (versión inicial)
```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

}
```

Siempre se importa el symbol de `Component` de la biblioteca central de Angular y anota la clase componente con `@Component`.

`@Component` es una función decorador que especifíca los metadatos de Angular al componente.

El Cli genera tres propiedades metadata:

1. `selector` - el selector de elemento CSS del componente.
2. `templateUrl` - la ubicación del archivo de plantilla del componente.
3. `styleUrls` - la ubicación de los estilos de CSS privados del componente. 

El [elemento selector CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors), `app-heroes`, coincide con el nombre del elemento HTML que identifica este componente dentro de la plantilla de un componente principal.

`NgOnInit`es un hook (gancho) de ciclo de vida. Angular llama a `ngOnInit`poco después de crear un componente. Es un buen lugar para poner la lógica de inicialización.

Siempre debemos exportar (`export`) la clase del componente para que pueda importarla (`import`) en otro lugar... como en el `AppModule`. 

### Añadir propiedad al héroe
Agregar al `hero` una propiedad al `HeroesComponent` para un héroe llamado "Windstorm".

**Archivo: `heroes.component.ts`** (propiedad del heroe)
```typescript
hero = 'Windstorm';
```

### Mostrar el héroe
Abre el archivo de plantilla `heroes.component.html`. Borra el texto por defecto generado por el CLI de Angular y reemplazalo con lo que viene a continuación.

**Archivo: `heroes.component.html`**
```html
{{hero}}
```

### Mostrar la vista *HeroesComponent* 
Para mostrar el `HeroesComponent`, debemos de agregarlo a la plantilla del shell `AppComponent`.

Recuerda que `app-heroes` es el selector de elementos para `HeroesComponent`. Así que agrega un elemento `<app-heroes>` al archivo de plantilla de `AppComponent`, justo debajo del título.

**Archivo: `src/app/app.component.html`**
```typescript
<h1>{{title}}</h1>
<app-heroes></app-heroes>
```

Suponiendo que el comando CLI `ng serve` aún se está ejecutando, el navegador debe actualizar y mostrar tanto el título de la aplicación como el nombre del héroe.

### Creando la clase Hero
Un héroe real es más que un simple nombre.

Crea una clase `Hero` creando tu propio archivo `hero.ts` en la carpeta `src/app`. Dale las propiedades `id` y `name`.

**Archivo: `src/app/hero.ts`**
```typescript
export class Hero {
  id: number;
  name: string;
}
```

Vuelve a la clase `HeroesComponent` e importa la clase `Hero`.

Refactoriza la propiedad del componente `hero` para que sea del tipo `Hero`. Inizializarlo con una `id`de `1` y el nombre `Windstorm`.

El archivo de clase `HeroesComponent` revisado debera de verse así:

**Archivo: `src/app/heroes/heroes.component.ts`**
```typescript
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {
  hero: Hero = {
    id: 1,
    name: 'Windstorm'
  };

  constructor() { }

  ngOnInit() {
  }

}
```

La página ya no se muestra correctamente porque ha cambiado el héroe de una cadena (`string`) a un objeto (`object`).

### Mostrar el objeto del héroe
Actualiza el enlace en la plantilla para anunciar el nombre del héroe y mostrar tanto la `id` como el `name` en un diseño como este:

**Archivo: `heroes.component.html`** (modelo HeroesComponent)
```html
<h2>{{hero.name}} Details</h2>
<div><span>id: </span>{{hero.id}}</div>
<div><span>name: </span>{{hero.name}}</div>
```

El navegador se refrescará y mostrara la información del héroe.

### Formato con *UppercasePipe*
Modifica el enlace `hero.name` como vemos aquí:

```html
<h2>{{hero.name | uppercase}} Details</h2>
```

El navegador se refrescará y ahora el nombre del héroe se verá en mayúsculas.

La palabra `uppercase` en el enlace de interpolación, justo después del operador de tubería (`pipe operator`) (|), activa el `UperCasePipe` incorporado.

Las 'tuberías' son una buena forma de formatear cadenas, cantidades de moneda, fechas y otros datos de visualización. Angular dispone de distintos [tuberías integradas](https://angular.io/guide/pipes) y puedes crear las tuyas propias.

### Editar un héroe
Los usuarios deberían poder editar el nombre del héroe en un cuadro dre texto `<input>`.

El cuadro de texto debe *mostrar* la propiedad de `name` del héroe y *actualizar* esa propiedad a medida que el usuario lo escribe. Eso significa que el flujo de datos de la clase de componente *salida* a la *pantalla* y de la *pantalla* se lo *devuelva* a la clase.

Para automizar ese flujo de datos, configura un enlace de datos bidireccional entre el elemento de formulario `<input>` y la propiedad del elemento `hero.name`.

### Enlace bidireccional
Refactoriza el área de detalles en la plantilla `HeroesComponent` para que se vea así:

**Archivo: `src/app/heroes/heroes.component.html`** (plantilla HeroesComponent)
```html
<div>
  <label>name:
    <input [(ngModel)]="hero.name" placeholder="name">
  </label>
</div>
```

`[(ngModel)]` es la sintaxis de enlace de datos bidireccional de Angular.

Aquí se vincula la propiedad `hero.name` al cuadro de texto HTML para que los datos puedan fluir en ambas direcciones: de la propiedad `hero.name` al cuadro de texto y del cuadro de texto a `hero.name`.

### Nos falta FormsModule
Nos daremos cuenta que la aplicación dejó de funcionar cuando agregamos `[(ngModel)]`.

Para ver estos errores, abrimos las herramientas de desarrollo del navegador y buscamos en la consola un mensaje como:

```shell
Template parse errors:
Can't bind to 'ngModel' since it isn't a known property of 'input'.
```

Aunque `ngModel` es una directiva de Angular válida, no está disponible por defecto.

Pertenece a `FormsModule`y es opcional, podemos optarlo si lo usamos.

### AppModule
Angular necesita saber cómo encajan las piezas de su aplicación y qué otros archivos y bibliotecas necesita la aplicación. Esta información se llama *metadata*.

Algunos de los metadatos están en los decoradores de `@Component` que ha agregado a sus clases de componentes. Otros metadatos críticos se encuentan en los decoradores de [@NgModule](https://angular.io/guide/ngmodules).

El decorador `@NgModule` más importante anota la clase `AppModule` de nivel superior.

El CLI de Angular genera una clase de `AppModule` en `src/app/app.module.ts` cuando crea el proyecto. Aquí es donde se puede optar por el `FormsModule`.

### Importando FormsModule
Abre `AppModule` (`app.module.ts`) e importa el symbol `FormsModule` de la libreria `@angular/forms`.

**Archivo: `app.module.ts`** (Importar symbol FormsModule)
```typescript
import { FormsModule } from '@angular/forms'; // <-- NgModel lives here
```

A continuación agrega `FormsModule` a la matriz de importaciones de los metadatos de `@NgModule`, que contiene una lista de módulos externos que la aplicación necesita.

**Archivo: `app.module.js`** (importa @NgModule)
```typescript
imports: [
  BrowserModule,
  FormsModule
],
```

Cuando el navegador se actualiza, la aplicación debería de funcionar nuvamente. Puedes editar el nombre del héroe y ver los cambios reflejados inmediatamente en el `<h2>` encima del cuadro de texto.

### Declarar *HeroesComponent*
Todo componente debe ser declarado exactamente en [NgModule](https://angular.io/guide/ngmodules).

¿No declaraste antes el componente `HeroesComponent`?. Entonces, ¿por qué funcionó la aplicación?.

Funcionó porque el CLI de Angular declaró `HeroesComponent`en el `AppModule` cuando generó ese componente.

Abre `src/app/app.module.ts` y encuentra `HeroesComponent` que está importado por arriba del todo.

```typescript
import { HeroesComponent } from './heroes/heroes.component';
```

`HeroesComponent` está declarado en el array `@NgModule.declarations`.

```typescript
declarations: [
  AppComponent,
  HeroesComponent
],
```

Ten en cuenta que `AppModule` declara ambos componentes en la aplicación `AppComponent` y `HeroesComponent`.

### Resumen
- Usamos el CLI para crear un segundo `HeroesComponent`. 
- Mostramos `HeroesComponent` agregándolo al shell de `AppComponent`. 
- Aplicamos `UppercasePipe` para formatear el nombre. Usó el enlace de datos bidireccional con la directiva `ngModel`. 
- Hemos aprendido sobre `AppModule`. 
- Hemos aprendido sobre `FormsModule` en el `AppModule` para que Angular reconozca y aplique la directiva `ngModel`. 
- Aprendimos la importancia de declarar componentes en el `AppModule` y agradecimos que el CLI lo declarara por nosotros.


## :arrow_right: Mostrar lista de héroes
En esta pgina, expandiremos la aplicación 'Tour of Heroes' para mostrar una lista de héroes y permitir a los usuarios seleccionar un héroe y mostrar los detalles de éste.

### Creando héroes simulados
Necesitaremos unos cuantos héroes para mostrarlos.

Normalmente los obtendremos de un servidor, pero por ahora, crearemos algunos héroes falsos y nos creeremos que vienen del servidor.

Crea un archivo llamado `mock-heroes.ts` en la ubicación `src/app/`. Define `HEROES` como una constante y un array de diez hroes y expórtala. El archivo debe verse así:

**Archivo: `src/app/mock-heroes.ts`**
```typescript
import { Hero } from './hero';

export const HEROES: Hero[] = [
  { id: 11, name: 'Mr. Nice' },
  { id: 12, name: 'Narco' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];
```

### Mostrando los héroes
Estás a punto de mostrar la lista de héroes en la parte superior de `HeroesComponent`.

Abre el archvio de clase `HeroesComponent` e importa la lista simulada de 'HEROES'.

**Archivo: `src/app/heroes/heroes.component.ts`** (importando HEROES)
```typescript
import { HEROES } from '../mock-heroes';
```

Agrega una propiedad de `heroes` a la clase que expone a estos héroes para vincularlos.

```typescript
heroes = HEROES;
```

### Listar los héroes con */*ngFor*
Abre el archivo de la plantilla `HeroesComponent` y realiza los siguientes cambios:

- Agrega un `<h2>` en la parte superior.
- A continuación, agrega una lista desordenada HTML (`<ul>`).
- Inserta un `<li>` dentro de `<ul>` que muestra las propiedades de un `hero`.
- Espolvoreamos algunas clases de CSS para el estilo (agregaremos los estilos CSS en breve).

Haz que se vea así:

**Archivo: `heroes.component.html`** (plantilla heroes)
```html
<h2>My Heroes</h2>
<ul class="heroes">
  <li>
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>
```

Ahora cambia el `<li>` así:

```html
<li *ngFor="let hero of heroes">
```

El [`*ngFor`](https://angular.io/guide/template-syntax#ngFor) es la directiva de repetidor de Angular. Repite el elemento host para cada elemento en una lista.

En este ejemplo:

- `<li>` es el elemento host.
- `heroes` es la listsa de la clase `HeroesComponent`.
- `hero` tiene el objeto héroe actual para cada iteración a través de la lista.

> No olvides el asterísco (*) delante de `ngFor`. Es una parte crítica de la sintaxis.

Después de que el navegador se actualiza, aparece la lista de héroes.

### Estilo de los héroes
La lista de héroes debe de ser atractiva y debe responder visualmente cuando los usuarios se pongan encima de la lista y seleccionen uno.

En la primera parte del tutorial, establecimos los estilos básicos para toda la aplicación en `styles.css`. Esa hoja de estilo no incluía estilos para esta lista de héroes.

Puedes añadir más estilos a `styles.css` y seguir creciendo esa hoja de estilos a medida que agregas componentes.

En su lugar, puedes preferir definir estilos privados para un componente en específico y mantener todo lo que necesita un componente - el código, el HTML y el CSS - en un sólo lugar.

Este enfoque hace que sea más fácil reutilizar el componente en otro lugar y entregar la apariencia prevista del componente, incluso si los estilos globales son diferentes.

Definimos los estilos privados ya sea en un array en `@Component.styles` o como un archivo(s) de hoja de estilos identificados en el array `@Component.styleUrls`.

Cuando el CLI generó `HeroesComponent`, creó una hoja de estilo `heroes.component.css` vaca para `HeroesComponent` y la apuntó en `@Component.styleUrls` de esta manera.

**Archivo: `src/app/heroes/heroes.component.ts`** (@Component)
```typescript
@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
```

Abre el archivo `heroes.component.css` y pega los estilos CSS privados para `HeroesComponent` que se muestran a continuación:

> Los estilos y las hojas de estilo identificadas en el metadata de `@Component` tiene un alcance para ese componente en específico. Los estilos de `heroes.component.css` se aplican sólo a `HeroesComponent` y no afecta al HTML externo o al HTML en ningún otro componente.

**Archivo: `src/app/heroes/heroes.component.css`**
```css
/* HeroesComponent's private CSS styles */
.selected {
  background-color: #CFD8DC !important;
  color: white;
}
.heroes {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes li.selected:hover {
  background-color: #BBD8DC !important;
  color: white;
}
.heroes li:hover {
  color: #607D8B;
  background-color: #DDD;
  left: .1em;
}
.heroes .text {
  position: relative;
  top: -3px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```

### Lista Maestra/Detalles
Cuando el usuario hace click en un héroe en la lista maestra, el componente debe mostrar los detalles del héroe seleccionado en la parte inferior de la página.

En esta sección, escuchará el evento de click del hemelento héroe y actualiza el detalle del héroe.

### Agregar un enlace al evento click
Vamos a agregar un evento click al enlace `<li>`, debe de quedar así:

**Archivo: `heroes.component.html`** (extracto de la plantilla)
```html
<li *ngFor="let hero of heroes" (click)="onSelect(hero)">
```

Este es un ejemplo de la sintáxis de Angular del [event binding](https://angular.io/guide/template-syntax#event-binding).

Los paréntesis de alrededor de `click` dicen a Angular que escuche el evento `click` del elemento`<li>`. Cuando el usuario hace click en el elemento `<li>`, Angular ejecuta la expresión `onSelect(hero)`.

`onSelect()` es un método de `HeroesComponent` que estamos a punto de escribir. Angular lo llama con el objeto `heroe` que se muestra en el `<li>` clickado, el mismo `hero` definido previamente en la expresión `*ngFor`.

### Agregar el controlador de eventos click
Renombramos la propiedad del componente `hero` a `selectedHero` pero no se lo asignamos. No hay un héroe seleccionado cuando se inicia la aplicación.

Agregamos el siguiente método `onSelect()`, que asigna al héroe clickado de la plantilla del componente `selectedHero`.

**Archivo: `src/app/heroes/heroes.component.ts`** (onSelect)
```typescript
selectedHero: Hero;

onSelect(hero: Hero): void {
  this.selectedHero = hero;
}
```

### Actualizar la plantilla de detalles
La plantilla todavía se refiere a la antigua propiedad del `hero` del componente que ya no existe. Cambiar el nombre de `hero` a `selectedHero`.

**Archivo: `heroes.component.html`** (Detalles seleccionados del héroe)
```html
<h2>{{selectedHero.name | uppercase}} Details</h2>
<div><span>id: </span>{{selectedHero.id}}</div>
<div>
  <label>name:
    <input [(ngModel)]="selectedHero.name" placeholder="name">
  </label>
</div>
```

### Ocultar detalles vacíos con */*ngIf*
Después de que el navegador se actualiza, la aplicación está rota.

Abre las herramientas de desarrollador del navegador y busca en la consola un mensaje de error como este:

```
HeroesComponent.html:3 ERROR TypeError: Cannot read property 'name' of undefined
```

Ahora haz click en uno de los elementos de la lista. La aplicación parece estar funcionando de nuevo. Los héroes aparecen en una lista y los detalles sobre el héroe clickado aparecen en la parte inferior de la página.

### ¿Qué ha pasado?
Cuando se inicia la aplicación, `selectedHero` está con el valor `undefined` por diseño.

Las expresiones vinculantes en la plantilla que hacen referencia a las propiedades de `selectedHero` - expresiones como `{{selectedHero.name}}` -  debe fallar porque no hay ningún héroe seleccionado.

### La solución
El componente sólo debera mostrar los detalles del héroe seleccionado si el `selectedHero` existe.

Envuelva el HTML de detalles del héroe con un `<div>`. Agrega la directiva de Angular `*ngIf` al `<div>` y establécelo en `selectedHero`.

> No olvides el asterisco (*) delante de `ngIf`. Es una parte crítica de la sintáxis.

**Archivo: `src/app/heroes/heroes.component.html`** (*ngif)
```html
<div *ngIf="selectedHero">

  <h2>{{selectedHero.name | uppercase}} Details</h2>
  <div><span>id: </span>{{selectedHero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="selectedHero.name" placeholder="name">
    </label>
  </div>

</div>
```

Después de que el navegador se actualiza, la lista de nombres vuelve a aparecer. El área de detalles está en blanco. Haz click en un héroe y aparecerán sus detalles.

### ¿Por qué funciona?
Cuando `selectedHero` está como `undefined`, `ngIf` elimina los detalles del héroe del DOM. No hay enlaces de `selectedHero` de los que preocuparse.

Cuando el usuario eige un héroe, `selectedHero` tiene un valor y `ngIf` pone el detalle del héroe en el DOM.

### Estilo del héroe seleccionado
Es difícil identificar al héroe selecccionado en la lista cuando todos los elementos `<li>` se aparecen.

Si el usuaruio hace click en "Magneta", ese héroe debe renderizarse con un color de fondo distinto pero sutil como este:

<p align="center">
<img src="https://gist.githubusercontent.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/53a0c1b2806443ac238d7b2d6080caf0f5931702/image-heroes-list-selected.png" width="200" height="200">
</p>

Ese color de héroe seleccionado es el trabajo de la clase CSS `.selected` en los estilos que agregamos antes. Sólo tenemos que aplicar la clase `.selected` al `<li>` cuando el usuario hace click.

El enlace de clase de Angular hace que sea fácil agregar y eliminar una clase de CSS condicionalmente. Simplemente agregamos `[class.some-css-class}="some-condition"` al elemento que deseamos diseñar.

Agregamos el siguiente enlace `[class.selected]` al elemento `<li>` en la plantilla `HeroesComponent`:

**Archivo: `heroes.component.html`** (alterna la clase CSS 'selected')
```typescript
[class.selected]="hero === selectedHero"
```

Cuando el héroe de fila actual es el mismo que el mismo que `selectedHero`, Angular agrega la clase de CSS `selected`. Cuando dos héroes son diferentes, Angular elimina la clase.e

El `<li>` terminado tiene este aspecto:

**Archivo: `heroes.component.html`** (elemento de lista de héroes)
```html
<li *ngFor="let hero of heroes"
  [class.selected]="hero === selectedHero"
  (click)="onSelect(hero)">
  <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
```

### Revisión de código
Para que quede todo claro vamos a ver como han quedado todos los archivos que hemos hecho en esta sección.

**Archivo: `src/app/heroes/heroes.component.ts`**
```typescript
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
import { HEROES } from '../mock-heroes';

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {

  heroes = HEROES;

  selectedHero: Hero;


  constructor() { }

  ngOnInit() {
  }

  onSelect(hero: Hero): void {
    this.selectedHero = hero;
  }
}
```


**Archivo: `src/app/heroes/heroes.component.html`**
```html
<h2>My Heroes</h2>
<ul class="heroes">
  <li *ngFor="let hero of heroes"
    [class.selected]="hero === selectedHero"
    (click)="onSelect(hero)">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>

<div *ngIf="selectedHero">

  <h2>{{selectedHero.name | uppercase}} Details</h2>
  <div><span>id: </span>{{selectedHero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="selectedHero.name" placeholder="name">
    </label>
  </div>

</div>
```


**Archivo: `src/app/heroes/heroes.component.css`**
```css
/* HeroesComponent's private CSS styles */
.selected {
  background-color: #CFD8DC !important;
  color: white;
}
.heroes {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes li.selected:hover {
  background-color: #BBD8DC !important;
  color: white;
}
.heroes li:hover {
  color: #607D8B;
  background-color: #DDD;
  left: .1em;
}
.heroes .text {
  position: relative;
  top: -3px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```

## :arrow_right: Componentes Maestro / Detalles

Por el momento, `HeroesComponent` muestra tanto la lista de héroes como los detalles del héroe seleccionado.

Mantener todas las características en un componente a medida que crece la aplicación no será mantenible. Deberemos dividir los componentes grandes en subcomponentes más pequeños, cada uno centrado en una tarea o flujo de trabajo específico.

En esta página, damos el primer paso en esa dirección al mover los detalles del héroe a un lugar separado y reutilizable `HeroDetailComponent`.

El `HeroesComponent` sólo presentará la lista de héroes. El `HeroDetailComponent` presentará los detalles de un héroe seleccionado.

### Hacer el *HeroDetailComponent*
Usa el CLI de Angular para generar un nuevo componente nombrado `hero-detail`.

```
ng generate component hero-detail
```

El comando hace scaffolding de los archivos de `HeroDetailComponent` y declara el componente en `AppModule`.

### Escribir la plantilla
Corta el HTML para el detalle del héroe desde la parte inferior de la plantilla `HeroesComponent` y pegalo sobre la plantilla repetitiva generada `HeroDetailComponent`.

El HTML pegado se refiere a `selectedHero`. El nuevo `HeroDetailComponent` puede presentar *cualquier* héroe, no sólo un héroe seleccionado. Reemplaza `selectedHero` por `hero` en todas partes en la plantilla.

Cuando termines, la plantilla `HeroDetailComponent` debería de verse así:

**Archivo: `src/app/hero-detail/hero-detail.component.html`**
```html
<div *ngIf="hero">

  <h2>{{hero.name | uppercase}} Details</h2>
  <div><span>id: </span>{{hero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="hero.name" placeholder="name"/>
    </label>
  </div>

</div>
```

### Agrega la propiedad de @Input() al héroe
La plantilla `HeroDetailComponent`se una a la propiedad `hero` del componente que es de tipo `Hero`.

Abre el archvio de clase `HeroDetailComponent` e importa el symbol `Hero`.

**Archivo: `src/app/hero-detail/hero-detail.components.ts`** (importar Hero)
```typescript
import { Hero } from '../hero';
```

La propiedad `hero` [debe ser una propiedad de entrada (Input)](https://angular.io/guide/template-syntax#inputs-outputs), anotada con el decorador `@Input()`, porque el `HeroesComponent` externo [se enlazará](https://angular.io/tutorial/toh-pt3#heroes-component-template) de esta manera.

```html
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
``` 

Modificamos la declaración de importación `@angular/core` para incluir el symbol `Input`. 

**Archivo: `src/app/hero-detail/hero-detail.component.ts`** (Importamos Input)
```typescript
import { Component, OnInit, Input } from '@angular/core';
```

Agregamos una propiedad a `hero`, procedidad por el decorador `@Input().

```typescript
@Input() hero: Hero;
```

Este es el único cambio que debemos hacer en la clase `HeroDetailComponent`. No hay más propiedades. No hay lógica de presentación. Este componente simplemente recibe un objeto héroe a través de su propiedad `hero` y lo muestra.

### Mostar *HeroDetailComponent*
`HeroesComponent` sigue siendo la vista maestra / detalles.

Mostraba los detalles del héroe por sí mismo, antes de cortaremos una pequeña parte de la plantilla. Ahora delegaremos en el `HeroDetailComponent`.

Los dos componentes tendrán una relación padre/hijo. El componente padre `heroesComponent` controlará al componente hijo `HeroDetailComponent` enviándole un nuevo héroe para mostrar cuando el usuario seleccione un héroe de la lista.

No cambiaremos la clase `HeroesComponent` pero cambiaremos su plantilla.

### Actualizar la plantilla *HeroesComponent*
El selector `HeroDetailComponent` es `app-hero-detail`. Aregamos un elemento `<app-hero-detail>` cerca de la parte inferior de la plantilla `HeroesComponent`, donde solía estar la vista de detalles del héroe.

Enlazamos el elemento `HeroesComponent.selectedHero` ala propiedad `hero` de esta manera.

**Archivo: `heroes.component.html`** (enlace de HeroDetail)
```html
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

`[hero]="selectedHero"` es una [propiedad binding](https://angular.io/guide/template-syntax#property-binding) de Angular.

Es un binding de datos *unidireccional* desde la propiedad `selectedHero` de `HeroesComponent` hasta la propiedad `hero` del elemento de destino, que se asigna a la propiedad `hero` de `HeroDetailComponent`.

Ahora cuando el usuario hace click en un héroe en la lista, se verán los cambios de `selectedHero`. Cuando se realizan los cambios de `selectedHero`, la propiedad `hero` se actualza y `HeroDetailComponent` muestra el nuevo héroe.

La plantilla `HeroesComponent` revisada debería de verse así:

**Archivo: `heroes.component.html`**
```html
<h2>My Heroes</h2>

<ul class="heroes">
  <li *ngFor="let hero of heroes"
    [class.selected]="hero === selectedHero"
    (click)="onSelect(hero)">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>

<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

El navegador se refrescará y la aplicación vuelve a funcionar como antes.

### ¿Qué ha cambiado?
Como antes, cada vez que un usuario hace click en un nombre de un héroe, el detalle del héroe aparece debajo de la lista de héroes. Ahora `HeroDetailComponent` está presentando esos detalles en lugar de `HeroesComponent`.

Refactorizando `HeroesComponent` original en dos componentes produce beneficios, tanto ahora como en un futuro:

1. Simplificamos `HeroesComponent` reduciendo sus responsabilidades.
2. Convertimos `HeroDetailComponent` en un rico editor de héroes sin tocar al padre `HeroesComponent`.
3. Evolucionamos `HeroesComponent` sin tocar la vista de detalle del héroe.
4. Reutilizamos `HeroDetailComponent` para algún componente en un fúturo.

### Revisión del código
Nuestros archivos deberían de verse así:

**Archivo: `src/app/hero-detail/hero-detail.component.ts`**
```typescript
import { Component, OnInit, Input } from '@angular/core';
import { Hero } from '../hero';

@Component({
  selector: 'app-hero-detail',
  templateUrl: './hero-detail.component.html',
  styleUrls: ['./hero-detail.component.css']
})
export class HeroDetailComponent implements OnInit {
  @Input() hero: Hero;

  constructor() { }

  ngOnInit() {
  }

}
```

**Archivo: `src/app/hero-detail/hero-detail.component.html`**
```html
<div *ngIf="hero">

  <h2>{{hero.name | uppercase}} Details</h2>
  <div><span>id: </span>{{hero.id}}</div>
  <div>
    <label>name:
      <input [(ngModel)]="hero.name" placeholder="name"/>
    </label>
  </div>

</div>
```

**Archivo: `src/app/heroes/heroes.component.html`**
```html
<h2>My Heroes</h2>

<ul class="heroes">
  <li *ngFor="let hero of heroes"
    [class.selected]="hero === selectedHero"
    (click)="onSelect(hero)">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
</ul>

<app-hero-detail [hero]="selectedHero"></app-hero-detail>
```

**Archivo: `src/app/app.module.ts`**
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { HeroesComponent } from './heroes/heroes.component';
import { HeroDetailComponent } from './hero-detail/hero-detail.component';

@NgModule({
  declarations: [
    AppComponent,
    HeroesComponent,
    HeroDetailComponent
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## :arrow_right: Servicios
El Tour de Héroes `HeroesComponent` está recibiendo y mostrando datos falsos.

Después de la refactorización en este tutorial, `HeroesComponent` se apoyará y se centrara en dar soporte a la vista. También será más fácil realizar una prueba unitaria con un servicio simulado..


### ¿Por qué los servicios?
Los componentes no deben buscar ni guardar datos directamente y, desde luego, no deben presentar datos falsos a sabiendas. Deben enfocarse en presentar datos y delegar el acceso a datos a un servicio.

En esta lección, crearemos un `HeroService` donde toda las vistas de la aplicación podrán usar para obtener héroes. En lugar de crear un servicio con `new`, dependeremos de [inyección de dependencia](https://angular.io/guide/dependency-injection) de Anglar para inyectarlo en el constructor `HeroesComponent`.

Los servicios son una excelente manera de compartir información entre cases que no se conocen entre sí. Crearemos `MessageService` que inyectará en dos sitios:

1. En `HeroService` que usa el servicio para enviar el mensaje.
2. En `MessageComponent`que se muestra el mensaje.

### Crear *HeroService*
Con el CLI de Angular, creamos un servicio llamado `hero`

```
ng generate service hero
```

El comando genera una estructura de la clase `HeroService` en `src/app/hero/hero.service.ts`. La clase `HeroService` debe verse como el siguiente ejemplo.

**Archivo: `src/app/hero.service.ts`** (Nuevo Servicio)
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class HeroService {

  constructor() { }

}
```

### Servicios inyectados (@Injectable)
Observamos que el nuevo servicio importa el symbol de Angular `Injectable` y anota la clase con el decorador `@Injectable()`. Esto marca la clase como una que participa en el *sistema de inyección de dependencia*. La clase `HeroService`proporcionará un servicio inyectable y también  puede tener sus propias dependencias inyectadas. Todavía no tenemos dependencias, pero [pronto lo haremos](https://angular.io/tutorial/toh-pt4#inject-message-service).

El decorador `@Injectable()` acepta metadatos del objeto del servicio, de la misma manera que con el decorador `@Component()` que hicimos para la clase de componentes.

### Obtener datos del héroe
`HeroService` puede obtener los datos del héroe desde cualquier lugar - un servicio web, almacenamiento local, o una fuente de datos simulada.

Eliminar el acceso a los datos de los componentes significa que podemos cambiar de opinión sobre la implementación en cualquier momento, sin tocar ningún componente. No sabemos como funciona el servicio.

La implementación en esta lección continuará entregando *héroes simulados*.

Importamos `Hero` y `HEROES`.

```typescript
import { Hero } from './hero';
import { HEROES } from './mock-heroes';
```

Agrega un método `getHeroes` para devolver a los *héroes falsos*.

```typescript
getHeroes(): Hero[] {
  return HEROES;
}
```

### Proporcionar HeroService
Debemos de poner `HeroService` a disposición del sistema de inyección de dependencia antes de que Angular pueda *inyectarlo* en `HeroesComponent`, como lo haremos a continuación. Haremos esto registrando un *proveedor*. Un proveedor es algo que puede crear o engregar un servicio; en este caso, una instalcia de la clase `HeroService` para proporcionar el servicio.

Ahora, debemos asegurarnos de que `HeroService` está registrado como proveedor de este servicio. Lo estamos registrando con un *inyector*, que es el objeto que es responsable de elegir e inyectar el proveedor donde se requiere.

De forma predeterminada, el comando CLI de Angular `ng generate service` registra un proveedor con el *inyector raíz* para el servicio al incluir los metadatos del proveedor al decorador `@Injectable`.

Si miramos la declaración `@Injectable()` justo antes de la definición de la clase `HeroService`, podemos ver que el valor de `providedIn` de los metadatos es 'root':

```
@Injectable({
  providedIn: 'root',
})
```

Cuando proporcionamos el servicio en la raíz, Angular crea una única instancia compartida de `HeroService` e inyecta en cualquier clase que lo solicite. El registro del proveedor de `@Injectable` en los metadatos también permite que a Angular opimizar una aplicación eliminando el servicio si resulta que no se usa después de todo.

> Para obtener más información sobre proveedores, consulta la [sección proveedores](https://angular.io/guide/providers). Para tener más información acerca de los inyectores consulta la [guía de inyección de dependencias](https://angular.io/guide/dependency-injection).

`HeroService` está ahora listo para conectar a `HeroesComponent`.

> Esta es una muesta de código provisional que nos permitirá proporcionar y usar `HeroService`. El código será diferente de `HeroService` en la revisión de código final.

### Actualizar *HeroesComponent*
Abre el archivo de la clase `HeroesComponent`.

Borra la importación `HEROES`, porque ya no la necesitaremos. Importaremos `HeroService` en su lugar.

**Archivo: `src/app/heroes/heroes.component.ts`** (importar HeroService)
```typescript
import { HeroService } from '../hero.service';
```

Reemplaza la definición de la propiedad `heroes` con una declaración simple.

```typescript
heroes: Hero[];
```

### Inyectar el *HeroService*
Agregamos un parámetro privado a `heroService`de tipo `HeroService` al constructor.

```typescript
constructor(private heroService: HeroService) { }
```

El parámetro define simultáneamente una propiedad privada de `heroService` y la identifica como una instancia simple de `HeroService`.

Cuando Angular crea `HeroesComponent`, el sistema de [Inyección de Dependencia](https://angular.io/guide/dependency-injection) establece el parámetro `heroService` en la única instancia de `HeroService`.

### Agergar *getHeroes()*
Crea una función para recuperar los héroes del servicio.

```typescript
getHeroes(): void {
  this.heroes = this.heroService.getHeroes();
}
```

### Llamarlo en el ngOnInit
Si bien puedes llamar a `getHeroes()` en el constructor, esta no es la mejor práctica.

Reserva el constructor para la inicialización simple, como el cableado de los parámetros del constructor a las propiedades. El constructor no debería *hacer nada*. Ciertamente, no debería de llamar a una función que realiza solicitudes HTTP a un servidor remoto como lo haría un servicio de datos real.

En su lugar, llama a `getHeroes()` dentro del [hook de ciclo de vida ngOnInit](https://angular.io/guide/lifecycle-hooks) y deja que Angular llame a `ngOnInit` en el momento apropiado después de construir una instancia `HeroesComponent`.

```typescript
ngOnInit() {
  this.getHeroes();
}
```

### Así se ejecuta
Después de que el navegador se refresque, la aplicación debería de ejecutarse como antes, mostrando una lista de héroes y una vista de detalles de héroe cuando haga clic en un nombre de héroe.

### Datos observables
El método `HeroService.getHeroes()` tiene una *firma síncrona*, lo que implica que `HeroService` puede obtener héroes con sincronía. `HeroesComponent` consume el resultado de `getHeroes()` obteniendo los héroes encontrados de forma síncrona. 

```typescript
this.heroes = this.heroService.getHeroes();
```

Esto no funcionará en una aplicación real. Te estás saliendo con la tuya ahora porque el servicio actualmente devuelve *héroes falsos*. Pero pronto la aplicación obtendrá héroes de un servidor remoto, que es una operación inherentemente asíncrona.

`HeroService` debe de esperar a que el servidor responda, `getHeroes()` no puede regresar de inmediato con datos de héroe, y el navegador no se bloqueará mientras el servicio espere.

`HeroService.getHeroes()` debe de tener una *firma asíncrona* de algún tipo.

Puede tomar una devolución de llamada. Podría regresar una `Promise`. Podría devolver un `Observable`.

En este tutorial, `HeroService.getHeroes()` se devolverá `Observable` en parte porque enventualmente usaremos el método de Angular `HttpClient.get` para obtener los héroes y [HttpClient.get() devolverá un Observable](https://angular.io/guide/http).

### Observable HeroService
`Observable` es una de las clases clave de la [bliblioteca RxJS](http://reactivex.io/rxjs/).

Más adelante aprenderemos que los métodos de Angular `HttpClient` devuelven RxJS `Observable`. En este tutorial, simularemos obtener datos del servidor con la función `of()` de RxJS.

Abrimo el archivo `HeroService` e importamos los symbols `Observable` y `of` de RxJS.

**Archivo: `src/app/hero.service.ts`** (Importacion Observable)
```typescript 
import { Observable, of } from 'rxjs';
```

Remplaza el método `getHeroes` con este.

```typescript
getHeroes(): Observable<Hero[]> {
  return of(HEROES);
}
```

`of(Heroes)` devuelve un `Observable<Hero[]>` que emite un único valor, la matriz de héroes simulados.

### Suscribirse en el *HeroesComponent* 

El método `HeroService.getHeroes` para devolver `Hero[]`. Ahora devuelve `Observable<Hero[]>`.

Vamos a tener que adaptar esta diferencia en `HeroesComponent`.

Encuentra el método `getHeroes` y reemplazalo con el siguiente código. (Mostramos la versión anterior para comparar)

**Archivo: `heroes.component`** (Observable)
```typescript
getHeroes(): void {
  this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
}
```

**Archivo: `heroes.component`** (Original)
```typescript
getHeroes(): void {
  this.heroes = this.heroService.getHeroes();
}
```

`Observable.suscribe()` es la única diferencia crítica.

La versión anterior asigna una matriz de héroes a la propiedad `heroes` del component. La asignación se produce de forma síncrona, como si el servidor pudiera devolver héroes al instante o el navegador pudiera congelar la interfaz de usuario mientras esperaba la respuesta del servidor.

Esto *no funcionaría* cuando en realidad `HeroService` se le realicen solicitudes de un servidor remoto.

La nueva version espera que `Observable` emita la serie de héroes, lo que podría suceder ahora o en varios minutos a partir de ahora. Luego `subscribe` pasa la matriz emitida a la devolución de la llamada, que establece la propiedad del componente `heroes`.

### Mostrar mensajes
En esta sección lo haremos.
- Agrega `MessagesComponent` que muestra los mensaje dela aplicación en la parte inferior de la pantalla.
- Crea un inyectable, a nivel de aplicación `MessageService` para enviar mensajes que se muestren.
-  Inyectar `MessageService` en `HeroService`.
-  Muestra un mensaje cuando `HeroService` obtiene con éxito héroes.

### Crear *MessagesComponent*
Usa el CLI para crear `MessagesComponent`.

```
ng generate component messages
```

El cCLI crea los archivos de los componentes en la carpeta y los declara en `src/app/messagesMessagesComponentAppModule`.

Modifica la plantilla `AppComponent` par amostrar el generado `MessagesComponent`.

**Archivo: `/src/app/app.component.html`**
```typescript
<h1>{{title}}</h1>
<app-heroes></app-heroes>
<app-messages></app-messages>
```

Deberíamos ver el párrafo predeterminado `MessageComponent` en la parte inferior de la página.

### Crea el *MessageService*
Utiliza el CLI para crear `MessageService` en `src/app`.

```
ng generate service message
```

Abre `MessageService` y reemplaza su contenido con lo siguiente.

**Archivo: `/src/app/message.service.ts`**
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class MessageService {
  messages: string[] = [];

  add(message: string) {
    this.messages.push(message);
  }

  clear() {
    this.messages = [];
  }
}
```

El servicio expone su caché `messages` y dos métodos: uno `add()` un mensaje a la caché y otro a `clear()` la caché.

### Inyectarlo en *HeroService*
Vamos a volver a abrir `HeroService`e importar el `MessageService`

**Archivo: `/src/app/hero.service.ts`** (importar MessageService)
```typescript
import { MessageService } from './message.service';
```

Modifica el constructor con un parámetro que declare una propiedad `messageService` privada. Angular inyectará el singleton `MessageService`en esa propiedad cuando cree `HeroService`.

```typescript
constructor(private messageService: MessageService) { }
```

> Este es un escenario típico de "servicio en servicio": se inyecta `MessageService` en `HeroService` que se inyecta en `HeroesComponent`.

### Enviar un mensaje desde *HeroService*
Modifica el método `getHeroes` par aenvíar un mensaje cuando se vaya a buscar a los héroes.

```typescript
getHeroes(): Observable<Hero[]> {
  // TODO: send the message _after_ fetching the heroes
  this.messageService.add('HeroService: fetched heroes');
  return of(HEROES);
}
```

### Mostrar el mensaje desde *HeroService*
`MessageComponent` debería mostrar todos los mensajes, incluido el mensaje enviado por `HeroService` cuando obtiene héroes.

Abre `MessageComponent`e importa `MessageService`

**Archivo: `/src/app/messages/messages.component.ts`** (importar MessageService)
```typescript
import { MessageService } from '../message.service';
```

Modifica el constructor con un parámetro que declare una propiedad pública `messageService`. Angular inyectará el singleton `MessageService` en esa propiedad cuando cree el `MessagesComponent`

```typescript
constructor(public messageService: MessageService) {}
```

La propiedad `messageService` debe ser pública porque está a punto de unirse a ella en la plantilla.

> Angular sólo se une a las propiedades de los componentes *públicos*

### Enlace a *MessageService*
Remplaza la plantilla `MessagesComponent` generada por el CLI con lo siguiente.

**Archivo: `/src/app/messages/messages.component.html`**
```typescript
<div *ngIf="messageService.messages.length">

  <h2>Messages</h2>
  <button class="clear"
          (click)="messageService.clear()">clear</button>
  <div *ngFor='let message of messageService.messages'> {{message}} </div>

</div>
```

Esta plantilla se une directamente a la del componente `messageService`.
- `ngIf` sólo muestra el área de mensajes si hay mensajes para mostrar.
- `ngFor` presenta la lista de mensajes en elementos repetidos.
- Un [enlace de evento](https://angular.io/guide/template-syntax#event-binding) de Angular víncula el evento click del botoón a `MessageService.clear()`.

Los mensajes se verán mejor cuando agregemos los estios de CSS privados a los `messages.component.css` listados en una de las pestañas de *revisión de código final* a continuación.

El navegador se actualiza y la página muestra la lista de héroes. Desplázalo hasta la parte inferior para ver el mensaje `HeroService` el área de mensajes. Haz click en el botón "borrar" y el área de mensaje desaparecerá.

### Revisión del código final

**Archivo: `/src/app/hero.service.ts`**
```typescript
import { Injectable } from '@angular/core';

import { Observable, of } from 'rxjs';

import { Hero } from './hero';
import { HEROES } from './mock-heroes';
import { MessageService } from './message.service';

@Injectable({
  providedIn: 'root',
})
export class HeroService {

  constructor(private messageService: MessageService) { }

  getHeroes(): Observable<Hero[]> {
    // TODO: send the message _after_ fetching the heroes
    this.messageService.add('HeroService: fetched heroes');
    return of(HEROES);
  }
}
```

**Archivo: `/src/app/message.service.ts`**
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class MessageService {
  messages: string[] = [];

  add(message: string) {
    this.messages.push(message);
  }

  clear() {
    this.messages = [];
  }
}
```

**Archivo: `/src/app/heroes/heroes.component.ts`**
```typescript
import { Component, OnInit } from '@angular/core';

import { Hero } from '../hero';
import { HeroService } from '../hero.service';

@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {

  selectedHero: Hero;

  heroes: Hero[];

  constructor(private heroService: HeroService) { }

  ngOnInit() {
    this.getHeroes();
  }

  onSelect(hero: Hero): void {
    this.selectedHero = hero;
  }

  getHeroes(): void {
    this.heroService.getHeroes()
        .subscribe(heroes => this.heroes = heroes);
  }
}
```

**Archivo: `/src/app/messages/messages.component.ts`**
```typescript
import { Component, OnInit } from '@angular/core';
import { MessageService } from '../message.service';

@Component({
  selector: 'app-messages',
  templateUrl: './messages.component.html',
  styleUrls: ['./messages.component.css']
})
export class MessagesComponent implements OnInit {

  constructor(public messageService: MessageService) {}

  ngOnInit() {
  }

}
```

**Archivo: `/src/app/messages/messages.component.html`**
```html
<div *ngIf="messageService.messages.length">

  <h2>Messages</h2>
  <button class="clear"
          (click)="messageService.clear()">clear</button>
  <div *ngFor='let message of messageService.messages'> {{message}} </div>

</div>
```

**Archivo: `/src/app/messages/messages.component.css`**
```css
/* MessagesComponent's private CSS styles */
h2 {
  color: red;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: lighter;
}
body {
  margin: 2em;
}
body, input[text], button {
  color: crimson;
  font-family: Cambria, Georgia;
}

button.clear {
  font-family: Arial;
  background-color: #eee;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  cursor: hand;
}
button:hover {
  background-color: #cfd8dc;
}
button:disabled {
  background-color: #eee;
  color: #aaa;
  cursor: auto;
}
button.clear {
  color: #888;
  margin-bottom: 12px;
}
```

**Archivo: `/src/app/app.module.ts`**
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';
import { HeroesComponent } from './heroes/heroes.component';
import { HeroDetailComponent } from './hero-detail/hero-detail.component';
import { MessagesComponent } from './messages/messages.component';

@NgModule({
  declarations: [
    AppComponent,
    HeroesComponent,
    HeroDetailComponent,
    MessagesComponent
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [
    // no need to place any providers due to the `providedIn` flag...
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

**Archivo: `/src/app/app.component.html`**
```html
<h1>{{title}}</h1>
<app-heroes></app-heroes>
<app-messages></app-messages>
```

### Sumario
- Refactorizamos el acceso a los datos de la clase `HeroService`.
- Registramos el `HeroService` como el proveedor de su servicio en el nivel de raíz para que pueda ser inyectado en cualquier lugar de la aplicación.
- Utilizamos la inyección de dependencia de Angular a inyectarlo en un componente.
- Proporcionamos al método `HeroService` recoger datos de una firma asincrónica.
- Descubrimos `Observable`y la biblioteca RxJS Observable .
 Usamos RxJS `of()`para devolver un observable de héroes falsos `(Observable<Hero[]>)`.
- El componente `ngOnInit` del hook del ciclo de vida llamando al método `HeroService`, no al constructor.
- Creamos un `MessageService` para la comunicación débilmente acoplada entre clases.
- `HeroService` inyectado en un componente  y creando otro servicio inyectado de `MessageService`.

## :arrow_right: Enrutamiento
Hay nuevos requisitos para la aplicación Tour of Heroes:
- Agregar una vista de Tablero.
- Agregar la capacidad de navegar entre las vistas *Héroes* y *Tablero*.
- Cuando los usuarios hacen click en un nombre de héroe en cualquiera de las vistas, navega hasta una vista de detalle del héroe seleccionado.
- Cuando los usuarios hacen click en un *enlace profundo* en un correo electrónico, abre la vista detalles de un héroe en particular.

Cuando hayamos terminado, los usuarios podrán navegar por la aplicación de esta manera:

<p align="center">
<img src="https://gist.githubusercontent.com/mrcodedev/228bd1f09270d921209413d1f427e499/raw/b19fda755dea3431f4c2709c21bf89eefbee0f8b/image-nav-diagram.png">
</p>

### Agrega *AppRoutingModule*
Una mejor páctica de Angular es cargar y configurar el enrutador en un módulo separado de nivel superior dedicado al enrutamiento e importado por la raíz `AppModule`.

Por convención, el nombre de la clase del módulo es `AppRoutingModule` y pertenece a `app-routing.module.ts` en la carpeta `src/app`.

Usamos el CLI para generarlo:

```
ng generate module app-routing --flat --module=app
```

> `--flat` coloca el archivo en `src/app` en lugar de su propia carpeta.
> `--module=app` le dice a el CLI que lo registre en `imports` de la matriz `AppModule`.

El archivo generado se verá así:

**Archivo: `src/app/app-routing.module.ts`** (generado)
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  imports: [
    CommonModule
  ],
  declarations: []
})
export class AppRoutingModule { }
```

Por lo general, no declara los componentes en un módulo de enrutamiento para que pueda eliminar el array `@NgModule.declarations` y eliminar las referencias de `CommonModule`.

Configuraremos el enrutador con `Routes`, en el `RouterModule` así que importamos dos symbols de la librería `@angular/router`.

Agregamos un array `@NgModule.exports` con `RouterModule` en él. Exportamos `RouterModule` hace que las directivas de enrutadores estén disponible para su uso en el componente`AppModule` que necesitarémos más adelante.

`AppRoutingModule` se ve así ahora:

**Archivo: `src/app/app-routing.module.ts`** (v1)
```typescript
import { NgModule }             from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

@NgModule({
  exports: [ RouterModule ]
})
export class AppRoutingModule {}
```

### Añadir rutas
Las rutas le dicen al enrutador qué vista mostrar cuando un usuario hace clic en un enlace o pega una URL en la barra de direcciones del navegador.

Una `Route` típica de Angular tiene dos propiedades:

1. `path`: una cadena que coincide con la URL en la barra de direcciones del navegador.
2. `component`: el componente que debe crear el enrutador cuando navega por esta ruta.

Vamos a intentar navegar hacia el componente `HeroesComponent` cuando la URL es esta `localhost:4200/heroes`.

Importa el archivo `HeroesComponent` par aque pueda referenciarlo en `Route`. Luego, define un array de rutas con un único componente `route`.

```typescript
import { HeroesComponent } from './heroes/heroes.component';

const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];
```

Una vez hayamos terminado de configurarlo, el enrutador coincidirá con esa URL `path: 'heroes'` y mostrará el componente `HeroesComponent`.

### *RouterModule.forRoot()*
Primero debemos de inicializar el enrutador y comenzar a escuchar los cambios de ubicación del navegador.

Agregar `RouterModule` al array `@NgModule.imports` y configurarla con `routes` en un solo paso llamando dentro del array `RouterModule.forRoot()`, de esta manera el array `imports`, queda así:

```typescript
imports: [ RouterModule.forRoot(routes) ],
```

> Se llama al método `forRoot()` porque configura el enrutador en el nivel raíz de la aplicación. El método `forRoot()` suministra los proveedores de servicios y las directivas necesarias para el enrutamiento y realiza la navegación inicial en función de la URL del navegador actual.

### Añadir *RouterOutlet*
Abre la plantilla `AppComponent`y reemplaza el elemento `<app-heroes>` con un elemento `<router-outlet>`.

**Archivo: `src/app/app.component.html`** (router-outlet)
```html
<h1>{{title}}</h1>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

Hemos eliminado `<app-heroes>` porque sólo mostraremos `HeroesComponent` cuando el usuario navega hacia él.

`<router-outlet>` le dice al enrutador dónde mostrar las vistas enrutadas.

> `RouterOutlet`es una de las directivas de enrutador que están disponibles para las `AppComponent` porque `AppModule` importa  `AppRoutingModule` que exporta `RouterModule`.

### Pruébalo
Debería ejecutarse con este comando CLI.

```
ng serve
```

El navegador debe de actualizarse y mostrar el título de la aplicación, pero no la lista de héroes.

Mira la barra de dirección del navegador. La URL termina en `/`. La ruta de acceso a `HeroesComponet` es `/heroes`.

Agrega `/heroes` a la URL de la barra de direcciones del navegador. Deberíamos ver el conocido maestro/detalle de la vista de héroes.

### Añadir un enlace de navegación (routerLinlk)
Los usuarios no deberían tener que pegar una URL de ruta en la barra de direcciones. Deben poder hacer clic en un enlace para navegar.

Agregamos un elemento `<nav>` y, dentro de eso, un elemento de anclaje que, al hacer click, desencadena la navegación hacia `HeroesComponent`. La plantilla `AppComponent` revisada se ve así:

**Archivo: `src/app/app.component.html`** (héroes RouterLink)
```html
<h1>{{title}}</h1>
<nav>
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```
El [atributo routerLink](https://angular.io/tutorial/toh-pt5#routerlink) se estable en `/heroes`, la cadena con la que el enrutador coincide con la ruta `HeroesComponent`. El `routerLink` es el selector de la [directiva RouterLink](https://angular.io/tutorial/toh-pt5#routerlink) que hace que el usuario haga click en las navegaciones del enrutador. Es otra de las directivas públicas en `RouterModule`.

El Navegador se actualiza y muestra el título de la aplicación y el enlace de héroes, pero no la lista de héroes.

Hacemos click en el enlace. La barra de direcciones se actualiza a `/heroes` y aparece en la lista de héroes.

> Haz esto y el futuro navegador de enlaces se verá mejor añadiendo unos estilos privados de CSS a `app.component.css`. Tendrás esto en la revisión final del código.

### Agregar una vista de tablero
El enrutamiento tiene más sentido cuando hay múltiples vistas. Hasta ahora solo hay una vista de héroes.

Agregamos una `DashboardComponent` usando el CLI:

```
ng generate component dashboard
```

El Cli genera los archivos para `DashboardComponent` y los declara en `AppModule`.

Reemplaza el contenido del archivo predeterminado en estos tres archivos de la siguiente manera y luego regrese para una pequeña discusión:

**Archivo: `src/app/dashboard/dashboard.component.html`**
```html
<h3>Top Heroes</h3>
<div class="grid grid-pad">
  <a *ngFor="let hero of heroes" class="col-1-4">
    <div class="module hero">
      <h4>{{hero.name}}</h4>
    </div>
  </a>
</div>
```

**Archivo: `src/app/dashboard/dashboard.component.ts`**
```typescript
import { Component, OnInit } from '@angular/core';
import { Hero } from '../hero';
import { HeroService } from '../hero.service';

@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
  styleUrls: [ './dashboard.component.css' ]
})
export class DashboardComponent implements OnInit {
  heroes: Hero[] = [];

  constructor(private heroService: HeroService) { }

  ngOnInit() {
    this.getHeroes();
  }

  getHeroes(): void {
    this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes.slice(1, 5));
  }
}
```

**Archivo: `src/app/dashboard/dashboard.component.css`**
```css
/* DashboardComponent's private CSS styles */
[class*='col-'] {
  float: left;
  padding-right: 20px;
  padding-bottom: 20px;
}
[class*='col-']:last-of-type {
  padding-right: 0;
}
a {
  text-decoration: none;
}
*, *:after, *:before {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
h3 {
  text-align: center; margin-bottom: 0;
}
h4 {
  position: relative;
}
.grid {
  margin: 0;
}
.col-1-4 {
  width: 25%;
}
.module {
  padding: 20px;
  text-align: center;
  color: #eee;
  max-height: 120px;
  min-width: 120px;
  background-color: #607d8b;
  border-radius: 2px;
}
.module:hover {
  background-color: #eee;
  cursor: pointer;
  color: #607d8b;
}
.grid-pad {
  padding: 10px 0;
}
.grid-pad > [class*='col-']:last-of-type {
  padding-right: 20px;
}
@media (max-width: 600px) {
  .module {
    font-size: 10px;
    max-height: 75px; }
}
@media (max-width: 1024px) {
  .grid {
    margin: 0;
  }
  .module {
    min-width: 60px;
  }
}
```

La plantilla presenta un gir de enlaces de héroes.

- El `*ngFor` crea tantos enlaces como están en el array del componente `heroes`.
- Los enlaces se diseñan como bloques de coloers por `dashboard.component.css`.
- Los enlaces no van a ningún lado todavía, pero lo harán en breve.

La clase es similar a la clase de `HeroesComponent`.

- Define una propiedad `heroes` al array.
- El constructor espera que Angular lo inyecte `HeroService` en una propiedad `heroService`privada.
- El hook `ngOnInit()` del ciclo de vida llama a `getHeroes`.

`getHeroes` devuelve la lista de héroes divididos en las posiciones 1 y 5, devolviendo sólo cuatro de los Héroes principales (2º, 3º, 4º, y 5º).

```typescript
getHeroes(): void {
  this.heroService.getHeroes()
    .subscribe(heroes => this.heroes = heroes.slice(1, 5));
}
```

### Agregar la ruta del tablero
Para navegar al tablero, el enrutador necesita una ruta apropiada.

Importar el `DashboardComponent` en el `AppRoutingModule`.

**Archivo: `src/app/app-routing.module.ts`** (importa DashBoardComponent)
```typescript
import { DashboardComponent }   from './dashboard/dashboard.component';
```

Agrega una ruta al array `AppRoutingModule.routes` que coincida con una ruta a `DashboardComponent`.

```typescript
{ path: 'dashboard', component: DashboardComponent },
```

### Agregar una ruta predeterminada
Cuando se inicia la aplicación, la barra de direcciones de los navegadores apunta a la raíz del sitio web. Eso no coincide con ninguna ruta existente por lo que el enrutador no navega a ninguna parte. El espacio debajo de el `<router-outlet>` está en blanco.

Para hacer que la aplicación vaya automáticamente al tablero, agregua la siguiente ruta al array `AppRoutingModule.Routes`.

```typescript
{ path: '', redirectTo: '/dashboard', pathMatch: 'full' },
```

Esta ruta redirige una URL que coincide completamente con la ruta vacía a la ruta cuya ruta es `/dashboard`.

Después de que el navegador se actualiza, el enrutador carga el `DashboardComponent` y la barra de direcciones del navegador muestra la URL `/dashboard`

### Añadir enlace del dashboard al shell
El usuario debe poder navegar hacia adelante y hacia atrás entre el `DashboardComponent` y el `HeroesComponent` haciendo clic en los enlaces en el área de navegación cerca de la parte superior de la página.

Agregua un enlace de navegación del tablero a la plantilla `AppComponent` de shell, justo encima del enlace *Héroes*.

**Archivo: `src/app/app.component.html`**
```html
<h1>{{title}}</h1>
<nav>
  <a routerLink="/dashboard">Dashboard</a>
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

Después de que el navegador se actualice, puedes navegar libremente entre las dos vistas haciendo click en los enlaces.
