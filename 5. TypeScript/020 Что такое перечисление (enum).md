Enum представляет собой некую смесь объекта и массива. При обращении к enum возвращается его индекс. Получать данные мы можем по значению, а также по ключу.
Все элементы enum по умолчанию нумеруются и нумерация начинается по порядку от 0

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
Directios.[0];    // 'Up'
Directions.[1];   // 'Down'
Directions.[2];   // 'Left'
Directions.[3];   // 'Right'
```

Также в enum мы можем задавать собственные индексы, что делает этот тип более гибким

```Typescript
enum Directions {
	Up = 2,
	Down = 4,
	Left = 6,
	Right
}

Directios.[2];    // 'Up'
Directions.[4];   // 'Down'
Directions.Left;  // 6
Directions.Right; // 7 - Присвоился по умолчанию от предыдущего индекса
```

Пример использования enum 

```Typescript
enum Links {
	youtube = 'https://youtube.com',
	vk = 'https://vk.com',
	google = 'https://google.com',
}

Links.vk       // 'https://vk.com'
Links.youtube  // 'https://youtube.com'
```
Результатом компиляции enum будет анонимная самовызываемая функция, которая конструирует объект, так как типа enum в JS нет

```javascript
var Links;
(function(links) {
	links[youtube] = 'https://youtube.com',
	links[vk] = 'https://vk.com',
	links[google] = 'https://google.com',
})(links || (links = {}));
```