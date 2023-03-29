---
title: "Notes"
---

<script>
  const deleteItems = [
    document.querySelector('.post-meta'),
    document.querySelector('.post-title'),
    document.querySelector('header'),
  ];
  deleteItems.forEach(dom => dom.remove());
  document.querySelector('main').style.padding = 0;
  document.querySelector('.post-body').style.transform = 'translateY(-4em)'
</script>

TS 描述 asycn 函数返回值，使用 Promise 泛型。

```ts
const asyncFn = async (): Promsie<number> => {
  return 100;
};
```
tuple明确指定数组每项的类型。
```typescript
Type Tuple = [string, number, string];
const items = ['first', 2, 'third'];
```


类型收窄
使用in操作符进行TypeNarrowing
```typescript
type First = {
	firstName: string;
};
type Second = {
	secondName: string;
};
type Name = First | Second;
const outputName = (content: Name) => {
	// 此处做类型收窄
	if ('firstName' in content) {
		return content.firstName;
	}
	return content.secondName;
}
```
Type assertion
重点在于isFish函数的返回值要写成`animal is Fish`，animal要与参数名一样
```typescript
type Fish = { swim: () => {} }
type Bird = { fly: () => {} }

function isFish(animal: Fish | Bird): animal is Fish {
	if ((animal as Fish).swim !== undefined) {
		return true;
	}
	return false;
}
function test(animal: Fish | Bird) {
	if (isFish(animal)) {
		animal.swim();
	} else {
		animal.fly();
	}
}
```

```typescript
import React from 'react';

interface CompoProps {
	thing: 'one' | 'two'
	children: React.ReactNode
}

const Compo = (props: CompoProps): React.ReactNode => {
	return <div>{props.thing}{props.children}</div>
}

interface CompoProps {
	thing: 'one' | 'two'
}

const Compo = (props: React.PropsWithChildren<CompoProps>): React.ReactNode => {
	return <div>{props.thing}{props.children}</div>
}
```

某个变量的值可以只为几个特定的字符串
```typescript
type Position = 'top' | 'bottom' | 'left' | 'right';

const getPosition = (position: Position): string => {
	return `Your position is ${position}`; 
}
```

interface继承
```typescript
interface People {
	age: number;
	sex: string;
}

interface Student extends People {
  score: number;
}

const tim: Student = {
  age: 18,
  sex: 'male',
  score: 69,
}
```

函数
```typescript
interface Test {
	(str1: string, str2: string): number;
}

type Test2 = (str1: string, str2: string) => number;

const test: Test = (str1, str2) => {
	return str1.length + str2.length;
}

const test2: Test2 = (str1, str2) => {
	return str1.length + str2.length;
}
```

交叉类型来结合两个interface
```typescript
interface One {
	one: string;
}

interface Two {
	two: string;
}

// 交叉类型
type OneAndTwo = One & Two;

// 通过继承多个interface来实现interface的结合
interface OneAndTwo extends One, Two {}
```


typeof
JavaScript中有typeof，Typescript也有。
```ts
const str = 'tim';
```
如果我们想获得str的类型
```ts
type TypeStr = typeof str;
```

![[Pasted image 20230126122651.png]]

如果此时我们声明一个对象，并且想获得这个对象的类型（也就是interface/shape)
```ts
const obj = {
	a: 'tim',
	b: 18,
	c: {
		d: true,
		e: 20,
	}
}

type IObj = typeof obj;
```
![[Pasted image 20230126122848.png]]