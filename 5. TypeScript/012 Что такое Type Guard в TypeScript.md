
Type guard - это механизм в TypeScript, позволяющий выполнить проверку типов во время выполнения кода. Он позволяет более точно определять типы переменных и использовать функциональные блоки кода в зависимости от типов.

Существуют несколько способов реализации type guard'ов в TypeScript:

1. Проверка на тип typeof:
```TS
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

const example: unknown = 'Hello';

if (isString(example)) {
  // Внутри блока if TypeScript будет рассматривать example как строку
  console.log(example.toUpperCase());
}
```
2. Проверка на наличие свойства:
```TS
interface Car {
  model: string;
  year: number;
}

function isCar(object: unknown): object is Car {
  return 'model' in object && 'year' in object;
}

const vehicle: unknown = {
  model: 'Mercedes',
  year: 2020,
};

if (isCar(vehicle)) {
  // Внутри блока if TypeScript будет рассматривать vehicle как объект типа Car
  console.log(vehicle.model);
}
```
3. Использование оператора instanceof:
```TS
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof!');
  }
}

function isDog(object: unknown): object is Dog {
  return object instanceof Dog;
}

const pet: unknown = new Dog('Rex');

if (isDog(pet)) {
  // Внутри блока if TypeScript будет рассматривать pet как объект типа Dog
  pet.bark();
}
```

Type guard позволяют проводить более точные проверки типов и работать с переменными, имеющими конкретные типы, вместо неизвестного типа unknown или широкого типа any. Это улучшает безопасность, надежность и удобство использования кода.