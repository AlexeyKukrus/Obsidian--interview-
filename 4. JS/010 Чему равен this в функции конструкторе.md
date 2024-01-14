**ОТВЕТ: 
	This в функции конструкторе равен новому экземпляру объекта который мы создаем при вызове функции

В конструкторах объектов, `this` ссылается на новый экземпляр объекта, который создается при вызове конструктора.
```javascript
function Person(name) {
  this.name = name;
  this.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const john = new Person("John");
john.greet(); // "Hello, my name is John"
```