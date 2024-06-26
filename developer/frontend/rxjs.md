# RxJs

Для предварительного преобразования отправляемых объектом Observable данных или преобразования и управления самими Observable используются специальные функции - операторы.
В RxJs есть «горячие» и «холодные» Observables.

- Горячий Observable порождает данные постоянно, даже если на него никто не подписан.
- Холодный Observable, соответственно, порождает данные только если у него есть хотя бы один подписчик.

Все RxJS операторы подразделяются на категории. Так, различают операторы:

- Создания (of, from, fromEvent, interval);
- Преобразования (map, scan, buffer);
- Фильтрации (filter, take, skip, distinct);
- Обработки ошибок (catchError, retry, onErrorResumeNext);
- Условия (skipUntil, skipWhile, takeUntil, takeWhile);
- Математические (min, max, count);
- Утилиты (tap, delay);
- Для Connectable Observable (share, shareReplay, publish).

Помимо создания через `Observable.create()` существует целое множество функций, при помощи которых можно получить Observable. Рассмотрим некоторые из них. (Для простоты обработки можно передавать не все обработчики при подписке).

Оператор `of` для создания `Observable`. Значение, которое было передано в качестве аргумента, будет “прокинуто в трубу” для дальнейшей обработки.

## `mergeAll/mergeMap`

Особенность mergeAll/mergeMap оператора в том, что, если к нему спускается еще один поток, то он так же подписывается на него. Таким образом, во внешний поток у нас могут попадать значения сразу из нескольких внутренних. https://habr.com/ru/post/450050/

## `concatAll/concatMap`

Данный оператор, подписавшись на внутренний поток, ждет, пока тот не завершится, и только потом подписывается на следующий. Если во время выполнения одного потока к нему спускается новый, то он помещается в очередь до тех пор, пока предыдущий не завершится.

```JavaScript
  // поток, генерирующий 1 по прошествии одной секунды
  const firstInnerObservable = timer(1000).pipe( mapTo(1) );

  // поток, генерирующий 2 по прошествии половины секунды
  const secondInnerObservable = timer(500).pipe( mapTo(2) );

  of(firstInnerObservable, secondInnerObservable).pipe(
    concatAll()
  ).subscribe({ next: console.log });
```

## `switchAll/switchMap`

Данный оператор отличается от предыдущих тем, что когда он получает новый поток, то сразу отписывается от предыдущего и подписывается на новый.

```JavaScript
  of(firstInnerObservable, secondInnerObservable).pipe(
    switchAll()
  ).subscribe({ next: console.log });
```

Во внешний поток попало только значение из второго внутреннего потока. Все потому что switchMap отписался от первого, когда получил второй поток.

## `concat`

- Удобно, когда важен порядок вывода последовательностей.

## `forkJoin`

- аналог Promise.all().

## `pairwisw`

- возвращает не только текущее значение, но в месте с ним и предыдущее значение последовательности.

## `combineLatest`

- получает последние значения из каждой последовательности при эммите одного из них.

```typescript
  this.model$ = combineLatest([
    this.store.pipe(select(lifeEditorSelector)),
    this.store.select(is Allergy History Questionnaire Visible Selector),
  ]).pipe(
    switchMap(([life, showAllergyHistoryQuestionnaire]: [ILifeEditorState, boolean]) => {
          if (life.state === 'ready') {
            return this.getModel(life.data, showAllergyHistoryQuestionnaire);
          }
          if (life.state === 'pending') {
            return of({ state: 'pending' } as IModel);
          }
          if (life.state === 'error') {
            return of({ state: 'error' } as IModel);
          }
        }),
      );
```

## `from`

- `from` в RxJS используется для создания Observable из различных источников данных, таких как массивы, промисы, итерируемые объекты и т.д.

```typescript
    from<T>(input: ObservableInput<T>): Observable<T>
    // Здесь input представляет собой источник данных, который нужно преобразовать в Observable.
    // Метод from возвращает Observable, который эмитирует элементы из источника данных.
```

```typescript
// Cоздать Observable из массива
import { from } from 'rxjs'

const array = [1, 2, 3]
const observable = from(array)

observable.subscribe(value => console.log(value))
```

```typescript
// Cозданиt Observable из промиса
import { from } from 'rxjs'

const promise = new Promise(resolve => resolve('Hello'))
const observable = from(promise)

observable.subscribe(value => console.log(value))
```

## `throwError`

- throwError в RxJS используется для создания Observable, который немедленно генерирует ошибку и завершается.
- Метод throwError также может принимать объект ошибки в качестве аргумента

```typescript
import { throwError } from 'rxjs'

const error = new Error('Something went wrong')
throwError(error)
```

## `map`

- map в RxJS используется для преобразования значений, передаваемых через поток данных (Observable). Он принимает функцию обратного вызова, которая принимает текущее значение в потоке данных и возвращает преобразованное значение.

```typescript
import { of } from 'rxjs'
import { map } from 'rxjs/operators'

const numbers$ = of(1, 2, 3, 4, 5)

const doubledNumbers$ = numbers$.pipe(map(number => number * 2))

doubledNumbers$.subscribe(value => console.log(value))
// Выводит: 2, 4, 6, 8, 10
```

## `filter`

- filter в RxJS используется для фильтрации значений, которые передаются через Observable. Он создает новый Observable, который будет содержать только те значения, которые удовлетворяют заданному условию.

```typescript
    // Синтаксис метода filter выглядит следующим образом:
    filter(predicate: (value: T, index: number, source: Observable<T>) => boolean, thisArg?: any): Observable<T>
```

`predicate` - это функция, которая принимает три аргумента:

- `value` - текущее значение, которое проходит через Observable
- `index` - индекс текущего значения
- `source` - исходный Observable

`predicate` должна возвращать true, чтобы значение прошло через фильтр, или false, чтобы оно было отфильтровано.

```typescript
import { from } from 'rxjs'
import { filter } from 'rxjs/operators'

const source = from([1, 2, 3, 4, 5])

const filtered = source.pipe(filter(value => value % 2 === 0))

filtered.subscribe(value => console.log(value)) // выводит 2, 4
```

## `debounceTime`

> Метод `debounceTime` в RxJS используется для задержки передачи значений через Observable на заданное время. Он принимает один параметр - время в миллисекундах, в течение которого Observable должен быть заблокирован, чтобы избежать передачи повторяющихся значений.

> В основном, `debounceTime` используется для обработки пользовательского ввода, когда вы хотите получать значение только после того, как пользователь закончил вводить данные. Например, если пользователь быстро нажимает клавиши на клавиатуре, debounceTime может задержать передачу значений, чтобы избежать обработки каждого нажатия клавиши и обрабатывать только последнее значение после заданной задержки.

> `debounceTime` работает следующим образом: когда Observable получает значение, он устанавливает таймер на заданное время. Если в течение этого времени Observable получает новое значение, таймер сбрасывается и начинается новый отсчет. Если таймер заканчивается, Observable передает последнее полученное значение.

```typescript
import { fromEvent } from 'rxjs'
import { debounceTime } from 'rxjs/operators'

const input = document.querySelector('input')

fromEvent(input, 'input')
	.pipe(debounceTime(500))
	.subscribe(event => console.log(event.target.value))
```

## Subject, Schedulers,

`Subject` является разновидностью объектов Observable. Особенность Subject в том, что он может отправлять данные одновременно множеству "потребителей", которые могут регистрироваться уже в процессе исполнения Subject, в то время как исполнение стандартного Observable осуществляется уникально для каждого его вызова.
Создание происходит с помощью new Subject(). Далее регистрируются обработчики вызовом метода subscribe(), принимающего подобно обычному Observable три функции: next(), error() и complete().

- `BehaviorSubject` хранит в себе последнее отправленное им значение. Так, каждому новому обработчику в момент регистрации (вызов subscribe()) будет отправлено это значение. Начальное значение задается в момент создания RxJS BehaviorSubject.

```TypeScript
  const sbj = new BehaviorSubject<number>(5);
  sbj.subscribe(vl => console.log(`1st: ${vl}`)); 1st: 5
```

- `ReplaySubject` способны хранить заданное количество последних значений, которое задается при создании объекта. Все новые "потребители" сразу же получают по очереди все n указанных значений RxJS ReplaySubject.

```TypeScript
  const sbj = new ReplaySubject(2);
  sbj.next(5);
  sbj.subscribe(vl => console.log(`1st: ${vl}`));
```

- `AsyncSubject` "потребителям" передается только последнее значение объекта и только, когда он завершит свое выполнение (вызов complete()).

```TypeScript
  const sbj = new AsyncSubject();
  sbj.subscribe(vl => console.log(`Async: ${vl}`));
  setTimeout(() => sbj.unsubscribe(), 3000);
```

Для управления временем и очередностью выполнения операций в объектах Observable, имеются RxJS Schedulers.
Сперва выполняется текущий синхронный код (callstack), далее очередь микрозадач (Promise), и если нет другого синхронного кода - очередь макрозадач (готовый для исполнения код, обернутый функциями setTimeout() и setInterval() или AJAX-запросы).Учитывая описанное выше, вполне логично, что имеются следующие типы RxJS Schedulers:

- queue - добавляет операцию в callstack;
- asap - регистрирует операцию в очереди микрозадач;
- async - регистрирует операцию в очереди макрозадач;
- animationFrame - отвечает за действия, выполняемые перед перерисовкой

## Observable

В RxJS, `Observable` представляет собой объект, который представляет поток асинхронных данных, которые могут быть переданы в течение времени. Observable может получать данные и уведомлять своих подписчиков об изменениях через метод next(), а также сообщать об ошибках через метод error() или завершаться с помощью метода complete().

Принцип работы Observable можно представить следующим образом:

```typescript
import { Observable } from 'rxjs'

const myObservable = new Observable(observer => {
	observer.next('Hello')
	observer.next('World')
	observer.complete()
})

// Подписка на Observable
myObservable.subscribe({
	next: value => console.log(value),
	error: error => console.error(error),
	complete: () => console.log('Observable completed'),
})
```

> В данном примере, мы создали Observable, который передает значения 'Hello' и 'World' своим подписчикам и завершается после этого. При подписке на Observable выводятся значения в консоль, а при завершении Observable выводится сообщение 'Observable completed'. Observable в RxJS предоставляет мощный инструмент для работы с потоками данных, а также позволяет легко комбинировать, трансформировать и обрабатывать потоки данных с помощью различных операторов, таких как map, filter, mergeMap и другие.

Функция `asObservable()` в RxJS используется для создания и возвращения объекта Observable из объекта, который не является Observable, например, из Subject или какого-то другого типа потока данных.

Этот метод позволяет "замаскировать" объект, чтобы он вел себя как Observable и предоставлял доступ только к методам Observable. Это полезно, когда вы хотите предоставить другим частям вашего приложения только доступ для подписки на поток данных, но не хотите, чтобы другие части могли изменять или отправлять элементы в этот поток.

Пример использования .asObservable() с Subject:

```js
import { Subject } from 'rxjs';

const subject = new Subject<number>();

const observable = subject.asObservable(); // Преобразование Subject в Observable

observable.subscribe({
  next: (value) => console.log(value),
});

subject.next(1); // Этот элемент не будет отправлен в observable, т.к. мы его превратили в Observable с помощью asObservable()
```

Таким образом `.asObservable()` позволяет создавать "read-only" обзерваблы для безопасного распространения данных в RxJS.

[Вернуться к началу статьи](#rxjs)

---
