# Angular

- [Что такое Angular?](#angular)
- [Директивы. Типы директив](#directives-types-of-directives)
- [Способ привязки данных в Angular. Data Binding](#data-binding)
- [Директивы Input(), Output()](#directives-input-output)
- [Пайпы](#pipes)
- [Life cycle hooks](#life-cycle-hooks)
- [Сервисы](#services-in-angular)
- [Модульность в Angular](#modules-in-angular-lazy-loading)
- [Observable. Отличия от Promise.](#observable-vs-promise)
- [Динамические элементы](#dynamic-elements)
- [Dependency Injection](#dependency-injection)
- [Injection Token](#injection-token)
- [Маршрутизация в Angular](#routing-in-angular)
- [Директивы ng-template, ngTemplateOutlet, ng-container, ng-content](#ng-template-ngtemplateoutlet-ng-container-ng-content)
- [Организация шаринга данных. NgRx](#organization-of-data-sharing)
- [Redux/Flux pattern](#redux-flux-pattern)
- [Observer pattern](#observer-pattern)
- [Сборка и настройка Angular проекта.](#assembly-in-angular)
- [Virtual DOM](#virtual-dom)
- [Опция trackBy](#trackby)
- [Reactive Forms в Angular](#reactive-forms-angular)
- [Event Bus (Шина событий)](#event-bus)
- [Безопасность в Angular](#security-in-angular)
- [Angular Universal](#angular-universal)
- [Angular Service Worker](#angular-service-workers)
- [Angular ngZone](#angular-ngzone)
- [Angular Internationalization](#internationalization)
- [Запуска обнаружения изменений в Angular](#starting-change-detection-angular)
- [Оптимизация производительность асинхронных валидаторов в Angular](#optimising-the-performance-of-asynchronous-validators)
- [Автономные компоненты (Standalone)](#standalone)

## Angular

> Angular - это открытая платформа для разработки веб-приложений, созданная компанией Google. Она позволяет разработчикам создавать динамические одностраничные приложения (SPA) с использованием HTML, CSS и JavaScript. Angular предоставляет множество инструментов и функций, таких как двустороннее связывание данных, инъекция зависимостей, маршрутизация и многие другие, что делает процесс разработки более эффективным и продуктивным.

### Что такое Angular CLI?

> Angular CLI `Command Line Interface` - это инструмент командной строки, предоставляемый Angular, который упрощает и автоматизирует процесс создания, развертывания и тестирования приложений Angular. Он позволяет разработчикам создавать новые проекты, компоненты, сервисы, директивы и многое другое, используя простые команды в терминале. Кроме того, Angular CLI предоставляет мощные инструменты для сборки и оптимизации приложений, включая функции, такие как автоматическая минификация и сжатие файлов, анализ размера бандла и многое другое. Это существенно упрощает процесс разработки и повышает производительность.

Чтобы узнать версию Angular CLI:

- `ng version` или `ng --version`: Для глобальной версии Angular CLI
- `npx ng version`: Для версии Angular CLI в конкретном проекте (если вы находитесь в каталоге проекта):

### Команды Angular CLI выполняют следующие действия:

- `ng new` - создает новый проект Angular с настройками по умолчанию в указанной директории. Например, ng new my-app создаст новый проект Angular в директории my-app.
- `ng generate` - создает новый компонент, сервис, директиву или другой элемент приложения Angular. Например, ng generate component my-component создаст новый компонент с именем my-component.
- `ng serve` - запускает локальный сервер разработки, который автоматически перезагружает приложение при изменении кода. Приложение будет доступно по адресу `http://localhost:4200`. Если нужен определенный порт при запуске - `ng serve --port 4201`
- `ng build` - собирает приложение Angular в оптимизированные файлы JavaScript, CSS и HTML, которые можно развернуть на сервере. Например, ng build --prod соберет приложение в режиме продакшена.

> Каждая из этих команд имеет множество опций и флагов для настройки поведения. Вы можете узнать больше о командах `Angular CLI`, запустив команду `ng help` в терминале.

Флаг `--host`

- Этот флаг задает IP-адрес или хост для сервера. По умолчанию используется localhost, но вы можете установить его, чтобы сервер был доступен по сети. Это позволяет другим устройствам в вашей сети обращаться к вашему приложению. Например:

```npm
ng serve --host 0.0.0.0
```

Флаг `--poll`

- Этот флаг используется для настройки механизма отслеживания изменений в файлах. Это может быть полезно, если вы работаете с файловыми системами, которые не поддерживают стандартные методы отслеживания изменений (например, Docker или некоторые сетевые файловые системы). Вы можете задать период в миллисекундах, чтобы установить, как часто будет происходить опрос файлов. Например:

```npm
ng serve --poll 2000
```

Пример запуска сборки на компьютере, а проверки сборки на смартфоне.

1. Запустите сервер с параметрами:

- Используйте команду `ng serve с флагом --host` для доступности по сети:

```npm
ng serve --host 0.0.0.0 --port 4200
```

> Здесь 0.0.0.0 означает, что сервер будет доступен на всех интерфейсах вашего компьютера, а 4200 — это стандартный порт для Angular.

2. Определите IP-адрес вашего компьютера

- Узнайте свой локальный IP-адрес. Это можно сделать, выполнив команду в терминале:

  - Для Windows: ipconfig
  - Для macOS/Linux: ifconfig или ip a

- Найдите строку с вашим сетевым подключением и запомните локальный IP-адрес (например, 192.168.1.10).

3. Подключитесь со смартфона

- Убедитесь, что ваш телефон подключен к той же Wi-Fi-сети, что и ваш компьютер.
- Откройте браузер на телефоне и введите IP-адрес вашего компьютера с портом, например:

```npm
http://192.168.1.10:4200
```

> Теперь вы должны быть в состоянии увидеть ваше Angular-приложение на телефоне.

### Что такое компонент? Как объявляется?

> Компоненты в Angular - это основные строительные блоки веб-приложений, которые позволяют разбить интерфейс на небольшие, независимые и переиспользуемые части. Каждый компонент содержит свой собственный шаблон (HTML), стили (CSS) и логику (TypeScript). Компоненты позволяют создавать модульные приложения, которые могут быть легко поддерживаемы и масштабируемы.

> Для объявления компонента в Angular, необходимо создать класс TypeScript, который определяет логику компонента, и декоратор @Component, который содержит метаданные компонента, такие как селектор, шаблон, стили и другие свойства. Например, вот простой компонент Angular:

```typescript
import { Component } from '@angular/core'

@Component({
	selector: 'app-hello-world',
	template: '<h1>Hello World!</h1>',
	styles: ['h1 { color: red; }'],
})
export class HelloWorldComponent {}
```

### Для чего нужны:

- `selector` - это свойство компонента в Angular, которое определяет селектор CSS, который будет использоваться для выбора элемента DOM, который будет заменен компонентом. Этот селектор может быть использован в HTML-разметке для создания экземпляра компонента.
- `template/templateUrl` - это свойство компонента в Angular, которое определяет шаблон, который будет использоваться для отображения компонента. `template` содержит сам шаблон в виде строки, а templateUrl содержит ссылку на файл шаблона. Шаблон определяет структуру и содержание компонента.
- `styles/styleUrls` - это свойство компонента в Angular, которое определяет стили, которые будут применены к компоненту. styles содержит стили в виде строки, а styleUrls содержит ссылки на файлы со стилями. Стили могут быть применены к компоненту, чтобы изменить его внешний вид.
- `providers` - это свойство компонента в Angular, которое определяет список провайдеров зависимостей, которые будут использоваться в компоненте. Провайдеры могут быть использованы для внедрения зависимостей в компонент, таких как сервисы или другие компоненты.
- `changeDetection` - это свойство компонента в Angular, которое определяет, как Angular будет обнаруживать изменения в компоненте. Это свойство определяет стратегию обнаружения изменений, которая может быть `OnPush`, `Default` или `Manual`. Стратегия `OnPush` означает, что Angular будет обнаруживать изменения только тогда, когда входные данные компонента изменятся, а `Default` означает, что Angular будет обнаруживать изменения при любом изменении в компоненте. Стратегия Manual означает, что обнаружение изменений будет происходить только вручную с помощью метода `detectChanges()`.

### Что такое модуль? Как объявляется?

> Модуль в Angular - это логическая группа компонентов, директив, сервисов и других функциональных элементов, которые работают вместе для выполнения определенной задачи в приложении.

> Модуль объявляется с помощью декоратора `@NgModule`. Этот декоратор принимает объект, который определяет метаданные модуля, такие как его имя, импортированные модули, объявленные компоненты, директивы и сервисы.

```typescript
import { NgModule } from '@angular/core'
import { BrowserModule } from '@angular/platform-browser'
import { AppComponent } from './app.component'

@NgModule({
	imports: [BrowserModule],
	declarations: [AppComponent],
	bootstrap: [AppComponent],
})
export class AppModule {}
```

### Свойства модуля в Angular, которые определяют различные аспекты приложения:

- `imports` : это свойство определяет список модулей, которые будут импортированы в текущий модуль. Это позволяет использовать функциональность других модулей в текущем модуле.
- `declarations` : это свойство определяет список компонентов, директив которые будут использоваться в текущем модуле. Это позволяет Angular знать о компонентах, которые должны быть доступны в текущем модуле.
- `entryComponents` : это свойство определяет список компонентов, которые должны быть созданы динамически. Это используется, когда компонент создается программно вместо того, чтобы быть включенным в шаблон.
- `schemas` : это свойство определяет схему, используемую для проверки шаблона компонента. Схема может быть `NO_ERRORS_SCHEMA`, которая отключает проверку схемы, или `CUSTOM_ELEMENTS_SCHEMA`, которая позволяет использовать пользовательские элементы в шаблоне.
- `providers` : это свойство определяет список сервисов, которые будут доступны в текущем модуле. Это позволяет использовать сервисы в компонентах и других сервисах в текущем модуле.
- `forRoot` : это метод, который используется для настройки модуля, который может быть импортирован в другие модули. Это позволяет передавать конфигурационные данные и сервисы в модуль при его импорте в другие модули. Например, `RouterModule.forRoot(routes)` используется для настройки маршрутизации в приложении.

### Angular CLI Builder

> `Angular CLI Builder` — это инструмент в Angular, который отвечает за выполнение различных задач сборки и разработки проектов. Он является частью Angular CLI (Command Line Interface) и позволяет вам настраивать и управлять процессом сборки приложения.

Основные особенности Angular CLI Builder:

- `Конфигурация`: Builders помогают настроить различные аспекты сборки, такие как компиляция приложений, тестирование, линтинг и оптимизация.

- `Плагины`: Вы можете использовать встроенные builders или создавать свои собственные, чтобы выполнять специфические задачи в процессе сборки.

- `Параметры сборки`: Angular CLI Builders позволяют определять различные параметры сборки, такие как флаги, пути к файлам и опции оптимизации.

- `Команды`: Builders могут быть вызваны через команды Angular CLI, такие как ng build, ng serve, ng test и т. д.

- `Расширяемость`: Developers могут создавать настраиваемые builders, чтобы адаптировать процесс сборки под специфические нужды проекта.

Использование

> Когда вы создаете проект с помощью `Angular CLI`, заданный `builder` автоматически настраивается, и вы можете его адаптировать в файле `angular.json`. Например, вы можете изменить настройки для `builder` на `@angular-devkit/build-angular:browser`, что отвечает за сборку веб-приложения.

```json
"projects": {
  "your-app": {
    "architect": {
      "build": {
        "builder": "@angular-devkit/build-angular:browser",
        "options": {
          // параметры сборки
        }
      }
    }
  }
}

```

### Дифференциальная загрузка Angular приложения

> Дифференциальная загрузка в Angular CLI имеет целью оптимизацию загрузки приложений для современных и устаревших браузеров, что позволяет улучшить производительность и уменьшить объем загружаемых ресурсов.
> Когда вы создаете приложение с помощью Angular CLI, дифференциальная загрузка включается автоматически, начиная с Angular версии 8. Angular CLI настраивает соответствующие скрипты для загрузки нужной версии приложения в зависимости от браузера пользователя.

Пример:

- В результате сборки приложения Angular вы увидите файлы .js, например:

  - main-es2015.js для современных браузеров.
  - main-es5.js для устаревших браузеров.

### Schema в Angular

> В Angular схема (или schema) обычно относится к описанию структуры и содержания данных, которые используются в ваших компонентах и приложениях. В контексте Angular можно выделить несколько типов схем:

Схемы компонентов:

- Описывают входные данные и выходные данные вашего компонента. Это может включать свойства, события и методы.

Схемы форм:

- Angular поддерживает реактивные и шаблонные формы, где схемы описывают, как данные должны быть валидированы и структурированы.

Схемы метаданных:

- Это информация о том, как Angular должен обрабатывать ваш компонент или другой элемент, включая декораторы, такие как @Component и @Directive.

- Схемы для маршрутизации:
  Описывают, как различные маршруты в приложении ссылаются друг на друга и какие компоненты должны загружаться по определенным URL.

### Schematics

Интерфейс командной строки Schematics в Angular — это инструмент, используемый для генерации и управления кодом в приложениях Angular. Он позволяет разработчикам создавать новые компоненты, сервисы, модули и другие элементы, используя предопределенные шаблоны

```npm
ng generate component my-component
```

### Schematics collection

В Angular коллекция (или Schematics collection) — это набор схем (schematics), которые организованы в единый пакет для облегчения генерации кода и выполнения различных задач в проектах Angular. Коллекции могут содержать различные схемы для создания компонентов, сервисов, модулей и других элементов, а также для выполнения обновлений кода. Коллекции могут быть добавлены в проекты Angular через `npm`, так что вы можете легко подключать и использовать сторонние коллекции, например, `@angular/material`.

### Создание своей Schematics

1. Сначала создайте новую библиотеку с помощью Angular CLI:

```npm
ng generate library my-library
```

2. Для создания схем вам понадобятся дополнительные зависимости:

```npm
npm install --save-dev @angular-devkit/schematics @schematics/angular

```

3. В корне вашей библиотеки создайте папку для схем, например /schematics.
4. В папке с схемами создайте файл `collection.json`, который будет описывать ваши схемы. Пример:

```json
{
	"schematics": {
		"my-schematic": {
			"description": "Описание вашей схемы",
			"path": "./my-schematic/index",
			"schema": "./my-schematic/schema.json"
		}
	}
}
```

5. Создайте подкаталог для вашей схемы и добавьте в него файл `schema.json`, где определите параметры вашего шаблона. Например:

```json
{
	"$schema": "http://json.schemastore.org/angular-cli",
	"id": "MySchematic",
	"title": "My Schematic",
	"type": "object",
	"properties": {
		"name": {
			"type": "string",
			"description": "Имя создаваемого компонента"
		}
	},
	"required": ["name"]
}
```

6. Создайте файл index.ts в папке вашей схемы, чтобы реализовать логику. Пример:

```typescript
import { Rule, SchematicContext, Tree } from '@angular-devkit/schematics'

export function mySchematic(options: any): Rule {
	return (tree: Tree, _context: SchematicContext) => {
		// Ваша логика для генерации файлов
		const { name } = options
		tree.create(`${name}.component.ts`, `export class ${name}Component {}`)
		return tree
	}
}
```

7. В package.json вашей библиотеки добавьте путь к коллекции:

```json
"schematics": "./schematics/collection.json"
```

8. Теперь вы можете тестировать вашу схему локально. Используйте команду:

```npm
ng generate my-library:my-schematic --name=my-component
```

### Что такое Angular lib?

> `Angular Library` (или Angular Lib) — это модульная структура, разработанная для создания переиспользуемых компонентов, директив, сервисов и другой логики, которые могут быть использованы в различных приложениях на Angular.

[Вернуться к началу статьи](#angular)

---

## Directives. Types of directives

> Директивы используются для изменения внешнего вида или поведения элемента DOM.
> Директива представляет класс с директивными метаданными. В TypeScript для прикрепления метаданных к классу применяется декоратор `@Directive`.

В Angular есть три типа директив:

- `Компоненты`: компонент по сути также является директивой, а декоратор `@Component` расширяет возможности декоратора `@Directive` с помощью добавления функционала по работе с шаблонами.
- `Собственные`: Директива - это обычный класс на TS, к которому применяется декоратор Directive, соответственно нам надо импортировать эту директиву из "angular/core". При применении декоратора @Directive необходимо определить селектор CSS, с которым будет ассоциирована директива. Селектор CSS для атрибута должен определяться в квадратных скобках. Надо подключить директиву в AppModule.

- `Структурные`: они изменяют структуру DOM с помощью добавления, изменения или удаления элементов html. Например, это директивы `ngFor` и `ngIf`.
  Директива `ngIf` позволяет удалить или, наоборот, добавить элемент при определенном условии.
  Директива `ngFor` позволяет перебрать в шаблоне элементы массива.
  С помощью директивы `ngSwitch` можно встроить в шаблон конструкцию `switch..case` и в зависимости от ее результата выполнения выводить тот или иной блок.

```HTML
  <div [ngSwitch]="car">
    <p *ngSwitchCase="'Audi'">This is Audi</p>
    <p *ngSwitchCase="'BMW'">This is BMW</p>
    <p *ngSwitchCase="'Mercedes'">This is Mercedes</p>
  </div>
```

- `Атрибутивные`: они изменяют поведение уже существующего элемента, к которому они применяются. Например, `ngModel`, `ngStyle`, `ngClass`.
  Директива `ngClass позволяет определить набор классов, которые будут применяться к элементу. В качестве значения она принимает набор классов в следующем виде:

```HTML
  <div [ngClass]="{'label': true}">Some text</div>
  <div [ngClass]="['label', 'label-small']">Some text</div>
```

> Директива `ngStyle` позволяет задать набор стилей, которые применяются к элементу. В качестве значения директива принимает js-объект, в котором ключи - названия свойств CSS.

```HTML
  <div [ngStyle]="elementStyles">Some text</div>
  <div [ngStyle]="{color: 5 < 10 ? 'green' ? 'red' }">Some text</div>
```

## Экспорт связанных директив.

1. Создайте компоненты и директивы:

```typescript
// DirectiveA
import { Directive, ElementRef, Renderer2 } from '@angular/core'

@Directive({
	selector: '[appDirectiveA]',
})
export class DirectiveA {
	constructor(el: ElementRef, renderer: Renderer2) {
		renderer.setStyle(el.nativeElement, 'color', 'blue') // Применение стилей или логики
	}
}

// DirectiveB
import { Directive, ElementRef, Renderer2 } from '@angular/core'

@Directive({
	selector: '[appDirectiveB]',
})
export class DirectiveB {
	constructor(el: ElementRef, renderer: Renderer2) {
		renderer.setStyle(el.nativeElement, 'font-weight', 'bold') // Применение стилей или логики
	}
}
```

2. Создайте модуль для директив:

```typescript
import { NgModule } from '@angular/core'
import { DirectiveA } from './directive-a.directive'
import { DirectiveB } from './directive-b.directive'

@NgModule({
	declarations: [DirectiveA, DirectiveB],
	exports: [DirectiveA, DirectiveB],
})
export class SharedDirectivesModule {}
```

3. Создайте основной модуль приложения и импортируйте модуль директив:

```typescript
import { NgModule } from '@angular/core'
import { BrowserModule } from '@angular/platform-browser'
import { AppComponent } from './app.component'
import { SharedDirectivesModule } from './shared-directives.module'

@NgModule({
	declarations: [AppComponent],
	imports: [
		BrowserModule,
		SharedDirectivesModule, // Импортируем модуль с директивами
	],
})
export class AppModule {}
```

4. Используйте директивы в шаблонах:

```HTML
<div appDirectiveA appDirectiveB>
  Этот текст будет синим и жирным.
</div>
```

## @Directive.providers

> Декоратор @Directive в Angular используется для создания директив, которые могут изменять поведение элементов в шаблоне. Параметр providers позволяет указать зависимости, которые будут доступны только для данной директивы. Это позволяет создавать экземпляры сервисов локально для каждой директивы, а не использовать глобальные экземпляры.

```typescript
// Service
import { Injectable } from '@angular/core'

@Injectable()
export class ExampleService {
	count = 0

	increment() {
		this.count++
	}
}

// Directive
import { Directive, HostListener } from '@angular/core'
import { ExampleService } from './example.service'

@Directive({
	selector: '[appExampleDirective]',
	providers: [ExampleService], // Локальный провайдер
})
export class ExampleDirective {
	constructor(private exampleService: ExampleService) {}

	@HostListener('click')
	onClick() {
		this.exampleService.increment()
		console.log(`Count: ${this.exampleService.count}`) // Локально отслеживаемое состояние
	}
}
```

`Важно помнить`

- Локальность: Использование `providers` создаст новый экземпляр сервиса для каждого элемента, который использует директиву, что не всегда нужно. Если вам нужен один общий экземпляр, лучше использовать провайдер в корневом модуле или в компоненте.

- Производительность: Если сервисы имеют тяжелую начальную загрузку, создание их экземпляров для каждой директивы может негативно сказаться на производительности приложения.

### @Component.viewProviders

> Декоратор `@Component` в Angular также имеет параметр `viewProviders`, который используется для определения сервисов, доступных только для дочерних компонентов и представлений (views) текущего компонента. Главное отличие между providers и viewProviders заключается в области видимости созданных сервисов.

```typescript
// Сервис
import { Injectable } from '@angular/core'

@Injectable()
export class ChildService {
	message = 'Hello from Child Service!'
}

// Родительский компонент
import { Component } from '@angular/core'
import { ChildService } from './child.service'

@Component({
	selector: 'app-parent',
	template: `<app-child></app-child>`,
	viewProviders: [ChildService], // Доступно только дочерним компонентам
})
export class ParentComponent {}

// Дочерний компонент
import { Component } from '@angular/core'
import { ChildService } from './child.service'

@Component({
	selector: 'app-child',
	template: `<p>{{ childService.message }}</p>`,
})
export class ChildComponent {
	constructor(public childService: ChildService) {}
}
```

[Вернуться к началу статьи](#angular)

---

## Data Binding

Angular поддерживает механизм привязки, благодаря которому различные части шаблона могут быть привязаны к некоторым значениям, определенным в компоненте.
В Angular есть четыре формы привязки данных:

- `Интерполяция`: привязка элемента DOM к значению компонента (односторонняя). В двойных фигурных скобках указывается выражение, к которому идет привязка:

```HTML
  {{ выражение }}
  <p>Hello, {{name}}</p>
  <p>{{'Hello,' + name}}</p>
```

- `Атрибуты`: привязка свойства элемента DOM к значению компонента (односторонняя).

```HTML
  <td [attr.colspan]="2 + 1">Table Cell Content</td>
  <p [class]="classes">Some text.</p>
  <div [style.width.%]="isHalf ? 50 : 100">Some text.</p>
```

- `Шаблонные переменные`: шаблонной переменной называется ссылка на HTML-элемент, директиву или компонент в пределах текущего представления. Инициализация и использование такой переменной осуществляется прямо в шаблоне. Объявление шаблонной переменной начинается с символа #.

```HTML
  <input type="text" #name />
  <p>Name: {{name.value}}</p>
```

- `Обработка событий`. Привязка метода компонента к событию в DOM (генерация события в DOM вызывает метод на компоненте)(односторонняя). Наиболее распространенные события:
  - click - нажатие кнопки мыши;
  - mouseover / mouseout - наведение/уход курсора мыши на/с элемента;
  - change - изменение состояние элемента, применяется к полям формы;
  - focus / blur - элемента получает / теряет фокус;
  - keydown / keyup - возникает, когда нажимается / отпускается клавиша. Для отслеживания нажатия Enter используется (keyup.enter).

```HTML
  <button (click)="showContacts()">Show Contacts List</button>
  <button on-click="showContacts()">Show Contacts List</button>
```

- `Двусторонняя привязка`: когда элемент DOM привязан к значению на компоненте, при этом изменения на одном конце привязки сразу приводят к изменениям на другом конце.

```HTML
  <contacts-item [(name)] = "contactPerson"></contacts-item>
  Запись [(name)] = "contactPerson" означает, что при изменении name в компоненте <contacts-item> его значение будет присвоено свойству contactPerson компонента, в который входит <contacts-item>.
  <input type="text" [(ngModel)]="contactPerson">
  При изменении поля его значение помещается в свойство contactPerson. [(NgModel)] находится в FormsModule, поэтому перед тем, как ее использовать, импортируйте FormsModule библиотеки @angular/forms.
```

[Вернуться к началу статьи](#angular)

---

## Directives Input, Output.

В Angular компоненты могут взаимодействовать друг с другом с помощью `Input()` и `Output()` свойств.

> Input свойство позволяет передавать данные из родительского компонента в дочерний компонент. Для этого в дочернем компоненте нужно определить свойство с помощью декоратора `@Input()`. Затем в родительском компоненте можно передать значение в это свойство, используя синтаксис привязки данных `[property]="value"`.

```typescript
// Дочерний компонент
import { Component, Input } from '@angular/core'

@Component({
	selector: 'app-child',
	template: '<p>{{ message }}</p>',
})
export class ChildComponent {
	@Input() message: string
}

// Родительский компонент
import { Component } from '@angular/core'

@Component({
	selector: 'app-parent',
	template: '<app-child [message]="parentMessage"></app-child>',
})
export class ParentComponent {
	parentMessage = 'Hello from parent'
}
// В этом примере мы передаем значение parentMessage из родительского компонента в свойство message дочернего компонента ChildComponent.
```

> Output свойство позволяет передавать данные из дочернего компонента в родительский компонент. Для этого в дочернем компоненте нужно определить событие с помощью декоратора `@Output()`. Затем в дочернем компоненте можно вызвать это событие, используя метод `emit()` и передавая данные в качестве аргумента. В родительском компоненте можно подписаться на это событие, используя синтаксис событий `(event)="handler($event)"`. Например:

```typescript
// Дочерний компонент
import { Component, EventEmitter, Output } from '@angular/core'

@Component({
	selector: 'app-child',
	template: '<button (click)="sendMessage()">Send message</button>',
})
export class ChildComponent {
	@Output() messageEvent = new EventEmitter<string>()

	sendMessage() {
		this.messageEvent.emit('Hello from child')
	}
}

// Родительский компонент
import { Component } from '@angular/core'

@Component({
	selector: 'app-parent',
	template: '<app-child (messageEvent)="receiveMessage($event)"></app-child><p>{{ message }}</p>',
})
export class ParentComponent {
	message: string

	receiveMessage($event) {
		this.message = $event
	}
}
// В этом примере мы создаем событие messageEvent в дочернем компоненте ChildComponent и вызываем его при нажатии на кнопку. Затем в родительском компоненте ParentComponent мы подписываемся на это событие и обрабатываем полученные данные в методе receiveMessage().
```

[Вернуться к началу статьи](#angular)

---

## Pipes

Фильтры позволяют провести некоторую предобработку перед выводом данных на страницу, например, отсортировать или как-то изменить набор данных.
Общий способ использования фильтров: `{{expression | filter}}`
Используя фильтры lowercase и uppercase, мы можем приводить содержимое к нижнему и верхнему регистру соответственно.
Наиболее часто используемые:

- date - преобразование даты;
- number - преобразование числа;
- uppercase / lowercase - приведение строкового значения в верхний / нижний регистр;
- slice - используется для ограничения вывода информации, в качестве параметров принимает начало и конец интервала отображаемых данных, применяется совместно с директивой \*ngFor.
- currency - форматирование валюты
- orderBy упорядочивает набор объектов по определенному свойству

```HTML
  <p>Transformed date: {{exampleDate | date : 'dd.MM.yyyy'}}</p>
  <p *ngFor="let user of list | slice : 0 : 1">{{user}}</p>
```

К одному значению допустимо применение нескольких фильтров.

```HTML
  {{someString | pipe1 | pipe2 | pipe3 | ... }}
```

Angular позволяет создавать свои собственные пайпы.

[Вернуться к началу статьи](#angular)

---

## Life cycle hooks

- `ngOnChanges`: вызывается до метода ngOnInit() при начальной установке свойств, которые связаны механизмом привязки, а также при любой их переустановке или изменении их значений. Данный метод в качестве параметра принимает объект класса SimpleChanges, который содержит предыдущие и текущие значения свойства.
- `ngOnInit`: вызывается один раз после установки свойств компонента, которые участвуют в привязке. Выполняет инициализацию компонента.
- `ngDoCheck`: вызывается при каждой проверке изменений свойств компонента сразу после методов ngOnChanges и ngOnInit
- `ngAfterContentInit`: вызывается один раз после метода ngDoCheck() после вставки содержимого в представление компонента кода html
- `ngAfterContentChecked`: вызывается фреймворком Angular при проверке изменений содержимого, которое добавляется в представление компонента. Вызывается после метода ngAfterContentInit() и после каждого последующего вызова метода ngDoCheck().
- `ngAfterViewInit`: вызывается фреймворком Angular после инициализации представления компонента, а также представлений дочерних компонентов. Вызывается только один раз сразу после первого вызова метода ngAfterContentChecked()
- `ngAfterViewChecked`: вызывается фреймворком Angular после проверки на изменения в представлении компонента, а также проверки представлений дочерних компонентов. Вызывается после первого вызова метода ngAfterViewInit() и после каждого последующего вызова ngAfterContentChecked()
- `ngOnDestroy`: вызывается перед тем, как фреймворк Angular удалит компонент.
  Каждый такой метод определен в отдельном интерфейсе, который называется по имени метода без префикса "ng".

[Вернуться к началу статьи](#angular)

---

## Services in Angular

Сервис — это класс, который используется для хранения состояния приложения или иных данных, которые в последующем могут быть использованы компонентами, директивами или другими сервисами. Объявлению класса сервиса предшествует декоратор `@Injectable()`.
Angular сервисы существуют в приложении в пределах свой области видимости в единственном экземпляре, что позволяет использовать их для взаимодействия компонентов и длительного хранения данных.

[Вернуться к началу статьи](#angular)

---

## Modules in Angular. Lazy loading.

Angular модуль представляет собой класс, который предваряется декоратором `@NgModule()` и используется для конфигурации Injector организации взаимосвязанных компонентов, директив и фильтров.
Angular приложение имеет модульную архитектуру и состоит, по крайней мере, из одного корневого модуля, который отвечает за загрузку приложения.
В больших и сложных приложениях модули используются для структурирования кода по определенному признаку. Так, по назначению модуль может быть:

- корневой;
- функциональный;
- маршрутизации;
- поставки сервисов и других внешних зависимостей.

`Ленивая загрузка (Lazy loading)` - это техника, при которой вы загружаете часть веб-страницы в более поздний момент времени, когда эта часть действительно необходима.
Первое, что вам нужно сделать, прежде чем реализовывать ленивую загрузку, это найти и разделить приложения на более мелкие модули. Убедитесь, что в основной модуль добавлен только необходимый функционал, а затем разместите остальные части приложения в его внутренних модулях.

[Вернуться к началу статьи](#angular)

---

## Observable vs promise.

`Promise` выполниться всегда(с ошибкой или успешно).
`Observable` — на него нужно обязательно подписаться.
`Observable` предпочтительнее `Promise`, поскольку он включает в себя функции Promise и имеет больший функционал. С Observable не имеет значения, хотите ли вы обрабатывать 0, 1 или несколько событий. Вы можете использовать один и тот же API. Observable также имеет преимущество перед Promise в том, что запрос может быть отменен. Если результат HTTP-запроса на сервер или какая-либо другая дорогостоящая асинхронная операция больше не требуется, Observable позволяет отменить подписку, а Promise в конечном итоге вызовет успешный или неудачный обратный вызов даже если результат вам уже не требуется.

[Вернуться к началу статьи](#angular)

---

## Dynamic elements

Вместо прямой работы с DOM-элементом Angular предоставляет следующие абстракции — `Renderer, TemplateRef, ElementRef и ViewContainerRef`. С помощью них можно создавать динамический контент.

### Renderer

Используется в основном для манипуляций над уже существующими элементами, например для изменения стилей элемента, атрибутов и параметров элемента.
Методы Renderer:

- Позволяет создать элемент DOM и опционально указать для него пространство имен.

```typescript
  createElement(name: string, namespace?: string): any

  let inputElement = this.renderer.createElement('input');
```

- Используются для вставки/удаления созданных или существующих элементов в DOM.

```typescript
  appendChild(parent: any, newChild: any): void
  insertBefore(parent: any, newChild: any, refChild: any): void
  removeChild(parent: any, oldChild: any): void

  let inputElement = this.renderer.createElement('input');
  this.renderer.appendChild(parent, inputElement);
```

- Используются для изменения атрибутов или параметров DOM-элемента, например, для установки значения checkbox.

```typescript
  setAttribute(el: any, name: string, value: string, namespace?: string): void
  removeAttribute(el: any, name: string, namespace?: string): void
  setProperty(el: any, name: string, value: any): void

  this.renderer.setAttribute(inputElement, 'value', 'Hello from renderer'); this.renderer.setProperty(inputElement, 'checked', true);
```

- Создает текстовый DOM-элемент, который можно добавит как дочерний в нужный элемент.

```typescript
  createText(value: string): any

  let buttonElement = this.renderer.createElement('button');
  const text = this.renderer.createText('Text');
  this.renderer.appendChild(buttonElement, text);
```

- Устанавливает или удаляет класс для DOM-элемента.

```TypeScript
  addClass(el: any, name: string): void
  removeClass(el: any, name: string): void

  this.renderer.addClass(buttonElement, 'btn-large');
```

> Это далеко не все, что предоставляет Renderer, но, даже используя указанные методы уже можно динамически создавать и изменять элементы DOM.

### Доступ к элементу через DI

> Данный способ довольно часто используется при создании собственных директив. Для того чтобы получить доступ к элементу (контейнеру) директивы, надо добавить в конструктор директивы приватную переменную с типом `ElementRef`.

> ![Some directive](./images/elementRef.png)

> Для поиска элементов в DOM ангуляр предоставляет ряд декораторов — `@ViewChild/@ViewChildren` и `@ViewChildren/@ContentChildren`. Директива @ViewChild отличается от @ViewChildren тем, что первая всегда вернет вам только один элемент, в то время как вторая позволяет вам находить несколько элементов, возвращая вам объект типа `QueryList`.

```typescript
import { Component, ViewChild, ElementRef } from '@angular/core'

@Component({
	selector: 'app-my-component',
	template: `<div #myElement>Hello World</div>`,
})
export class MyComponent {
	@ViewChild('myElement') myElement!: ElementRef

	ngAfterViewInit() {
		console.log(this.myElement.nativeElement) // Доступ к элементу
	}
}
```

> `QueryList` представляет из себя итерируемый интерфейс, а также позволяет подписываться на изменение элементов через механизм Observable. Декораторы @ViewChildren и @ContentChildren необходимо использовать в обработчике ngAfterViewInit жизненного цикла компонента, так как раньше QuryList просто будет не определен.

> Пара директив @ViewChildren/@ContentChildren ведет себя аналогичным образом и отличается от связки @ViewChild/@ViewChildren только тем, что @ViewChildren ищет элементы просто в DOM-дереве, в то время как @ViewChild ищет элементы в ShadowDom.

```TypeScript
@ViewChild('[query params]', { read: [referenceType], descendants: boolean });
```

- `query params` – элемент который ищем. Может быть, как имя шаблона, html элемент или компонент/директива.
- `descendants` – определяет искать элемент только среди прямых потомков или смотреть глубже.
- `read` — указание типа возвращаемого элемента.

> При объявлении @ViewChild вы можете указать третий параметр. Но не обязательно. В Angular, начиная с версии 8, при использовании @ViewChild вы можете указать статический флаг, но это не обязательно.

- `static: true`: это означает, что Angular должен получить ссылку на элемент во время инициализации компонента.
- `static: false`: это означает, что ссылка будет доступна только после выполнения ngAfterViewInit.

```typescript
@ViewChild('myElement', { static: true }) myElement!: ElementRef;

ngOnInit() {
  console.log(this.myElement.nativeElement); // Доступно здесь
}
```

Когда использовать статический флаг:

- Если вам не нужно ждать до `ngAfterViewInit` и вы хотите иметь доступ к элементу в `ngOnInit`, используйте `{ static: true }`.
- Если элемент создается или изменяется только после полной инициализации представления (например, в случае `*ngIf`, `*ngFor`), лучше использовать `{ static: false }`.

> Обычно указание данного параметра не является необходимым, так как ангуляр довольно сообразителен и, если вы ищете шаблон, он вернет вам TemplateRef, если вы ищете html элемент, ангуляр вернет вам ElementRef. Но в некоторых случая, например, когда вам надо получить ViewContainerRef, вам придётся указать тип возвращаемого элемента.

> В Angular вы можете использовать `@ViewChild` и `@ContentChild` для объявления шаблонных переменных и получения ссылок на элементы и компоненты.

Пример с `@ViewChild` и элементами внутри цикла:

```typescript
import { Component, AfterViewInit, ViewChildren, QueryList, ElementRef } from '@angular/core'

@Component({
	selector: 'app-my-component',
	template: `
		<div *ngFor="let item of items; let i = index" #itemElement>Item {{ i + 1 }}: {{ item }}</div>
		<button (click)="logItems()">Log Items</button>
	`,
})
export class MyComponent implements AfterViewInit {
	@ViewChildren('itemElement') itemElements!: QueryList<ElementRef>
	items = ['Apple', 'Banana', 'Cherry']

	ngAfterViewInit() {
		console.log(this.itemElements) // Список всех элементов
	}

	logItems() {
		this.itemElements.forEach(el => {
			console.log(el.nativeElement.innerText) // Логгируем текст каждого элемента
		})
	}
}
```

Пример с @ContentChild:

```typescript
import { Component, AfterContentInit, ContentChild, ElementRef } from '@angular/core'

@Component({
	selector: 'app-content',
	template: `<ng-content></ng-content>`,
})
export class ContentComponent implements AfterContentInit {
	@ContentChild('contentElement') contentElement!: ElementRef

	ngAfterContentInit() {
		console.log(this.contentElement.nativeElement.innerText) // Доступ к элементу
	}
}

@Component({
	selector: 'app-parent',
	template: `
		<app-content>
			<div #contentElement>Inserted Content</div>
		</app-content>
	`,
})
export class ParentComponent {}
```

Работа с элементами внутри циклов:

> Если вам нужно получить доступ к нескольким элементам, которые создаются в цикле (например, с помощью `*ngFor`), используйте `@ViewChildren` и `QueryList` для работы с этими элементами.

Кратко о @ViewChild и @ContentChild:

- `@ViewChild` используется для получения доступа к элементам и компонентам внутри собственного шаблона компонента.
- `@ContentChild` позволяет получать доступ к элементам внутри вставленного контента, используемого с `<ng-content>`.

### TemplateRef

> Ангуляр предоставляет свою нотацию описания шаблонов, а также позволяет манипулировать шаблоном и его содержимым. С этой абстракцией вы могли познакомиться, если создавали свои собственные структурные директивы наподобие ngIf и ngFor. Для доступа к шаблону мы воспользуемся типом TemplateRef — это ссылка на элемент ng-template в вашем компоненте или директиве.

### ViewContainerRef

> `ViewContainerRef` представляет собой ссылку на контейнер компонента или директивы и, кроме доступа к элементу, позволяет создавать два типа View — Host Views (View элементы, создаваемые на основе компонентов) и Embedded Views (View элементы, создаваемые на основе готовых шаблонов). Все создаваемые элементы имеют базовый тип View, который является основным строительным блоком для Angular приложений и представляет собой сгруппированные DOM-элементы, с которыми ангуляр работает как с единым целым и позволяет привязывать эту группу к Change Detection механизму.

ViewContainerRef методы:

- `ViewContainerRef.createEmbeddedView` : это метод в Angular, который позволяет создавать встроенные представления (embedded views) с использованием шаблонов, определенных в `ng-template`. Это полезно, когда вы хотите динамически создавать интерфейс на основе определенных условий или данных.

Основные моменты:

- `Embedded Views`:

  - Встроенные представления создаются из шаблонов (например, через `ng-template`).
  - Они могут включать в себя динамические данные и быть повторно использованы в разных местах.

- Использование `ViewContainerRef`:
  - `ViewContainerRef` представляет контейнер, в который можно вставлять представления.
  - С помощью `createEmbeddedView` вы вставляете встроенное представление в контейнер.

```TypeScript
  createEmbeddedView(templateRef: TemplateRef, context?: C, index?: number): EmbeddedViewRef
```

```html
<ng-template #myTemplate let-name="name">
	<p>Hello, {{ name }}!</p>
</ng-template>
```

```typescript
import { Component, ViewChild, TemplateRef, ViewContainerRef } from '@angular/core'

@Component({
	selector: 'app-my-component',
	template: `
		<ng-template #myTemplate let-name="name">
			<p>Hello, {{ name }}!</p>
		</ng-template>
		<button (click)="createView()">Create View</button>
	`,
})
export class MyComponent {
	@ViewChild('myTemplate') myTemplate!: TemplateRef<any>

	constructor(private viewContainerRef: ViewContainerRef) {}

	createView() {
		const embeddedView = this.viewContainerRef.createEmbeddedView(this.myTemplate, {
			// Передаем данные в контекст
			name: 'User',
		})
	}
}
```

- `ViewContainerRef.createComponent` : Создает View элемент на основе экземпляра компонента и вставляет его в DOM, возвращая нам указатель на созданный компонент. Для создания элемента необходимо сначала получить фабрику компонента и инжектор.

```TypeScript
  createComponent(componentFactory: ComponentFactory, index?: number, injector?: Injector, projectableNodes?: any[][], ngModule?: NgModuleRef): ComponentRef
```

- `ViewContainerRef.clear` - Удаляет все View элементы в контейнере

```TypeScript
  clear(): void
```

- `ViewContainerRef.insert` : Вставляет View-элемент, в заданную позицию контейнера

```TypeScript
  insert(viewRef: ViewRef, index?: number): ViewRef
```

- `ViewContainerRef.remove` : Удаляет View-элемент по указанному индексу. Если индекс не задан, будет удален последний View-элемент.

```TypeScript
  remove(index?: number): void
```

- `ViewContainerRef.destroy` : Удаляет View-элемент из DOM

```TypeScript
  destroy (index?: number): ViewRef
```

### Optional injectors in Embedded Views

> В Angular `Optional injectors in embedded views` позволяет вам использовать различные инжекторы для внедрения зависимостей в встроенные представления (embedded views). Это особенно полезно, когда вы хотите, чтобы ваше встроенное представление могло получать определенные зависимости, не полагаясь на стандартный инжектор компонента.

#### Зачем это нужно?

> Когда вы создаете динамическое встроенное представление с помощью createEmbeddedView, вы можете передать ему собственный инжектор, который может быть `опциональным`. Это значит, что представление может иметь доступ к различным сервисам или данным, которые могут не быть доступны в стандартном контексте инжектора.

#### Как это работает?

> Вы создаете встроенное представление с использованием опциональных инжекторов, передавая специальный объект, который описывает, какие зависимости нужно внедрить. Если указанные зависимости недоступны, вместо этого ничего не будет внедрено, и приложение не упадет.

Пример использования:

1. Создайте сервис:

```typescript
import { Injectable } from '@angular/core'

@Injectable({ providedIn: 'root' })
export class MyService {
	getMessage() {
		return 'Hello from MyService!'
	}
}
```

2. Создайте компонент:

```typescript
import { Component, ViewChild, TemplateRef, ViewContainerRef, Injector } from '@angular/core'
import { MyService } from './my.service'

@Component({
	selector: 'app-my-component',
	template: `
		<ng-template #myTemplate let-message="message">
			<p>{{ message }}</p>
		</ng-template>
		<button (click)="createView()">Create View</button>
	`,
})
export class MyComponent {
	@ViewChild('myTemplate') myTemplate!: TemplateRef<any>

	constructor(private viewContainerRef: ViewContainerRef, private injector: Injector) {}

	createView() {
		const service = this.injector.get(MyService, null) // Опциональное получение сервиса
		const message = service ? service.getMessage() : 'Service is not available.'

		this.viewContainerRef.createEmbeddedView(this.myTemplate, {
			message: message,
		})
	}
}
```

[Вернуться к началу статьи](#angular)

---

## Dependency Injection

## Dependency Injection в Angular. Способы объявления. Di токены. Декораторы @SkipSelf, @Host, @Optional.

`Dependency Injection (DI)` - шаблон проектирования, который упрощает создание веб-приложений и ограничивает тесную связь. Самый простой пример DI в Angular - это использованием компонентом сервиса, чаще всего для получения данных.
Все сервисы регистрируются Injector-ом, который является частью механизма DI в Angular. Возможные значения свойства providedIn:

- 'root' - экземпляр сервиса будет создан на уровне приложения в корневом инжекторе;
- 'platform' - сервис будет инициализирован в инжекторе платформы;
- 'any' - для каждого асинхронно загружаемого модуля будет создан свой экземпляр сервиса, все остальные модули имеют собственный один на всех экземпляр.

Самый главный - root injector. Он регистрирует все сервисы, которые определяются на уровне модулей. Дочерние injector-ы создаются в том случае, если есть хотя бы один сервис, который определен только в пределах компонента.

```TypeScript
  @Injectable({providedIn: 'root'})
```

Когда компоненту требуется сервис, то его поиск начинается с самого нижнего injector-а и далее вверх по иерархии, то есть сначала проверяется уровень самого компонента.
Для создания injection token, по которому injector идентифицирует запрашиваемый сервис, используется класс InjectionToken, конструктор которого в качестве первого параметра принимает строковое описание, а в качестве второго - объект с дополнительной конфигурацией (по умолчанию undefined).
В конфигурации можно указать только свойства providedIn и factory. Свойство factory должно определять функцию, которая возвращает значение для создаваемого injection token.

- `@SkipSelf()` позволяет пропустить инжектор текущего уровня и начать поиск зависимости со следующего далее по иерархии инжектора.
- `@Host()` обозначает текущий уровень как последний при поиске зависимости, относительно которой он применяется. Часто @Host() используется совместно с декоратором
- `@Optional()` задает null в качестве значения внешней зависимости, если она не доступна на текущем уровне или вовсе отсутствует, и не генерирует исключение.

[Вернуться к началу статьи](#angular)

---

## Injection Token

В Angular, `Injection Token` - это специальный тип данных, который представляет собой объект, используемый для инжектирования зависимостей в Angular приложениях. Injection Token определяет, каким образом Angular должен проводить внедрение зависимостей для определенного провайдера сервиса или объекта.

- Пример :

```ts
import { Injectable, InjectionToken, Inject } from '@angular/core'

// Создаем Injection Token
export const API_URL = new InjectionToken<string>('ApiUrl')

// Создаем сервис, который будет использовать Injection Token
@Injectable()
export class ApiService {
	constructor(@Inject(API_URL) private apiUrl: string) {}

	get(endpoint: string) {
		return fetch(`${this.apiUrl}/${endpoint}`).then(response => response.json())
	}
}
```

- Пример :

```ts
type PluginEventKeys = 'OPEN' | 'CLOSE' | 'CHANGE' | 'DEFAULT'

type PluginEvent = {
	[key in PluginEventKeys]: string
}

export type { PluginEvent }

/////////////////////////////////////////////////////

import { PluginEvent } from './types'

const EVENTS: PluginEvent = {
	OPEN: 'open',
	CLOSE: 'close',
	CHANGE: 'change',
	DEFAULT: '',
}

export { EVENTS }

/////////////////////////////////////////////////////

import { InjectionToken } from '@angular/core'
import { PluginEvent } from '../types'
import { EVENTS } from '../consts'

// Создаем Injection Token
const EVENT_COMPARISON_TOKEN = new InjectionToken<PluginEvent>('Plugin event', {
	factory: () => EVENTS,
})

export { EVENT_COMPARISON_TOKEN }
```

[Вернуться к началу статьи](#angular)

---

## Routing in Angular.

```TypeScript
// app.module.ts
// I
import { RouterModule } from '@angular/router'

@NgModule({
  imports: [
      // II
    RouterModule.forRoot([{
            path: 'welcome',
            component: WelcomeComponent
        }, {
            path: '',
            redirectTo: 'welcome',
            pathMatch: 'full'
        }, {
            path: '**',
            component: PageNotFoundComponent
        }
    ]),

/// III (index.html)
```

`Свойства Routes:`

- `path` - путь для маршрута
- `component` - компонент для URL
- `pathMatch` - задает соответствие URL свойству PATH ('full', 'prefix'); свойство обязательно при наличии redirectTo
- `redirectTo` - редирект на другой URL
- `children` - для задания дочерних маршрутов, которые отображают дополнительные компоненты во вложенных элементах router-outlet, содержащихся в шаблоне компонента активации
- `outlet` - для поддержки множественных компонентов outlet
- `resolve` - определяет действия, которые должны быть совершены перед активацией маршрута
- `canActive` - управляем активацией маршрута
- `canActiveChild` - управляем активацией дочернего маршрута
- `canDeactivate` - управляем тем, когда маршрут может деактивироваться для активации нового маршрута
- `loadCildren` - для настройки модуля, который загружается только в случае необходимости
- `canLoad` - загрузка модулей по требованию

`Директивы RouterOutlet.`

Именно корневой компонент обеспечивает навигацию между разными компонентами. RouterOutlet - директива (<router-outlet>) станет заполнителем, где роутер отобразит view (при этом все предыдущие компоненты будут удалены).

`Именованные элементы router-outlet.`

`<router-outlet></router-outlet>` может быть несколько. Отсюда следует, что по одному маршруту можно вывести несколько компонентов, загрузив их в разные `router-outlet`.
Чтобы отличать элементы router-outlet используется атрибут `name`. `<router-outlet></router-outlet>` без атрибута `name` является первичным, что равносильно `outlet: "primary"`.

```HTML
  <div>
    <router-outlet name="left"></router-outlet>
  </div>
  <div>
    <router-outlet name="right"></router-outlet>
  </div>
```

```TypeScript
let routing = RouterModule.forChild([
    {
        path: "",
        component: TestComponent,
        children: [
            {
                path: "",
                children: [
                    // свойство outlet используется для назначения router-outlet
                    { outlet: "primary", path: "", component: FirstComponent, },
                    { outlet: "left", path: "", component: SecondComponent, },
                    { outlet: "right", path: "", component: SecondComponent, },
                ]
            },
```

[Вернуться к началу статьи](#angular)

---

## ng-template, ngTemplateOutlet, ng-container, ng-content

Директивы `ng-template` и связанная `ngTemplateOutlet` очень мощные инструменты Angular, которые часто используются с `ng-container`.

### Angular директива ng-template

`ng-template` директива 'отрисовывает' Angular шаблон: это означает, что содержимое этого тега будет содержать часть шаблона, которая затем может быть использована вместе с другими шаблонами для формирования окончательного шаблона компонента. Директива `ng-template` используется под капотом в `ngIf`, `ngFor` и `ngSwitch` директивах.

```TypeScript
  @Component({
    selector: 'app-root',
    template: `
          <ng-template>
              <button class="tab-button"
                      (click)="login()">{{loginText}}</button>
              <button class="tab-button"
                      (click)="signUp()">{{signUpText}}</button>
          </ng-template>
    `})
  export class AppComponent {
    public loginText = 'Login';
    public signUpText = 'Sign Up';
    public lessons = ['Lesson 1', 'Lessons 2'];

    public login(): void {
          console.log('Login');
      }

    public signUp(): void {
          console.log('Sign Up');
      }
  }
```

### ВАЖНО!!!

> Изначально ng-template ничего не рендерит, мы просто определяем шаблон, но пока не используем его

### ng-template директива и ngIf

```HTML
  <div class="lessons-list" *ngIf="lessons else loading">
      ...
  </div>

  <ng-template #loading>
      <div>Loading...</div>
  </ng-template>
```

Очень частый случай: мы показываем альтернативный шаблон `loading` пока данные не будут получены с бэка. Как вы видите условие `else` указывает на шаблон, который имеет имя `loading`. Имя привязано через переменную шаблона `#loading`.

Помимо шаблона для `else`, использование `ngIf` также неявно создает второй `ng-template`.

```HTML
  <ng-template [ngIf]="lessons" [ngIfElse]="loading">
      <div class="lessons-list">
          ...
      </div>
  </ng-template>

  <ng-template #loading>
      <div>Loading...</div>
  </ng-template>
```

`*ngIf` имеет более лаконичный синтаксис. Что же происходит под капотом `*ngIf`:

- элемент, к которому была применена структурная директива был перемещен в ng-template
- выражение `*ngIf` было разделено на две отдельные директивы `[ngIf]` и `[ngIfElse]` с использованием `Input` синтаксиса
  `ngFor` и `ngSwitch` работают схожим образом.

Отметьте, что мы не можем использовать несколько структурных директив на одном элементе.

### Директива ng-container

Директива `ng-container` позволяет применить структурную директиву к разделу страницы, не создавай при этом дополнительный элемент (тег).

Итак, чтобы не создавать дополнительный `div` мы можем воспользоваться директивой `ng-container` (в разметке тега `ng-container` вы не увидите) и уже на ней применить структурную директиву:

```HTML
  <ng-container *ngIf="lessons">
      <div class="lesson" *ngFor="let lesson of lessons">
          <div class="lesson-detail">
              {{ lesson | json }}
          </div>
      </div>
  </ng-container>
```

Есть еще важная черта директивы `ng-container`, она может предоставить заполнитель для инжектирования динамического шаблона на страницу.

### Создание динамических шаблонов с директивой ngTemplateOutlet

Возможность создавать ссылки на шаблоны и указывать в их другие директивы, такие как `ngIf` это только начало.
Мы также можем взять сам шаблон и создать его экземпляр где угодно на странице, используя `ngTemplateOutlet` директиву:

```HTML
  <ng-container *ngTemplateOutlet="loading"></ng-container>
```

Здесь мы используем `ng-container` и структурный директиву `ngTemplateOutlet` для создания шаблона `loading`, который мы определили выше при помощи переменной шаблона `#loading`.

### Контекст шаблона

Один вопрос насчет шаблона - что мы видим внутри него? Имеет ли шаблон свою собственную область видимости? Какие переменный может видеть шаблон?

Внутри тела `ng-template` мы имеем доступ к тому же контексту, который виден во внешнем шаблоне, например, переменной lessons (то есть `ng-template` экземпляр имеет доступ к тому же контексту, в которой он встроен).

Но каждый шаблон также может определить свой собственный набор входящих переменных! Фактически, каждый шаблон имеет связанный объект контекста, содержащий все входные переменные специфичный для шаблоны.

```TypeScript
  @Component({
    selector: 'app-root',
    template: `
      <ng-template #estimateTemplate let-lessonsCounter="estimate">
          <div> Approximately {{lessonsCounter}} lessons ...</div>
      </ng-template>

      <ng-container
          *ngTemplateOutlet="estimateTemplate; context: templateCtx"
      >
      </ng-container>
  `})
  export class AppComponent {

    public totalEstimate = 10;
    public templateCtx = {
          estimate: this.totalEstimate
      };

  }
```

Особенности:

- входящая переменная названа `lessonsCounter`, и определена в `ng-template` через префикс `let-`
- переменная `lessonsCounter` видна внутри `ng-template`, но не снаружи
- значение переменной `lessonsCounter` равно выражение, которое присвоено `let-lessonsCounter`
- это выражение берется по объекту контекста, который передан `ngTemplateOutlet` вместе с шаблоном
- объект контекста должен иметь свойство `estimate`, чтобы его значение отображалось внутри шаблона
- объект контекста передан `ngTemplateOutlet` через свойство context

Пример выше отрендерит:

```HTML
  Approximately 10 lessons ...
```

Отличный пример того как определять и создавать наши собственные шаблоны.

### Переменные шаблона

Декоратор `@ViewChild` позволяет нам получить доступ к дочернему компоненту из родительского компонента.

### Настраиваем компоненты с Частичными Шаблонами @Inputs

Возьмем таб контейнер и разрешим пользователям настраивать внешний вид кнопок вкладок (в контексте статьи автор просто передает через декоратор `Input` 'пользовательский' шаблон с кнопками дочернему компоненту; если его не передать будет использован дефолтный шаблон с кнопками).

Определим шаблон с кнопками в **родительском компоненте**:

```TypeScript
  @Component({
    selector: 'app-root',
    template: `
      <ng-template #customTabButtons>
          <div class="custom-class">
              <button class="tab-button" (click)="login()">
                  {{loginText}}
              </button>
              <button class="tab-button" (click)="signUp()">
                  {{signUpText}}
              </button>
          </div>
      </ng-template>
      <tab-container [headerTemplate]="customTabButtons"></tab-container>
  `})
  export class AppComponent implements OnInit {}
```

Затем в компоненте таб контейнера определим входящее свойство, котороя также является шаблоном с именем `headerTemplate`.

```TypeScript
  @Component({
      selector: 'tab-container',
      template: `

      <ng-template #defaultTabButtons>
        <div class="default-tab-buttons">
            ...
        </div>
      </ng-template>

      <ng-container
        *ngTemplateOutlet="headerTemplate ? headerTemplate : defaultTabButtons"
      >
      </ng-container>
  ... rest of tab container component ...
  `})
  export class TabContainerComponent {
      @Input() public headerTemplate: TemplateRef<any>;
  }
```

Пара вещей, которые стоит отметить:

- шаблон по умолчанию для кнопок назван `defaultTabButtons`
- этот шаблон будет использован, если входящее свойство `headerTemplate` не undefined
- если свойство определено, то пользовательский входящий шаблон переданные через `headerTemplate` будет использован для показа кнопок
- шаблон с кнопками создается внутри `ng-container` и с использованием `ngTemplateOutlet`

По сути мы будем использовать пользовательский шаблон, если он есть, или шаблон по умолчанию.

### Заключение

Корневые директивы ng-container, ng-template и ngTemplateOutlet объединяются вместе, чтобы позволить нам создавать высоко динамичные и настраиваемые компоненты.

[Вернуться к началу статьи](#angular)

---

## Organization of data sharing.

### Организация шаринга данных: Observable Data Services, ngstore.

`NgRx Store` (хранилище) представляет собой глобальное состояние Angular приложения и является одним большим объектом. В приложении может быть только одно хранилище. За работу с хранилищем отвечает отдельно устанавливаемый модуль @ngrx/store.
Хранилище в NgRx представлено сервисом Store и выполняет функции:

- хранение состояния приложения и предоставление к нему доступа;
- предоставление возможности обновить состояние через заранее определенные действия;
- регистрация функций, вызов которых будут осуществлен при любом изменении состояния.
  Формирование глобального состояния в NgRx Store происходит путем объединения более мелких состояний, которые возвращают зарегистрированные в приложении редюсеры. Делается это с использованием `ActionReducerMap<State>`.
  > ![NgRx Store](./images/NgRx_store.png)

[Вернуться к началу статьи](#angular)

---

## Redux. Flux pattern.

`Redux` — библиотека управления состоянием для приложений, написанных на JavaScript.Библиотека NgRx реализует принцип работы Redux для Angular приложений.
Цель достигается благодаря заложенным в библиотеке нескольким фундаментальным принципам:

- Наличие единственного источника данных о состоянии - хранилища (store);
- Доступно только для чтения, изменить ничего напрямую нельзя. Изменения возможны только при отправке action (действия).
- Действие (action) — это JavaScript-объект, который лаконично описывает суть изменения. Единственное требование к объекту действия — это наличие свойства type, значением которого обычно является строка.
- Создатели действий (action creators): функции, которые создают действия
- Reducer функция (чистые функции), которая получает действие и в соответствии с этим действием изменяет состояние хранилища
- Хранилище (store) — это объект, который:
  - Содержит состояние приложения;
  - Отображает состояние через getState();
  - Может обновлять состояние через dispatch();
  - Позволяет регистрироваться (или удаляться) в качестве слушателя изменения состояния через subscribe().

`Flux-архитектура` — архитектурный подход или набор шаблонов программирования для построения пользовательского интерфейса веб-приложений, сочетающийся с реактивным программированием и построенный на однонаправленных потоках данных. Flux является архитектурным решением.
Основной отличительной особенностью Flux является односторонняя направленность передачи данных между компонентами Flux-архитектуры. Архитектура накладывает ограничения на поток данных, в частности, исключая возможность обновления состояния компонентов самими собой.

В минимальном варианте Flux-архитектура может содержать три слоя, взаимодействующие по порядку:

- Actions (действия)
- Stores (хранилища)
- Views (представления)

Обычно между действиями и хранилищами добавляют Dispatcher (диспетчер).
Действия. (actions) — выражение событий (часто используются просто имена — строки). Диспетчеры передают действия нижележащим компонентам (хранилищам) по одному. Новое действие не передаётся пока предыдущее полностью не обработано компонентами. Действия поступают асинхронно, но их диспетчеризация является синхронным процессом. Кроме имени (name), действия могут иметь полезную нагрузку (payload), содержащую относящиеся к действию данные.
Диспетчер (dispatcher) предназначен для передачи действий хранилищам. В упрощённом варианте диспетчер может вообще не выделяться, как единственный на всё приложение.
Хранилища (store) является местом, где сосредоточено состояние (state) приложения. Остальные компоненты, согласно Flux, не имеют значимого состояния. Изменение состояния хранилища происходит строго на основе данных действия (чистая функция).
Представления (view) — компонент, обычно отвечающий за выдачу информации пользователю. Во Flux-архитектуре, которая может технически не касаться внутреннего устройства представлений вообще, это — конечная точка потоков данных.

[Вернуться к началу статьи](#angular)

---

## Observer pattern.

`Наблюдатель (Observer)` — поведенческий шаблон проектирования. Также известен как «подчинённые» (Dependents). Реализует у класса механизм, который позволяет объекту этого класса получать оповещения об изменении состояния других объектов и тем самым наблюдать за ними.
Классы, на события которых другие классы подписываются, называются субъектами (Subjects), а подписывающиеся классы называются наблюдателями (Observers).
Похожие шаблоны: «издатель-подписчик», «посредник», «одиночка».
Определяет зависимость типа один ко многим между объектами таким образом, что при изменении состояния одного объекта все зависящие от него оповещаются об этом событии.
При реализации шаблона «наблюдатель» обычно используются следующие классы:

1. Observable — интерфейс, определяющий методы для добавления, удаления и оповещения наблюдателей;
1. Observer — интерфейс, с помощью которого наблюдатель получает оповещение;
1. ConcreteObservable — конкретный класс, который реализует интерфейс Observable;
1. ConcreteObserver — конкретный класс, который реализует интерфейс Observer.

Шаблон «наблюдатель» применяется в тех случаях, когда система обладает следующими свойствами:

1. существует как минимум один объект, рассылающий сообщения;
2. имеется не менее одного получателя сообщений, причём их количество и состав могут изменяться во время работы приложения;
3. позволяет избежать сильного зацепления взаимодействующих классов.

[Вернуться к началу статьи](#angular)

---

## Assembly in Angular

## Как устроена сборка в Angular. (treeshake - при сборке выкидывает лишнее).

> од сборкой подразумевается процесс компиляции и компоновки исходного кода, результатом является готовое для разворачивания на web-сервере приложение. Для сборки приложения в Angular используется команда ng build модуля Angular CLI. По умолчанию результат сборки помещается в директорию /dist/{app}/browser, где {app} - имя текущего проекта. Для оптимизации процесса сборки, применительно к ng build используется флаг --prod.

Оптимизированная сборка включает в себя:

- AoT-компиляцию;
- активацию режима production путем вызова метода enableProdMode() в файле main.ts;
- объединение всех файлов в несколько больших;
- минификацию;
- удаление неиспользуемого кода.

> В режиме production приложение работает гораздо быстрее за счет отключения специфических для режима development проверок, например, за счет отключения двойного запуска механизма отслеживания изменений. `ng build` принимает множество параметров, самые распространенные из которых:

- watch - собирает приложение в режиме отслеживания изменений, что означает его пересборку при любом изменении исходных файлов;
- deploy-url - задает начало пути для файлов стилей и скриптов, запрашиваемых из файла index.html
- configuration - указывает конфигурацию сборки, описанную в angular.json; обычно новые конфигурации создаются для разных сред развертывания для возможности задания другого значения переменной environment.

> `Environment` файл `/src/environments/environment.ts` содержит переменную `environment`, которая используется для хранения и использования в приложении специфичных для окружения значений.
> Проксирование для перенаправления HTTP-запросов на другой адрес, в Angular предусмотрен механизм проксирования.
> Сначала необходимо в директории src создать файл proxy.conf.json следующего содержания. Описанное в файле правило указывает, что все запросы, которые начинаются с/, будут перенаправлены по адресу, указанному в свойстве target. Свойство secure задает протокол запроса: если равно true - https, если false — http.
> Теперь прокисрование будет применяться при запуске приложения с помощью команды ng serve.
> В proxy.conf.json может быть определено несколько правил.

### Различие jit и aot компиляции в angular.

> Для запуска в браузере приложение должно быть предварительно обработано компилятором Angular, который конвертирует код исходных файлов в исполняемый JavaScript.

Механизм Angular compile реализован в двух режимах:

1. JiT-компиляция (Just-in-TIme);
2. AoT-компиляция (Ahead-of-Time).

> В режиме `JiT` (по умолчанию) приложение компилируется в момент его запуска в браузере. Angular поочередно компилирует каждый компонент и только после этого начинает отображение пользователю интерфейса.
> При компиляции JiT, в машинный код преобразовывается не весь исходный код, а только та его часть, которая необходима для работы приложения в данный момент времени. Далее, если осуществляется вызов функции, которая еще не была преобразована в машинный код, сначала осуществляется ее преобразование, а потом она уже используется в месте вызова.
> Описанный подход позволяет значительно уменьшить использование ЦПУ и сделать приложение более быстрым за счет компиляции только того кода, который нужен в настоящий момент.

> В режиме `AoT` компиляция происходит в момент сборки приложения. При сборке приложения с флагом —prod AoT-компиляция используется по умолчанию.

Преимущества Angular AoT:

- Быстрая загрузка в браузере. Меньше времени тратится за счет того, что:
- Приложение компилируется до загрузки в браузер;
- В сборку не включается компилятор Angular, конечные файлы имеют меньший размер;
- Выполняется меньше AJAX-запросов на получение исходных HTML- и CSS-файлов, поскольку они включаются в строковом виде.
- Обнаружение ошибок при сборке. Имеется возможность исправить все ошибки до запуска приложения в режиме эксплуатации.
- Повышенная безопасность. Поскольку HTML- и CSS-файлы включаются в процессе Angular compile в файлы JavaScript, то нет возможности просмотреть шаблоны, что снижает риск осуществления атак.

> Компиляцию Angular AoT можно разделить на три стадии:

- Анализ. В процессе анализа формируются данные, необходимые для генерации кода. Это файлы определения типов _.d.ts и файлы, содержащие информацию о метаданных, указанных в декораторах _.metadata.json. Также процесс анализа включает в себя некоторую оптимизацию кода.
- Генерация кода. На этой стадии интерпретируются все файлы, сгенерированные на стадии анализа.
- Валидация. На стадии валидации компилятор шаблонов использует компилятор TypeScript для проверки правильности использования свойств и методов компонентов и сервисов в шаблонах.

> Как видно, AoT-компиляция имеет гораздо больше преимуществ перед JiT-компиляцией. Но сборка Angular AoT занимает гораздо больше времени. Поэтому рекомендуется при разработке использовать режим JiT, а для сборки версии и последующего ее развертывания — AoT.
> IVY
> Angular Ivy компилятор, который пришел на смену View Engine.

Преимущества Angular Ivy:

- Более быстрая сборка за счет того, что зависимые компоненты и директивы теперь не включаются в зависящий компонент, вместо этого в зависящем компоненте указываются ссылки на зависимости, Таким образом, при изменении одной из зависимостей нужно перекомпилировать только ее;
- Меньший размер файлов сборки из-за преобразования всех декораторов в статические методы класса;
- Меньший размер бандла. Компилятор Ivy был разработан для удаления частей Angular, которые не используются с помощью treeshaking, и для уменьшения количества кода, генерируемого для компонент Angular.
- Более быстрое тестирование. TestBed пересобирается только после изменений
- Усовершенствованная отладка;
- Улучшен байндинг стилей и CSS классов. С Ivy стили сливаются предсказуемо.
- Использование динамической загрузки.

> Ivy работает только с AoT-компиляцией. Для активации/деактивации Angular Ivy в уже созданном проекте, необходимо в файле tsconfig.app.json изменить значение параметра enableIvy.

---

## Virtual DOM

- Virtual DOM - это концепция, используемая во многих современных JavaScript-фреймворках, включая React и Vue.js. Она заключается в том, что браузерный DOM, который представляет собой иерархию элементов на странице, имитируется в памяти приложения в виде виртуального дерева.

- Когда происходят изменения в состоянии приложения, Virtual DOM сравнивает виртуальное дерево с предыдущей версией и определяет, какие изменения необходимо внести в реальный DOM. Затем только эти изменения применяются к реальному DOM, что позволяет избежать перерисовки всей страницы при каждом изменении состояния.

- Таким образом, Virtual DOM ускоряет процесс обновления страницы, и повышает производительность приложения. Кроме того, он упрощает процесс разработки, поскольку разработчикам не нужно беспокоиться о том, какие именно изменения произошли в DOM, а просто обновлять виртуальное дерево в соответствии с изменениями в состоянии приложения.

[Вернуться к началу статьи](#angular)

---

## trackBy

> `trackBy` - это опция, которая используется в Angular для оптимизации производительности при работе со списками данных.

> Когда Angular рендерит список данных, он может использовать trackBy для отслеживания изменений в элементах списка. Если изменения произошли только в одном элементе списка, Angular может обновить только этот элемент, а не перерисовывать весь список заново.

> trackBy принимает функцию, которая принимает два аргумента: индекс элемента в списке и сам элемент. Функция должна возвращать уникальный идентификатор элемента. Этот идентификатор используется Angular для отслеживания изменений в элементах списка.

```html
<ng-container *ngFor="let item of items; trackBy: trackByFn">
	<div>{{ item.name }}</div>
</ng-container>
```

```typescript
    trackByFn(index, item) { return item.id }
```

[Вернуться к началу статьи](#angular)

---

## Reactive Forms Angular

> Reactive Forms в Angular - это инструмент для создания форм, который использует реактивное программирование. Reactive Forms предоставляет более гибкий и мощный способ создания форм, чем Template-Driven Forms.

> Основным компонентом `Reactive Forms`является `FormGroup`, который представляет собой группу элементов управления формы. Каждый элемент управления представлен в `FormGroup` в виде `FormControl`. `FormControl` представляет собой отдельный элемент управления формы, такой как текстовое поле или флажок.

> `FormGroup` и `FormControl` предоставляют множество методов и свойств для работы с элементами управления формы. Например, `setValue` и `patchValue` используются для установки значения элемента управления, а `valueChanges` используется для получения потока значений элемента управления.

> `Reactive Forms` также позволяет создавать вложенные `FormGroup` и `FormControl`, что делает создание сложных форм более простым и понятным.

> `FormArray` - это класс в Reactive Forms в Angular, который представляет собой группу элементов управления формы. Он позволяет создавать массивы элементов управления и управлять ими в реактивном стиле.
> `FormArray` используется для создания форм, которые содержат несколько элементов одного типа, например, список контактов или список задач. Каждый элемент в FormArray является экземпляром FormControl, FormGroup или другого FormArray.
> `FormArray` имеет множество методов, которые позволяют добавлять, удалять и изменять элементы в массиве. Он также предоставляет методы для валидации и управления состоянием элементов массива.

Пример использования FormArray:

```typescript
import { Component } from '@angular/core'
import { FormArray, FormControl, FormGroup } from '@angular/forms'

@Component({
	selector: 'app-form-array-example',
	template: `
		<form [formGroup]="form">
			<div formArrayName="items">
				<div *ngFor="let item of items.controls; let i = index" [formGroupName]="i">
					<input formControlName="name" />
					<input formControlName="age" />
				</div>
			</div>
			<button (click)="addItem()">Add Item</button>
		</form>
	`,
})
export class FormArrayExampleComponent {
	form = new FormGroup({
		items: new FormArray([]),
	})

	get items(): FormArray {
		return this.form.get('items') as FormArray
	}

	addItem() {
		const item = new FormGroup({
			name: new FormControl(''),
			age: new FormControl(''),
		})
		this.items.push(item)
	}
}
// В этом примере мы создаем форму, которая содержит FormArray с именем items.
// Мы используем метод controls для получения массива элементов в FormArray и метод formGroupName для связывания каждого элемента с его соответствующим FormGroup.
// Метод addItem добавляет новый элемент в массив при нажатии на кнопку.
```

> Для использования `Reactive Forms` в Angular необходимо импортировать модуль `ReactiveFormsModule` и добавить его в список импортов в модуле приложения.

[Вернуться к началу статьи](#angular)

---

## Event Bus

В Angular `Event Bus` - это паттерн проектирования, который позволяет компонентам взаимодействовать друг с другом через отправку и прослушивание событий. Event Bus представляет собой глобальный шину событий, через которую компоненты могут обмениваться данными или уведомлениями, не имея прямой связи друг с другом.

Для создания `Event Bus` в Angular вы можете использовать сервис с помощью RxJS `Subject` или `BehaviorSubject`. Этот сервис будет служить в качестве посредника для отправки и прослушивания событий.

Пример простой реализации Event Bus с использованием RxJS Subject:

```ts
import { Injectable } from '@angular/core'
import { Subject } from 'rxjs'

@Injectable({
	providedIn: 'root',
})
export class EventBusService {
	private eventBus = new Subject<any>()

	emit(event: any) {
		this.eventBus.next(event)
	}

	on(eventType: any) {
		return this.eventBus.asObservable().pipe(filter((event: any) => event.type === eventType))
	}
}
```

- Еще пример :

```ts
export interface IEventBus {
	on<DetailType>(type: string, listener: (event: CustomEvent<DetailType>) => void): void
	once<DetailType>(type: string, listener: (event: CustomEvent<DetailType>) => void): void
	off<DetailType>(type: string, listener: (event: CustomEvent<DetailType>) => void): void
	emit<DetailType>(type: string, detail?: DetailType): void
}

////////////////////////////////////////////////////////

import { IEventBus } from '../interfaces'

/**
 * EventBus (Шина событий) служит для связи между микросервисами или микрофронтендами.
 * Event Bus - это механизм, который позволяет различным компонентам или сервисам обмениваться событиями или сообщениями асинхронно.
 */
export class EventBus implements IEventBus {
	private eventTarget: EventTarget

	constructor(description = '') {
		this.eventTarget = document.appendChild(document.createComment(description))
	}

	emit<T>(type: string, detail?: T): void {
		this.eventTarget.dispatchEvent(new CustomEvent(type, { detail }))
	}

	off<T>(type: string, listener: (event: CustomEvent<T>) => void): void {
		this.eventTarget.removeEventListener(type, listener as EventListener)
	}

	on<T>(type: string, listener: (event: CustomEvent<T>) => void): void {
		this.eventTarget.addEventListener(type, listener as EventListener)
	}

	once<T>(type: string, listener: (event: CustomEvent<T>) => void): void {
		this.eventTarget.addEventListener(type, listener as EventListener, {
			once: true,
		})
	}
}
```

[Вернуться к началу статьи](#angular)

---

## Security in angular

- ### Что произойдет, если вы используете тег скрипта внутри шаблона?
  > Если вы используете тег `<script>` внутри шаблона Angular, как правило, это не будет работать ожидаемым образом из-за специфики работы фреймворка Angular.

Вот почему это может быть проблемой:

1. `Проблемы безопасности`: Использование тега `<script>` в Angular-шаблоне может привести к уязвимостям XSS (межсайтового скриптинга). Angular по умолчанию выполняет санитизацию (очистку) потенциально опасного контента, такого как JavaScript, чтобы предотвратить такие атаки. Вставка сценариев напрямую может обойти эту защиту.

2. `Конфликт с Angular компиляцией`: Angular компилирует шаблоны, создавая свое собственное DOM-дерево и управляя им. Добавление скриптов вручную может нарушить этот процесс компиляции и привести к непредсказуемому поведению или ошибкам.

3. `Ухудшение производительности`: Выполнение JavaScript напрямую в шаблоне может отрицательно сказаться на производительности вашего приложения, поскольку это делает сложнее оптимизацию и управление ресурсами.

> Вместо использования тега `<script>` в шаблонах Angular рекомендуется использовать Angular-специфичные инструменты и возможности, такие как сервисы, директивы или интерполяция данных через двойные фигурные скобки `{{}}`, чтобы обеспечить безопасное и эффективное взаимодействие со скриптами и данными в вашем приложении.

- ### Как внедрить динамический скрипт в angular?

> Для внедрения динамического скрипта в Angular можно воспользоваться Angular сервисом Renderer2. Этот сервис позволяет добавлять элементы такие как `script` DOM динамически. Вот пример того, как можно внедрить динамический скрипт в Angular:

```TypeScript
import { Injectable, Renderer2, Inject } from '@angular/core';
import { DOCUMENT } from '@angular/common';

@Injectable({
  providedIn: 'root',
})
export class ScriptService {

  constructor(private renderer: Renderer2, @Inject(DOCUMENT) private document: Document) {}

  addScript(src: string): void {
    const script = this.renderer.createElement('script');
    script.src = src;
    this.renderer.appendChild(this.document.body, script);
  }
}
```

> Вызов метода добавления скрипта. Чтобы динамически добавить скрипт, вы можете вызвать метод addScript в вашем Angular компоненте или другом месте, где этот сервис доступен:

```typescript
import { Component, OnInit } from '@angular/core'

@Component({
	selector: 'app-your-component',
	templateUrl: './your-component.component.html',
	styleUrls: ['./your-component.component.css'],
})
export class YourComponent implements OnInit {
	constructor(private scriptService: ScriptService) {}

	ngOnInit(): void {
		this.loadScript()
	}

	loadScript() {
		this.scriptService.addScript('https://example.com/your-script.js')
	}
}
```

> Таким образом, Angular предоставляет инструменты для динамического добавления скриптов в ваше приложение с помощью безопасных и контролируемых методов, таких как использование Renderer2 и сервисов.

- ### Каковы наилучшие методы обеспечения безопасности в angular?
  > Angular предоставляет несколько встроенных механизмов безопасности для защиты приложений от распространенных уязвимостей. Ниже приведены некоторые из лучших методов обеспечения безопасности в Angular:

1. `Sanitization (Санитизация данных)`:

   - Angular автоматически санитизирует данные по умолчанию, чтобы предотвратить XSS-атаки (межсайтовый скриптинг). Для встраивания небезопасного HTML, CSS или URL можно использовать DomSanitizer.

2. `Content Security Policy (Политика безопасности контента)`:

   - Внедрение правильной CSP помогает предотвратить уязвимости, связанные со встраиванием скриптов из внешних источников. Заголовок `Content-Security-Policy` может быть установлен на стороне сервера.

3. `HTTP Interceptors (HTTP-перехватчики)`:

   - Используйте HTTP-перехватчики для проверки, фильтрации или изменения HTTP-запросов и ответов. Это может быть полезно для добавления токенов безопасности или проверки их на каждом запросе.

4. `JWT (JSON Web Tokens)`:

   - Используйте JWT для аутентификации и авторизации пользователей. Angular имеет хорошую интеграцию с механизмами для работы с токенами.

5. `Angular Guards (Angular защитники)`:

   - Angular Guards (CanActivate, CanLoad, CanDeactivate, CanActivateChild) позволяют контролировать доступ к определенным маршрутам или функциональности на основе прав и условий доступа.

6. `Input Validation (Проверка ввода)`:

   - Всегда проверяйте и валидируйте входные данные, поступающие от пользователей, как на стороне клиента, так и на сервере.

7. `Security Headers (Заголовки безопасности)`:

   - Управление заголовками безопасности HTTP (например, X-Frame-Options, X-XSS-Protection, Strict-Transport-Security) помогает предотвратить атаки, такие как clickjacking или XSS.

8. `CSRF Protection (Защита от CSRF)`:

   - Angular помогает защититься от атак типа CSRF с помощью механизма XSRF-токенов, предоставляемого Angular HTTPClientModule.

9. `Актуальные библиотеки и расширения`:

   - Всегда используйте актуальные версии Angular и его зависимостей, чтобы получить последние улучшения безопасности.

10. `Обработка ошибок`:
    - Обработка ошибок на клиентской и серверной сторонах поможет предотвратить утечку информации и обнаружить попытки взлома.

> Эти методы помогут обеспечить безопасность вашего Angular-приложения на различных уровнях, начиная от защиты от атак XSS и CSRF до контроля доступа и защиты ваших ресурсов и данных.

- ### Что такое модель безопасности Angular для предотвращения XSS-атак?
  > Модель безопасности Angular для предотвращения XSS-атак включает в себя несколько уровней защиты, цель которых - предотвратить внедрение вредоносного кода на страницу и обеспечить безопасное отображение пользовательского контента. Вот основные аспекты модели безопасности Angular для борьбы с XSS-атаками:

1. `Санитизация данных`: Angular включает встроенный механизм санитизации, который автоматически санитизирует небезопасные значения, чтобы предотвратить XSS-атаки. Это означает, что необработанные данные, содержащие потенциально вредоносный код, будут предварительно обработаны и безопасно отображены.

2. `DomSanitizer`: Angular предоставляет DomSanitizer для явной санитизации данных перед вставкой их в DOM. Этот сервис используется для обработки небезопасного HTML, CSS или URL, обеспечивая безопасное встраивание данных из потенциально небезопасных источников.

3. `Angular Interpolation и Property Binding`: Angular по умолчанию производит экранирование данных, вставляемых через интерполяцию или связывание свойств. Это помогает предотвратить внедрение кода через шаблоны и динамически формируемый контент.

4. `Безопасные пайпы`: Angular предлагает безопасные пайпы (safe pipes) для обработки небезопасных данных перед их выводом. Использование безопасных пайпов помогает гарантировать, что данные будут отображаться безопасно.

5. `Strict Contextual Auto-escaping (SCAE)`: Angular внедряет строгую контекстуальную автоэкранизацию, обеспечивая соответствие безопасности контексту вывода, что уменьшает риски XSS-атак.

6. `Content Security Policy (CSP)`: Настройка CSP на сервере для приложения Angular может предотвратить выполнение небезопасного кода и ограничить источники файлов, доступных вашему приложению.

7. `HTTP Interceptors`: HTTP-перехватчики позволяют контролировать HTTP-запросы и ответы, что может быть полезно для проверки и фильтрации данных, возвращаемых с сервера.

> Сочетание этих методов и механизмов помогает обеспечить безопасность Angular-приложений, предотвращая XSS-уязвимости и обеспечивая безопасное отображение данных пользователю.

- ### Какова роль компилятора шаблонов для предотвращения XSS-атак?
  > Компилятор шаблонов в Angular играет ключевую роль в предотвращении XSS-атак за счет того, что он осуществляет процесс трансформации HTML-шаблонов в код JavaScript, который затем выполняется в браузере. Вот как компилятор шаблонов в Angular помогает предотвращать XSS-уязвимости:

1. `Экранирование данных`: Компилятор шаблонов автоматически экранирует данные, встраиваемые в шаблоны, по умолчанию. Это значит, что компилятор применяет необходимые экранирующие механизмы, чтобы предотвратить внедрение вредоносного кода в HTML-документы, которые могут быть выполнены в браузере.

2. `Безопасные интерполяции`: Компилятор Angular обрабатывает выражения в шаблонах, чтобы предотвратить выполнение скриптов и XSS-атак через интерполяцию данных. Это помогает гарантировать безопасный вывод данных на стороне клиента.

3. `Проверка безопасности`: Компилятор Angular анализирует шаблоны и выражения на предмет потенциальных безопасностей, обеспечивая соответствие стандартам безопасности и предотвращая потенциальные XSS-уязвимости.

4. `Content Security Policy (CSP)`: Компилятор Angular работает в соответствии с политиками безопасности контента (CSP), которые можно настроить для ограничения возможностей атаки XSS и других угроз безопасности.

5. `Другие меры безопасности`: Компилятор шаблонов также совместно работает с другими механизмами безопасности Angular, такими как санитизация данных, использование безопасных пайпов и контрольные структуры, чтобы обеспечить общую безопасность приложения от атак XSS.

> Эффективное использование компилятора шаблонов Angular совместно с другими мерами безопасности помогает гарантировать, что приложения Angular защищены от угроз XSS и обеспечивают безопасное отображение пользовательского контента.

- ### Каковы различные контексты безопасности в Angular?
  > В Angular существуют различные контексты безопасности, которые определяют, как приложение должно обращаться с потенциально опасными операциями и данными. Вот несколько основных контекстов безопасности в Angular:

1. `Safe HTML (Безопасный HTML)`:

   - Angular обеспечивает механизмы безопасного встраивания HTML, чтобы предотвратить XSS-атаки. Механизм безопасного HTML (Safe HTML) позволяет отображать HTML-код без риска исполнения вредоносных скриптов.

2. `Safe Styles (Безопасные стили)`:

   - Аналогично безопасному HTML, Angular предоставляет средства для безопасного применения стилей к элементам, обеспечивая безопасность CSS и предотвращая XSS-атаки через стили.

3. `Safe Resource URLs (Безопасные URL-адреса ресурсов)`:

   - Для обеспечения безопасности при работе с внешними ресурсами, Angular предоставляет безопасный способ указания URL-адресов для ресурсов, таких как изображения, видео или аудиофайлы, чтобы избежать уязвимостей.

4. `Safe Script URLs (Безопасные URL-адреса скриптов)`:

   - Angular предоставляет механизм безопасного использования URL-адресов скриптов, чтобы предотвратить внедрение вредоносных скриптов в приложение.

5. `Safe Pipes (Безопасные пайпы)`:
   - Пайпы в Angular могут использоваться для преобразования данных. Angular предоставляет безопасные пайпы, которые также помогают предотвратить уязвимости и атаки.

Кроме того, Angular обладает другими функциями безопасности, такими как:

- `Санитизация данных` (Data Sanitization): Angular автоматически санитизирует данные по умолчанию, чтобы предотвратить уязвимости XSS.
- `Контроль доступа к маршрутам` (Route Guards): Angular Guards можно использовать для контроля доступа к определенным маршрутам или компонентам в приложении.

> Каждый из этих контекстов безопасности в Angular играет важную роль в обеспечении безопасности приложения и предотвращении различных видов угроз. Понимание и использование этих механизмов помогут сделать ваше приложение более надежным и защищенным.

- ### Что такое санитарная обработка? Угловой поддерживает это?
  > `Санитарная обработка (Sanitization)` веб-приложений является процессом очистки и обработки данных с целью предотвращения уязвимостей безопасности, в частности, атак типа XSS (межсайтовый скриптинг). Angular, безусловно, поддерживает санитизацию данных для безопасного отображения содержимого, так называемый Safe HTML.

> В контексте Angular санитизация обычно применяется к данным, которые могут содержать потенциально опасный HTML-код, CSS, URL или другую разметку, чтобы предотвратить возможные атаки XSS при отображении этих данных в шаблонах компонентов.

> Angular использует процесс под названием DomSanitizer для санитизации и безопасного отображения таких данных. DomSanitizer предоставляет методы для различных типов санитизации данных, такие как:

1. `bypassSecurityTrustHtml`: Помечает значение как безопасный HTML.
2. `bypassSecurityTrustStyle`: Помечает значение как безопасный стиль CSS.

3. `bypassSecurityTrustScript`: Помечает значение как безопасный JavaScript.
4. `bypassSecurityTrustUrl`: Помечает значение как безопасный URL-адрес.
5. `bypassSecurityTrustResourceUrl`: Помечает значение как безопасный URL-адрес ресурса (например, изображение).

> Эти методы позволяют разработчикам Angular явно указывать, что данные безопасны для использования в предоставленном контексте, минуя стандартные правила безопасности Angular. Необходимо использовать их осторожно, так как неправильное использование может все же создать уязвимости безопасности.

> Таким образом, санитарная обработка является важным аспектом обеспечения безопасности веб-приложений, и Angular обеспечивает специальные инструменты и методы для обеспечения этого процесса в вашем приложении.

- ### В чем разница между интерполированным содержимым и innerHTML?
  > В Angular разница между интерполированным содержимым и `innerHTML` заключается в способе обработки и вставки данных в шаблоны компонента.

### Интерполяция в Angular:

1. `Интерполяция` представляет собой способ вставки значений переменных компонента Angular в HTML-шаблон.
2. `Интерполяция` выполняется с помощью двойных фигурных скобок `{{ }}`.
3. Angular автоматически обновляет привязанные значения, отслеживая изменения внутри компонента.
4. `Интерполяция` безопасна по умолчанию и предотвращает вставку опасного HTML-кода.

```html
<p>Привет, {{ имя }}</p>
```

### `innerHTML` в Angular:

1. `innerHTML` - это свойство DOM элемента, которое позволяет вставлять HTML содержимое в элемент.
2. Использование `innerHTML` в Angular может привести к уязвимостям безопасности, таким как XSS, если данные не прошли проверку на безопасность.
3. Angular предлагает `безопасный вариант` использования `innerHTML` через `DomSanitizer`.
4. При использовании `innerHTML` в Angular, требуется соблюдать правила безопасности и проверять содержимое на предмет потенциально опасного кода.

```typescript
import { DomSanitizer, SafeHtml } from '@angular/platform-browser'

// В компоненте
export class MyComponent {
	htmlContent: SafeHtml

	constructor(private sanitizer: DomSanitizer) {
		this.htmlContent = this.sanitizer.bypassSecurityTrustHtml('<p>HTML содержимое</p>')
	}
}
```

### Ключевые различия:

- `Интерполяция` является специфичным синтаксисом Angular для вставки данных из компонента в шаблон безопасным способом.
- `innerHTML` просто вставляет предоставленное HTML содержимое внутрь элемента, и требует дополнительных мер безопасности в Angular для предотвращения уязвимостей.

Используйте `интерполяцию`, когда хотите вставить данные из компонента безопасным способом. `innerHTML` следует использовать осторожно в Angular, особенно если вставляемое содержимое не является безопасным или контролируемым.

- ### Как предотвратить автоматическую дезинфекцию?
  > В Angular автоматическая **дезинфекция (automatically sanitizing)** происходит, чтобы предотвратить потенциальные атаки на безопасность, такие как XSS (межсайтовый скриптинг). Однако в некоторых случаях может потребоваться отключить или предотвратить автоматическую дезинфекцию. Ниже приведены способы предотвращения автоматической дезинфекции в Angular:

1. Использование `bypassSecurityTrustHtml` и `bypassSecurityTrustStyle`

- Angular предоставляет сервис `DomSanitizer`, который позволяет безопасно встраивать HTML и CSS. С помощью методов `bypassSecurityTrustHtml` и `bypassSecurityTrustStyle` можно вручную указать Angular не дезинфицировать определенные куски контента.

Пример:

```typescript
import { DomSanitizer } from '@angular/platform-browser';

constructor(private sanitizer: DomSanitizer) {
    this.htmlContent = this.sanitizer.bypassSecurityTrustHtml('<p>HTML содержимое</p>');
}
```

2. Использование `bypassSecurityTrustScript` и `bypassSecurityTrustUrl`

- Сервис `DomSanitizer` также предоставляет методы для встраивания скриптов и URL без автоматической дезинфекции. Эти методы также могут использоваться для предотвращения дезинфекции.

3. Использование `DomSanitizer.bypassSecurityTrustResourceUrl`

- Если необходимо загрузить содержимое с внешнего ресурса, можно использовать этот метод для предотвращения дезинфекции URL.

4. Вывод предопределенной безопасной HTML разметки

- Если содержимое безопасно и уже необходимо вывести как HTML, можно использовать простую интерполяцию без использования `bypassSecurityTrustHtml`.

Важно отметить:

- `Безопасность` всегда должна быть приоритетом. Предотвращение дезинфекции может повысить риск уязвимости, поэтому необходимо тщательно оценить, действительно ли это необходимо.
- Всегда следуйте `лучшим практикам безопасности` и убедитесь, что контент, который вы встраиваете без дезинфекции, действительно безопасен.

- ### Безопасно ли использовать прямые методы DOM API с точки зрения безопасности?
  > Использование прямых методов DOM API в Angular с точки зрения безопасности представляет определенные риски, особенно если данные, получаемые извне, встраиваются напрямую без должной обработки или проверки. Вот почему:

Потенциальные угрозы безопасности при использовании прямых методов DOM API:

1. `Межсайтовый скриптинг (XSS)`:

   - Внедрение вредоносного JavaScript кода в приложение.
   - Использование методов DOM API для встраивания такого кода и потенциального выполнения на клиентской стороне.

2. `Прямые манипуляции с DOM:
   - Изменение или вмешательство в DOM без должной проверки и санитарной обработки вводимых данных.
   - Возможность создания уязвимостей, связанных с некорректными операциями с DOM.

Меры предосторожности при использовании прямых методов DOM API:

1. `Санизация вводимых данных`:

   - Перед тем как встроить данные в DOM, удостоверьтесь, что они прошли санитацию и отфильтрованы от потенциально опасного содержимого.

2. `Использование Angular Sanitizer`:

   - Если необходимо встраивать HTML, CSS или другие контенты, использование Angular Sanitizer (например, `DomSanitizer`) для безопасного встраивания.

3. `Ограничение доступа к DOM`:

   - Избегайте ненужных манипуляций с DOM. Предпочитайте использование инструментов Angular или библиотек, предназначенных для работы с DOM.

4. `Валидация ввода и вывода`:
   - Удостоверьтесь, что данные, которые вы получаете и встраиваете в DOM, соответствуют ожидаемому формату и содержанию.

Вывод:

> Прямое использование методов DOM API в Angular может быть безопасным при правильном подходе и соблюдении мер безопасности. Однако рекомендуется предпочитать использование инструментов и паттернов, предлагаемых Angular, для манипуляций с DOM, чтобы снизить риски возможных атак на безопасность, таких как XSS.

- ### Что такое DomSanitizer средство DOM?

> DomSanitizer в Angular — это сервис, предоставляемый Angular для безопасного манипулирования и анализа HTML, CSS и URL. Этот сервис играет важную роль в предотвращении уязвимостей безопасности, таких как межсайтовый скриптинг (XSS), путем фильтрации и санитизации входящих данных, которые отображаются пользователю в виде HTML.

Работа DomSanitizer в Angular:

1. `Санитизация HTML, CSS и URL`:

   - DomSanitizer позволяет фреймворку Angular предоставлять безопасные ресурсы для отображения пользователю. Например, при встраивании HTML из пользовательского ввода, DomSanitizer убеждается, что этот HTML безопасен для отображения и не содержит возможно опасных сценариев выполнения скриптов.

2. `Контроль над безопасностью`:

   - С помощью DomSanitizer можно контролировать, какие типы контента считаются безопасными для отображения и обработки в Angular-приложениях.

3. `Пример использования`:
   - Например, при получении HTML-кода из внешнего источника и его необходимости вставки в ваше приложение, DomSanitizer позволяет выполнить процесс санитизации данных перед отображением, обеспечивая безопасность вашего приложения.

Как использовать DomSanitizer:

1. `Импорт и инъекция`:

   - Чтобы использовать DomSanitizer, его необходимо импортировать из `@angular/platform-browser` и затем инъецировать в соответствующий Angular-класс.

2. `Методы санитизации`:
   - DomSanitizer предоставляет методы, такие как `bypassSecurityTrustHtml`, `bypassSecurityTrustStyle`, `bypassSecurityTrustScript`, `bypassSecurityTrustUrl` и `bypassSecurityTrustResourceUrl`, которые могут использоваться для обработки различных типов данных.

Пример:

```typescript
import { DomSanitizer } from '@angular/platform-browser';

constructor(private sanitizer: DomSanitizer) {
    const unsafeHtml = '<script>alert("XSS Attack")</script>';
    const safeHtml = this.sanitizer.bypassSecurityTrustHtml(unsafeHtml);
}
```

> Использование DomSanitizer в Angular помогает уменьшить риски безопасности, связанные с динамическим вводом данных, и обеспечивает безопасность при работе с HTML, CSS и URL в Angular-приложениях.

- ### Как вы поддерживаете защиту XSS на стороне сервера в приложении Angular?
  > Для поддержки защиты от XSS на стороне сервера в приложении Angular необходимо принимать ряд мер и рекомендаций, чтобы обеспечить безопасность входящих данных и контента до того, как они достигнут клиентской части приложения. Ниже приведены некоторые методы и практики для защиты от XSS на стороне сервера в приложении Angular:

1. `Регулярная санитизация данных на сервере`:

   - Перед тем как отправлять данные на клиентскую сторону, убедитесь, что все входящие данные санитизированы и правильно экранированы, чтобы предотвратить XSS-атаки.

2. `Использование Content Security Policy (CSP)`:

   - Настройте заголовки CSP на вашем сервере. CSP позволяет вам указать браузеру, откуда можно загружать ресурсы (например, скрипты, стили, шрифты) или какой тип контента можно отображать. Это может помочь предотвратить несанкционированные скрипты и другие ресурсы.

3. `Валидация и фильтрация входных данных`:

   - Проверяйте и фильтруйте входные данные на стороне сервера. Не доверяйте данным, полученным от пользователя без должной валидации.

4. `Экранизация специальных символов`:

   - Перед отправкой данных на клиентскую сторону преобразуйте специальные символы, такие как `<`, `>`, `&`, чтобы предотвратить внедрение вредоносного кода.

5. `Использование безопасных API-методов`:

   - Обращайтесь к безопасным API-методам и библиотекам для манипуляции строками, чтобы избежать возможности XSS-уязвимостей.

6. `Контроль доступа к данным`:

   - Управляйте правами доступа к данным на сервере, чтобы предотвратить несанкционированный доступ к конфиденциальной информации.

7. `Обновление и обновление безопасности`:

   - Регулярно проверяйте обновления безопасности для вашего серверного ПО и библиотек, чтобы избежать известных уязвимостей.

8. `Создание безопасных HTML-шаблонов`:
   - Если ваше приложение генерирует HTML-контент динамически на сервере, убедитесь, что это выполняется безопасно с помощью библиотек или методов, которые автоматически санитизируют или фильтруют входящие данные.

> Объединение этих методов и практик поможет обеспечить хороший уровень защиты от XSS-атак на стороне сервера вашего приложения Angular.

- ### Предотвращает ли angular уязвимости уровня http?
  > Angular как фреймворк для разработки веб-приложений предоставляет некоторые механизмы и инструменты, которые могут помочь предотвратить некоторые типы уязвимостей на уровне HTTP. Однако в целом защита от уязвимостей на уровне HTTP зависит не только от фронтенд-фреймворка, такого как Angular, но и от правильной конфигурации серверной стороны, общей архитектуры приложения, хороших практик разработки и других факторов. Вот несколько способов, с которыми Angular может помочь в предотвращении уязвимостей на уровне HTTP:

1. `CORS (Cross-Origin Resource Sharing)`:

   - Angular позволяет вам настроить CORS правила в фронтенд-коде для контроля доступа к ресурсам между разными доменами. Это помогает предотвратить некоторые типы атак, связанных с междоменными запросами.

2. `HTTP Interceptors`:

   - Angular предоставляет HTTP Interceptors для перехвата и обработки HTTP-запросов и ответов. Это может быть использовано для внедрения различных механизмов безопасности, таких как добавление заголовков безопасности, обработка ошибок, и т.д.

3. `HTTPS`:

   - Angular сам по себе не обеспечивает безопасность при передаче данных по сети. Он рекомендует использование HTTPS для защиты конфиденциальности и целостности данных, передаваемых между клиентом и сервером.

4. `Встроенные механизмы защиты`:

   - Angular включает в себя некоторые встроенные механизмы защиты, такие как санитизация данных, чтобы предотвратить XSS-атаки, и другие инструменты безопасности.

5. `Контроль сессий и аутентификация`:

   - Часто Angular приложения взаимодействуют с бэкендом для аутентификации и управления сессиями. Корректная реализация этих механизмов помогает в предотвращении атак на уровне HTTP.

6. `Обработка ошибок и обновления`:
   - Разработчики могут использовать Angular для обработки и отображения ошибок, что помогает улучшить общую безопасность приложения. Регулярное обновление Angular и его зависимостей также помогает в предотвращении известных уязвимостей.

> Хотя Angular предоставляет определенные инструменты и механизмы для повышения безопасности приложений на уровне HTTP, безопасной разработкой и правильной настройкой серверных аспектов также являются ключевые аспекты в борьбе с уязвимостями на уровне HTTP.

[Вернуться к началу статьи](#angular)

---

## Angular Universal

> Angular Universal — это технология, которая позволяет выполнять рендеринг Angular приложения на сервере вместо браузера. Это привносит ряд преимуществ, включая улучшенную производительность, SEO-оптимизацию и повышенную доступность для поисковых роботов.

> В контексте веб-разработки Angular Universal позволяет создавать приложения, которые могут быть рендерены как на сервере, так и на клиенте. Это означает, что при первом запросе от клиента сервер может сгенерировать и вернуть полностью отрендеренную страницу, что способствует более быстрой загрузке и улучшенной опыту для пользователей.

Основные преимущества Angular Universal:

1. `Улучшенная производительность`: Предварительный рендеринг на сервере сокращает время загрузки и позволяет снизить нагрузку на клиентское устройство.
2. `SEO-оптимизация`: Поисковые системы имеют лучший доступ к контенту, отображаемому на странице, когда он рендерится на сервере.

3. `Улучшенная доступность для поисковых роботов`: Контент, отображаемый на странице при помощи Angular Universal, может быть лучше проиндексирован поисковыми системами.

> Использование Angular Universal требует определенной настройки и адаптации вашего Angular приложения, чтобы оно могло работать как на стороне сервера, так и на стороне клиента.

[Вернуться к началу статьи](#angular)

---

## Angular service workers

> Сервис-воркер (Service Worker) - это скрипт на стороне клиента, который запускается браузером и работает в фоновом режиме, независимо от веб-приложения. Он предназначен для обработки событий, таких как сетевые запросы, уведомления и другие, а также может использоваться для кэширования ресурсов и обеспечения возможности работы офлайн.

> В Angular сервис-воркер обычно используется совместно с `Angular Service Worker`, который является встроенным механизмом для работы с сервис-воркером в приложениях Angular. Он обеспечивает ряд возможностей, таких как кэширование ресурсов, управление кэшем, обработка событий сети и другие.

Роль сервис-воркера в Angular включает в себя следующее:

- `Кэширование ресурсов` : С помощью сервис-воркера можно кэшировать ресурсы, такие как HTML, CSS, JavaScript, изображения и другие файлы. Это позволяет улучшить производительность приложения, особенно на медленных или ненадежных сетях.

- `Работа в офлайн-режиме` : Сервис-воркер может обрабатывать запросы, даже когда приложение находится в офлайн-режиме. Это позволяет предоставлять пользователю более качественный опыт использования приложения, сохраняя его работоспособность в условиях непостоянной сетевой связи.

- `Управление кэшем` : Сервис-воркер также обеспечивает возможность динамического управления кэшем, что позволяет приложению быть более гибким и эффективно использовать кэшированные ресурсы.

- `Уведомления` : С помощью сервис-воркера можно также обрабатывать уведомления, позволяя приложению отправлять уведомления пользователю, даже если приложение не запущено.

> Использование сервис-воркера в Angular приложении обычно включает настройку Angular Service Worker, что позволяет интегрировать данную функциональность в приложение с минимальными усилиями.

> `Angular Service Worker` является инструментом, предоставляемым Angular для облегчения создания прогрессивных веб-приложений (PWA) с использованием сервис-воркеров. Angular Service Worker предоставляет ряд функций, которые позволяют кэшировать ресурсы, обрабатывать запросы, управлять оффлайн-режимом и предоставлять другие возможности, связанные с использованием сервис-воркеров в веб-приложениях.

Рассмотрим основные шаги работы Angular Service Worker:

- `Настройка` : Для начала работы с Angular Service Worker необходимо добавить его в проект Angular. Это можно сделать с помощью Angular CLI или вручную. После этого необходимо настроить файл конфигурации для сервис-воркера, указывая, какие ресурсы кэшировать, как обрабатывать события сети и другие параметры.

- `Создание манифеста` : Для создания PWA также требуется манифест приложения, который определяет его имя, иконки, цвет темы и другие свойства. Angular Service Worker может помочь с генерацией и обслуживанием этого манифеста.

- `Развертывание` : После настройки Angular Service Worker и создания необходимых файлов приложение должно быть развернуто на сервере. Сервис-воркер зарегистрируется и начнет работу, обрабатывая запросы и управляя кэшированием ресурсов.

- `Работа в оффлайн-режиме` : После установки и активации сервис-воркера, приложение становится способным кэшировать ресурсы и продолжать работу в оффлайн-режиме. Это означает, что пользователи смогут использовать приложение, даже если у них нет подключения к интернету.

- `Управление кэшем и событиями` : Angular Service Worker предоставляет API для управления кэшем, что позволяет добавлять, обновлять и удалять ресурсы из кэша во время выполнения. Он также позволяет обрабатывать события сети, такие как запросы,
  изменения статуса сети и другие.

> `Angular Service Worker`, основанный на сервис-воркерах, имеет свои собственные ограничения, которые следует учитывать при разработке приложений. Некоторые из наиболее значимых ограничений включают в себя:

- `HTTPS` :
  Сервис-воркеры требуют использования шифрования SSL/TLS, что означает, что они могут работать только на сайтах, использующих протокол HTTPS или на локальных серверах во время разработки (localhost).

- `Ограничения кэширования` :
  Некоторые ресурсы не могут быть безопасно кэшированы, например, конфиденциальные или изменяющиеся динамически данные. Для таких данных следует настраивать политику кэширования внимательно.

- `Недоступность сетевых ресурсов` :
  Сервис-воркеры имеют ограничения по доступу к ресурсам, расположенным вне своего происхождения из-за политики безопасности браузера, известной как Same-Origin Policy.

- `Ограничения доступа к DOM` :
  Сервис-воркеры не имеют прямого доступа к DOM страницы, таким образом, они не могут модифицировать ее напрямую. Они предназначены для управления сетевыми запросами и кэширования, но не для работы с DOM.

- `Ограничения по использованию файловой системы` :
  Сервис-воркеры работают в песочнице без доступа к файловой системе пользователя.

- `Поддержка браузерами` :
  В зависимости от возможностей различных браузеров, поддержка сервис-воркеров может быть различной. Некоторые функции могут не быть доступны во всех браузерах, что ограничивает их использование на определенных платформах.

> Хотя сервис-воркеры предоставляют превосходные возможности для улучшения производительности и оффлайн-поддержки веб-приложений, важно учитывать эти ограничения при их использовании для обеспечения корректного и безопасного функционирования приложений.

[Вернуться к началу статьи](#angular)

---

## Angular ngZone

> В Angular, `Zone` (или Zone.js) — это библиотека, которая помогает управлять асинхронными операциями и отслеживать изменения в приложении. Она позволяет автоматически обнаруживать изменения в состоянии приложения и инициировать обновление представления, когда это необходимо.

> `ngZone` в Angular — это сервис, который предоставляет API для работы с механизмом обнаружения изменений, основанным на Zone.js. Он позволяет разработчикам управлять зоной выполнения и контролировать, когда и как выполняется обнаружение изменений в приложении.

Основные функции ngZone:

- `Обнаружение изменений`: ngZone автоматически отслеживает асинхронные операции и инициирует обновление представления, когда это необходимо. Это позволяет избежать ручного вызова методов обновления.

- `Вход и выход из зоны`: Вы можете явно войти в ngZone с помощью метода run(), который позволяет выполнять код в пределах Angular-зоны, где будут автоматически отслеживаться изменения. Кроме того, можно использовать runOutsideAngular(), чтобы выполнять код вне Angular-зоны, тем самым отключая автоматическое обнаружение изменений, что может быть полезно для повышения производительности в некоторых сценариях.

- `Производительность`: Если вы знаете, что определенный код не должен инициировать обнаружение изменений — например, в обработчиках событий или долгих вычислениях — использование runOutsideAngular() может помочь избежать ненужных обновлений интерфейса и улучшить производительность приложения. ⚡️

- `Обработка ошибок`: ngZone также предоставляет механизм для перехвата и обработки ошибок, происходящих в асинхронных операциях. Это может быть полезно для централизованной обработки ошибок в вашем приложении.

> В Angular есть несколько хуков жизненного цикла зоны, которые позволяют вам выполнять код в ответ на различные события и изменения состояния в вашей зоне. Вот основные из них:

1. `onEnter`
   Этот хук вызывается при входе в зону. Вы можете использовать его для выполнения кода, как только начнется выполнение асинхронной операции.

2. `onLeave`
   Вызывается при выходе из зоны. Это полезно для выполнения действий, когда завершены асинхронные операции, и вам нужно выполнить некоторые завершающие действия.

3. `onStable`
   Этот хук срабатывает, когда все асинхронные операции завершены, и система вернулась в стабильное состояние. Вы можете использовать его для выполнения логики, которая должна выполняться после завершения всех обновлений.

4. `onUnstable`
   Вызывается, когда зона считает, что начала обрабатываться асинхронная активность. Это может быть полезно для отслеживания начала процесса, когда начинаются долгие операции.

5. `onError`
   Этот хук срабатывает, когда возникает ошибка в приложении. Он может быть использован для глобальной обработки ошибок.

```typescript
import { NgZone } from '@angular/core';

constructor(private ngZone: NgZone) {
  this.ngZone.run(() => {
    // Код при входе в зону
    console.log('Entered zone');
  });

  this.ngZone.onStable.subscribe(() => {
    // Код, который выполняется, когда все асинхронные задачи завершены
    console.log('Zone is stable');
  });

  this.ngZone.onError.subscribe((error) => {
    // Обработка ошибок
    console.error('An error occurred:', error);
  });
}
```

### Методы NgZone для управления обнаружением изменений в Angular.

1. `run()`
   Этот метод позволяет выполнить код внутри зоны. Angular будет отслеживать любые изменения, вызванные этим кодом, и обновлять представление соответственно.

```typescript
this.ngZone.run(() => {
	// Код, который должен быть выполнен в зоне
})
```

2. `runOutsideAngular()`
   Этот метод позволяет выполнить код вне зоны, что предотвращает ненужные детекции изменений при выполнении асинхронных операций. Это полезно для улучшения производительности, когда вам не нужно обновлять состояние Angular.

```typescript
this.ngZone.runOutsideAngular(() => {
	// Код, который выполняется вне зоны
})
```

3. `onStable`
   Этот метод возвращает Observable, который позволяет подписаться на события, когда зона переходит в стабильное состояние после завершения всех асинхронных задач. Это полезно для выполнения кода после завершения всех изменений.

```typescript
this.ngZone.onStable.subscribe(() => {
	// Код, который выполняется, когда зона стабильна
})
```

4. `onUnstable`
   Этот метод также возвращает Observable и позволяет подписаться на события, когда зона становится нестабильной. Это может быть полезно для отслеживания начала выполнения асинхронных операций.

```typescript
this.ngZone.onUnstable.subscribe(() => {
	// Код, который выполняется, когда зона нестабильна
})
```

5. `runGuarded()`
   Этот метод позволяет выполнить код внутри зоны с защитой от ошибок. Если в этом коде возникает ошибка, она будет поймана и передана, а не вызовет сбой приложения.

```typescript
this.ngZone.runGuarded(() => {
	// Код, который выполняется внутри зоны с защитой от ошибок
})
```

> Настройки zone.js в Angular могут быть изменены в зависимости от ваших требований по производительности и специфики приложения.

- Настройка через zone.js API (методы).
- Настроить `zone.js` в файле `polyfills.ts`, добавив или изменив параметры.
- Можно создать пользовательские зоны.

```typescript
import 'zone.js'
import { Zone } from 'zone.js'

const myCustomZone = Zone.current.fork({
	name: 'myCustomZone',
	onSchedule: (parentZoneDelegate, currentZone, targetZone, zoneSpec) => {
		console.log('Scheduled in myCustomZone')
		return parentZoneDelegate.scheduleTask(targetZone, zone)
	},
})

// Использование вашей зоны
myCustomZone.run(() => {
	// Ваш код
})
```

- Отключение zone.js (не рекомендуется).

[Вернуться к началу статьи](#angular)

---

## Internationalization

> Angular предоставляет мощные инструменты для интернационализации (i18n), которые помогают разработчикам легко адаптировать приложения для разных языков и культур. Вот несколько ключевых аспектов, которые упрощают этот процесс.

> В Angular вы можете вручную зарегистрировать данные локали, используя модуль @angular/common и класс registerLocaleData.

- Импортируйте необходимые модули: Вам нужно импортировать `registerLocaleData` и данные локали из соответствующего файла, например, для русского языка.
- Зарегистрируйте данные локали: Вызывайте `registerLocaleData`, передавая ему данные локали.
- Настройте `LOCALE_ID`: Вам нужно также указать LOCALE_ID, чтобы Angular знал, какую локаль использовать.

```typescript
import { NgModule } from '@angular/core'
import { BrowserModule } from '@angular/platform-browser'
import { registerLocaleData } from '@angular/common'
import localeRu from '@angular/common/locales/ru' // Импортируйте данные локали для русского языка
import { AppComponent } from './app.component'
import { LOCALE_ID } from '@angular/core'

registerLocaleData(localeRu) // Регистрация локали

@NgModule({
	declarations: [AppComponent],
	imports: [BrowserModule],
	providers: [
		{ provide: LOCALE_ID, useValue: 'ru' }, // Указываем, что используем русский язык
	],
	bootstrap: [AppComponent],
})
export class AppModule {}
```

> В Angular перевод шаблона проходит через несколько этапов. Основные этапы перевода можно описать следующим образом:

1. Анализ шаблона:

   > Angular анализирует шаблон на наличие элементов, которые нужно интерполировать или изменить, таких как текст, атрибуты, директивы и биндинги.
   > Этот этап также включает в себя выявление структурных и атрибутных директив.

2. Трансляция:

   > Angular преобразует шаблон в дерево компонентов и создает функциональные представления, которые могут быть использованы в приложении.
   > На этом этапе создаются функции для обновления представлений при изменении данных.

3. Создание и внедрение:

   > На основе анализа и трансляции Angular создает экземпляры компонентов и внедряет их в DOM.
   > Внедрение зависимостей и создание дочерних компонентов также происходят на этом этапе.

4. Отслеживание изменений:
   > Angular использует механизм отслеживания изменений `Change Detection` для определения, когда обновить представление на основе изменений данных.
   > Это обеспечивает согласованность между моделью и представлением.

### Перевод текста

> В Angular Можете переводить текст без создания дополнительных элементов, используя встроенный механизм интернационализации (i18n) или сторонние библиотеки, такие как ngx-translate.

```html
<p i18n="@@hello">Привет</p>
```

```npm
npm install @ngx-translate/core @ngx-translate/http-loader

```

```typescript
import { Component } from '@angular/core'
import { TranslateService } from '@ngx-translate/core'

@Component({
	selector: 'app-root',
	template: `<div>{{ 'HELLO' | translate }}</div>`,
})
export class AppComponent {
	constructor(private translate: TranslateService) {
		this.translate.setDefaultLang('en')
		this.translate.use('en')
	}
}
```

> В Angular для работы с интернационализацией и множественными числами используется механизм, называемый i18n plural. Он основан на различных категориях множественного числа, которые зависят от языка. Вот основные категории:

- `one` (один) — используется, когда значение равно 1 (для языков, где это применимо).
- `few`(несколько) — для некоторых языков используется при значениях 2-4, но не используется в русском языке.
- `many` (много) — применяется, когда значение больше 1 или соответствует определённым правилам языка (например, для 0 и чисел выше 4 в русском).
- `other` (другие) — используется для всех других случаев, которые не подходят под предыдущие категории.

> Выражение `select ICU` в Angular — это специальный синтаксис для интернационализации (i18n), который позволяет вам делать выбор в зависимости от нескольких условий. Это особенно полезно, когда вам нужно обрабатывать различные варианты текста в зависимости от значений, таких как изменения статуса, пола и т. д.

```html
<p i18n="@@userStatus">{ user.gender, select, male {Мужчина} female {Женщина} other {Не указано} }</p>
```

Как это работает:

- `Ключ`: Это значение, по которому происходит выбор (в данном случае user.gender).
- `Параметры`: После ключа идет слово select, за которым следуют пары ключ-значение, разделенные пробелами. Каждый ключ соответствует одному из условий.
- `Резервный вариант`: Можно использовать опцию other, чтобы задать текст, который будет использоваться, если ни одно из условий не выполнено.

> В Angular для получения текущего направления текста в зависимости от локали можно использовать сервис `LOCALE_ID`, а также библиотеку @angular/common. Текст может быть направлен слева направо (`LTR`) или справа налево (`RTL`) в зависимости от языка.

```typescript
@Component({
	selector: 'app-my-component',
	template: ` <div [dir]="textDirection">Ваш контент здесь...</div> `,
})
export class MyComponent {
	public textDirection: string

	constructor(@Inject(LOCALE_ID) private locale: string) {
		this.textDirection = this.isRtlLocale(locale) ? 'rtl' : 'ltr'
	}

	private isRtlLocale(locale: string): boolean {
		// Здесь вы можете перечислить локали, для которых используется RTL
		return ['ar', 'he'].includes(locale)
	}
}
```

[Вернуться к началу статьи](#angular)

---

## Starting change detection Angular

> В Angular изменение данных и обновление интерфейса могут быть выполнены несколькими способами. Вот основные из них:

- `Zone.js`: Angular использует библиотеку Zone.js для отслеживания изменений в приложении. Когда выполняется код внутри зоны, Angular автоматически обнаруживает изменения и запускает проверку изменений.

- `ChangeDetectorRef`: Вы можете вручную управлять механизмом обнаружения изменений, используя ChangeDetectorRef. Это позволяет вам оптимизировать, когда стоит выполнять обнаружение изменений, например, использовать методы markForCheck и detectChanges.

- `Async Pipe`: Использование async pipe в шаблонах, который автоматически подписывается на Observable и обновляет интерфейс при изменении данных.

- `NgZone`: Вы можете использовать NgZone.run() для выполнения кода вне Angular зоны и затем снова входить в нее для обновления интерфейса.

- `Events`: Через событийное взаимодействие, такое как события DOM или пользовательские события, Angular также может реагировать на изменения данных и запускать обнаружение изменений.

- `OnPush` стратегия изменения: Используя стратегию обнаружения изменений OnPush, вы ограничиваете обновления компонентов только при изменении ссылок на входные данные или при эмитации событий.

- `Observable`: Если данные являются Observable, Angular автоматически выполняет обнаружение изменений при изменении данного Observable.

[Вернуться к началу статьи](#angular)

---

## Optimising the performance of asynchronous validators

1. Использование `debounceTime()`

- При работе с асинхронными валидаторами, особенно когда они связаны с запросами к серверу, вы можете использовать операторы RxJS, такие как `debounceTime()`, чтобы уменьшить количество запросов. Это особенно важно для полей ввода, где пользователь может вводить данные быстро.

```typescript
import { debounceTime } from 'rxjs/operators'

this.form
	.get('fieldName')
	.valueChanges.pipe(debounceTime(300)) // Задержка в 300 мс
	.subscribe(value => {
		// запуск асинхронного валидатора
	})
```

2. `Кеширование результатов`

- Если валидатор вызывает API для проверки значения, вы можете кэшировать результаты, чтобы не выполнять повторные запросы для одинаковых значений.

```typescript
const cache = {};

async validate(value: string) {
  if (cache[value]) {
    return cache[value];
  }

  const result = await this.someAsyncCheck(value);
  cache[value] = result;
  return result;
}

```

3. `Использование switchMap()` для обработки запросов

- Использование `switchMap()` для асинхронных операций гарантирует, что предыдущие запросы будут отменены, если новое значение было введено до того, как предыдущий запрос завершился.

```typescript
import { switchMap } from 'rxjs/operators'

this.form
	.get('fieldName')
	.valueChanges.pipe(
		debounceTime(300),
		switchMap(value => this.someAsyncCheck(value))
	)
	.subscribe(result => {
		// Обработка результата
	})
```

4. Минимизация количества асинхронных операций

- Старайтесь уменьшить количество асинхронных операций, проводимых в валидаторах. Проводите проверки, которые могут быть выполнены синхронно, перед асинхронными.

5. Асинхронный валидатор на уровне формы

- Иногда имеет смысл использовать асинхронную валидацию на уровне формы (например, для всех полей сразу), что может снизить количество необходимых запросов.

6. Ленивая загрузка данных

- Если ваши валидаторы требуют данных из базы данных, рассмотрите возможность ленивой загрузки данных только в случае необходимости, а не заранее.

7. Проффиленный селектор для автоматической валидации

- Избегайте лишней валидации на каждом изменении поля. Например, можно использовать `ngModelOptions` с `updateOn` для изменения момента запуска валидации.

```html
<input [(ngModel)]="fieldValue" [ngModelOptions]="{ updateOn: 'blur' }" />
```

[Вернуться к началу статьи](#angular)

---

## Standalone

> Автономный компонент `Standalone Component` в Angular — это компонент, который может существовать независимо от других компонентов и модулей. Он не требует объявления в каком-либо модуле, что упрощает структуру приложения и делает компоненты более переиспользуемыми.

```npm
ng generate component имя-компонента --standalone
```

```typescript
import { Component } from '@angular/core'

@Component({
	selector: 'app-standalone',
	template: `<h1>Hello, Standalone Component!</h1>`,
	standalone: true, // Указвыет что данный компонент будет автономным
	providers: [], // Импортируйте другие Service и Module для использоваия
	imports: [ExampleComponent], // Импортируйте другие Component для использоваия
})
export class StandaloneComponent {}
```

> В Angular можно использовать автономные компоненты `standalone components` внутри модулей, созданных с помощью `NgModule`

```typescript
// Создать компонент
import { Component } from '@angular/core'

@Component({
	selector: 'app-autonomous',
	template: `<h1>Автономный компонент!</h1>`,
	standalone: true,
})
export class AutonomousComponent {}

// Добавить его в модуль

import { NgModule } from '@angular/core'
import { CommonModule } from '@angular/common'
import { AutonomousComponent } from './autonomous.component'

@NgModule({
	declarations: [],
	imports: [
		CommonModule,
		AutonomousComponent, // Импортируем автономный компонент
	],
	exports: [AutonomousComponent],
})
export class ExampleModule {}
```

> Чтобы лениво загрузить автономный компонент в `Angular`, можно использовать механизмы маршрутизации, которые поддерживают ленивую загрузку модулей.

1. Создайте автономный компонент

```typescript
import { Component } from '@angular/core'

@Component({
	selector: 'app-autonomous',
	template: `<h1>Автономный компонент загружен!</h1>`,
	standalone: true,
})
export class AutonomousComponent {}
```

2. Создайте модуль для ленивой загрузки

```typescript
import { NgModule } from '@angular/core'
import { CommonModule } from '@angular/common'
import { RouterModule } from '@angular/router'
import { AutonomousComponent } from './autonomous.component'

@NgModule({
	declarations: [],
	imports: [
		CommonModule,
		RouterModule.forChild([{ path: '', component: AutonomousComponent }]), // Ленивое подключение
	],
	exports: [],
})
export class AutonomousModule {}
```

3. Настройте маршрутизацию

```typescript
import { NgModule } from '@angular/core'
import { RouterModule, Routes } from '@angular/router'

const routes: Routes = [
	{
		path: 'autonomous',
		loadChildren: () => import('./path-to/autonomous.module').then(m => m.AutonomousModule),
	},
]

@NgModule({
	imports: [RouterModule.forRoot(routes)],
	exports: [RouterModule],
})
export class AppRoutingModule {}
```

4. Используйте маршрутизацию в приложении

```HTML
<nav>
  <a routerLink="/autonomous">Перейти к автономному компоненту</a>
</nav>
<router-outlet></router-outlet>
```

[Вернуться к началу статьи](#angular)

---

### Ресурсы

- [Маршрутизация в Angular](https://proweb63.ru/help/angular/ng-routing-doc)
- [Директивы ng-template, ngTemplateOutlet и ng-container](https://proweb63.ru/help/angular/angular-directives-nt-tpl-ng-cnt)
- [Использование Angular Service Worker RUS](https://angdev.ru/archive/angular9/service-workers/)
- [Использование Angular Service Worker ENG](https://blog.angular-university.io/angular-service-worker/)
