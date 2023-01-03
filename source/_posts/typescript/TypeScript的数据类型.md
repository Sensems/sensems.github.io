---
title: TypeScript的数据类型
date: 2022/3/5 16:47:36
cover: https://s2.loli.net/2023/01/03/yaCgTcBLzJk1672.png
categories:
  - TypeScript
tags:
  - TypeScript
  - 数据类型
---

# TypeScript的数据类型

> 变量一但定义了某个数据类型后就不允许赋值其他数据类型的数值了


## 基础数据类型

### number

### string

### boolean

### void

### null

### undefinded

### any (使用 TS 时不建议使用 any 类型)

```typescript
// 声明类型时如果不指定类型或者不赋值,则 ts 解析器会自动判断变量为 any 类型
let d; <=> let d: any;

// any 类型还可以赋值给任意类型的变量
let s: string;
s = d // 这时候是成立的
```

### unknown

```typescript
// 声明类型时如果不指定类型或者不赋值,则 ts 解析器会自动判断变量为 any 类型
let un: unknown;

// any 类型还可以赋值给任意类型的变量
let s: string;
s = un // 这时候是不成立的
// 由于 un 是 unknow 类型的(未知类型数值), 是不能赋值给 string 类型的

// unknown 实际上就是一个类型安全的 any
// unknown 类型的变量不能直接赋值给其他类型的变量,可以间接实现
if (typeof un === 'string') {
  s = un; // 由于先进行了类型判断, 所以这时候赋值是成立的
}
```

### enum(枚举类型)

```typescript
// 使用场景
enum Gender {
  male,
  female
}

let p: { name: string, gender: Gender }
p = {
  name: '林丹',
  gnder: Gender.male
}
```

## 引用数据类型

### array

### object

```typescript
// 基础的定义方式
// 由于在 js 中几乎万物皆是对象,所以不推荐这样使用
let o: object
o = {}
o = function

// 可以用字面量的方式
let o1: { name: string, age: number }
o1 = { name: 'hanler', age: 12 }

// 如果要可选常数则在常数后面加个问号
let o2: { name: string, age?: number }
o2 = { name: 'hehe' }

// 当你需要一个固定值, 但是又需要其他值且不清楚数量的时候可以像以下定义
/**
 * @param {string} propsName 这个是属性名, 后面的 string 代表的是 string 格式的属性名
 * 中括号后面的 string 代表的是属性(propsName)的值的格式
 * */
let o3: { name: string, [propsName: string]: string }
o3 = { name: 'str', age: '12' }
```

## 类型断言

> 可以用来告诉 ts 解析器变量的实际数据类型


```typescript
let un: nuknown;
un = 'string'

let s: string;

s = un; // 此时是不成立的
// 由于 un 是 unknow 类型的(未知类型数值), 是不能赋值给 string 类型的

// 由于此时的 un 确实是 string 类型,我们可以使用类型断言来告诉解析器 un 就是 string 类型的来解决解析器报错问题

// 两种写法
s = un as string;
s = <string>un;
```
