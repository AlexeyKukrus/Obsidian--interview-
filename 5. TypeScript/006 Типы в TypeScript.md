TypeScript добавляет слой статических типов, которые будут сохраняться в месте хранения данных (переменная, ключ в объекте, параметр в функции…) на протяжении всей работы приложения
Типы проверяются в процессе разработки (всплывают ошибки и подсказки), а также при компиляции и если проверка не проходит, то приложение не работает. Проверка типов гарантирует, что значения всегда будут соответствовать прогнозу.

- **boolean (логический тип)
```Typescript
const isCompleted: boolean = false;
```
- **number (числовой тип)
```Typescript
const num: number = 21;
```
- **string (строковый тип)
```Typescript
const name: string = 'Alex';
const str: string = `Hello, ${name}`;
```
- **array (массив)
```Typescript
const list: number[] = [1, 2, 3];
const list2: Array<number> = [1, 2, 3];
```
- **tuple (кортеж)
```Typescript
const list: [number, string, boolean] = [1, '2', true];

const list2: [number, string, boolean];
list = [1, '2', true];
```
- enum (перечисление)
```Typescript
enum Directions {
	Up,
	Down,
	Left,
	Right
}

Directios.Up;     // 0
Directions.Down;  // 1
Directions.Left;  // 2
Directions.Right; // 3
//____________________________________________________________________________
enum Directions {
	Up = 2,
	Down = 4,
	Left = 6,
	Right
}

Directios.Up;     // 2
Directions.Down;  // 4
Directions.Left;  // 6
Directions.Right; // 7
```
- **any (любой тип)
```Typescript
let list: [any, any, any] = [1, '2', true];
list = [1, null, 'true'];
```
- **void (отсутствие возвращаемого значения)
```Typescript
const greetUser = ():void => {
	alert('Hello');
};
```
- **null и undefined
```Typescript
const n: null = null;
const u: undefined = undefined;
```
- **never - тип, который обозначает, что результата от выполнения функции не будет получен. Используется в 2 случаях:
```Typescript
//1. Когда функция возвращает ошибку
const msg = 'hello';
const error = (msg: string): never => {
	throw new Error(msg)
};

//2. Когда функция бесконечно выполняется
const infinityLoop = (): never => {
	while (true) {
	}
};
```
- object (не примитивный тип данных)
- **type (тип, который позволяет создавать пользовательские типы)
```Typescript
type Name = string;

let id: Name;
id = '42'  //No Error
id = 10   // Error
```



