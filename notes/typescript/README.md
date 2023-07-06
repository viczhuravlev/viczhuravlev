# TypeScript

## Types

### Unknown

Тип `unknown` является безопасной (с точки зрения типов) версией типа `any`.

### Never

Тип `never` является индикатором того, что функция выбрасывает исключение или прерывает выполнение программы:
```ts
function test(value: number): number | never {
  if(value === 1) return value + 1

  throw new Error('Ошибка!')
}
```

### Infer

> Ключевое слово `infer` позволяет выводить один тип из другого внутри условного типа.

```ts
const data =  [
  { name: 'First addon', id: 1 },
  { name: 'Second addon', id: 2 }
];

type UnpackArray<T> = T extends (infer R)[] ? R : T

type DataType = UnpackArray<typeof data> // { name: string, id: number }
```

## Tricks with types

### Type assertion (утверждение типа)

```ts
unknownValue as Function
```

### Type guard (предохранитель типа)

```ts
if (typeof unknownValue === 'string') unknownValue.toString()
```

### Type predicates (предохранителя типа)

```ts
function isUser(value: any): value is User {
  return 'username' in value;
}
```

### Assertion function (функции-утверждения)

> Существует специальный набор функций, выбрасывающих исключения, когда происходит что-либо неожиданное.

```ts
function isNumber(value: any): asserts value is number {
  if (typeof value !== 'number') throw Error('Переданное значение не является числом!')
}
```


## Links:

* [Заметка о полезных возможностях современного TypeScript](https://my-js.org/blog/ts-features/#%D1%82%D0%B8%D0%BF-unknown)
