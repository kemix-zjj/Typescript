##### 介绍

学 TypeScript 是不是就不需要学 JavaScript 了？

用大家公认的说法，Typescript是JavaScript的超集，你可以理解为，它是加了一身装备铭文的进化版 JavaScript。JavaScript 有的，它都有，而且做得更好。JavaScript 没有的，它也有，而且我是在很长一段时间内不会被 JavaScript 赶上的。

[CSDN 中关于ts的最详尽介绍](https://blog.csdn.net/Aria_Miazzy/article/details/105641241?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166173962716781683991840%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166173962716781683991840&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-105641241-null-null.142^v42^pc_ran_alice,185^v2^control&utm_term=typescript&spm=1018.2226.3001.4187)

[最好的 ts 教程](https://github.com/mqyqingfeng/learn-typescript)

##### 环境搭建

安装： npm install -g typescript

- 编译：tsc hello.ts

- 运行：node hello.js

可以直接运行ts文件的插件：ts-node

- 安装：npm install -g ts-node

- 运行：ts-node hello.ts

快速生成配置文件
- npm init -y 生成 package.json 文件

- tsc init 生成 tsconfig.json 文件

##### 静态类型

一旦定义，就不可以随意改变。且它继承了其身上绑定类型的所有属性。

```
// 如下count继承了number上的所有属性。
// count.Xxx Xxx为number的属性
const count: number = 1;
​
//自定义静态类型 -- 通过接口实现
//zhh继承了接口Kemix上的所有属性
interface Kemix {
    uname: string;
    age:number
}
const zhh: Kemix = {
    uname: '张哈哈',
    age:21
}
console.log(zhh.uname);
​
```

静态类型分为**基础静态类型**和**对象静态类型**。

###### 基础静态类型

number，string，null，undefined，boolean，void，symbol ...

```
//基础静态类型
const num: number = 918;
const myName: string = 'Kemix';
// 还有null,undefined,boolean,void,symbol...
```

###### 对象静态类型

类类型，数组类型，函数类型，对象类型

```
// 类类型
class Person{ }
const Kemix: Person = new Person()
​
// 函数类型:
// () => string 代表kkk是一个函数，且返回值是string类型
// = 赋值
// ()=>{} 以箭头函数进行赋值
const kkk: () => string = () => {
    return 'kkk'
}
​
// 数组类型：string[]代表Kemix是由字符串构成的数组
const Kemix: string[] = ['小张', '小咔', '小哈']
​
// 对象类型
// 第一个{}是对象类型 赋值于 第二个{}
const Kemix: {
    name: string,
    age:number
} = {
    name: '张哈哈',
    age:20
}
```

##### 类型注解和类型推断

类型注解（type annotation）与类型注解（type inference）

默认潜规则：能够推断出的不用类型注解，不能推断的要进行类型注解

（TS 能够自动分析变量类型，我们就不需要做什么了； TS 无法分析变量类型的话，我们就需要使用类型注解）

```
//类型注解：这里给sum注解类型为number
let sum: number;
sum = 123;

//类型推断：通过其的初始值进行类型推断出它是number
let sumInterface = 123;

//无法进行类型推断的时候，进行类型注解one和two
function getTotal(one: number, two: number) {
    return one + two
}
const total = getTotal(1, 2)
console.log(total);
```

##### 函数参数和返回类型的注解

```
// 1.函数的返回类型的注解 :number
function getSumNum(one: number, two: number) :number{
    return one + two
    // return one + two + '' 会报错
}
const SumNum = getSumNum(1, 2)
​
​
// 2.void代表无返回值
function sayHello(): void{
    console.log('Hello World');
    // return '' 会报错
}
​
//3. 当永远执行不完，返回值可以定为never
function erroFunction():never{
    throw new Error()
     //上面抛出错误，下面就不会编译运行了
    console.log('Hello World'); 
   
}
// 死循环 永远执行不完
function forNever(): never{
    while (true) {
        console.log('Hello,World');
    }
}
​
// 4.函数的参数是对象时，如何确定对象的属性类型？
// 当参数有两个的时候  :{one:number,two:number}
function add({ one, two }:{one:number,two:number}) {
    return one + two
}
const addNum = add({ one: 1, two: 2 })
​
// 但参数只有一个的时候  :{one:number}
function getNum({ one }:{one:number}) {
    return one
}
const one = getNum({one:1})
```

##### 数组类型注解的方法

```
// 数值数组
const numberArr: number[] = [3, 2, 1]
​
// 字符串数组
const stringArr: string[] = ['a', 'b', 'c']
​
// undefined数组
const undefinedArr: undefined[] = [undefined, undefined]
​
// 组合数组
const arr: (number | string)[] = [1, 'string', 2]
​
// 对象数组
const Kemix :{name:string,age:number}[]= [
    { name: '小张', age: 20 },
    { name: '小哈', age: 21 }
]
// 对象数组的优化  --- 使用类型别名 
//类型别名法1： type
type tc = { name: string, age: number }
const Kemix: tc[] = [
    { name: '小张', age: 20 },
    { name: '小柯', age: 21 }
]
// 类型别名法2：class
class sg {
    name: string;
    age: number;
}
const Kemix :sg[] = [
    { name: '小张', age: 20 },
    { name: '小柯', age: 21 }
]
```

##### 元组的使用和类型约束

元组是加强版的数组，但在实际开发中，运用不多。

```
// const person: (string | number)[] = ['zhanghaha', 28, 'teacher']  //这样不跑错，但实际上程序的逻辑出现错误

// 数组的类型注释
const person: (string | number)[] = ['zhanghaha', 'teacher', 28]  //正确
​
// 数组的plus版 -- 元组的出现
// 元组的类型注释
const person: [string, string, number] = ['zhanghaha', 'teachers', 20]
​
// 数据源数组CSV  -- 元组的实际应用  很少用
const Kemix: [string, string, number][] = [
    // 数据源 由元组组成的数组
    ['whh', 'students', 18],
    ['zhh', 'teacher', 28],
    ['zkk', 'teacher', 28] 
]
​
// 对象格式存储数据比较常见
// {
//     name: 'hahaha', work: 'kakka', age:20
// }
```

##### 初始接口 Interface

```
const screenResume = (name: string, age: number, skill: number) => {
    age < 24 && skill >= 90 && console.log(name + '进入面试')
    age > 24 || skill < 90 && console.log(name+'你被淘汰')
}
​
const getResum = (name: string, age: number, skill: number)=>{
    console.log(name + '年龄是' + age);
    console.log(name+'技能是'+ skill);
}
​
screenResume('张哈哈', 18, 98)
getResum('张苦苦', 19, 89)
```

 以上代码发现 screenResume 和 getResum 很多相似 此时需要用到接口interface

```
interface Girl {
    name: string;
    age: number;
    skill: number;
    // 可选选项 --> ?:
    saying?: number;
}
// 接口 interface 和 类型别名 type 很相似
// 不同：类型别名可以直接给它赋值一个字符串的（type Girl1 = string），
//但是接口只能以对象形式进行赋值的，传递的值必须是对象
​
const girl = {
    name: '张咔咔',
    age: 20,
    skill: 94,
    saying: 21
}
​
const screenResume = (girl: Girl) => {
    girl.age < 24 && girl.skill >= 90 && console.log(girl.name + '进入面试');
    girl.age > 24 || girl.skill < 90 && console.log(girl.name + '你被淘汰'); 
}
const getResum = (girl: Girl) => {
    console.log(girl.name + '年龄是' + girl.age);
    console.log(girl.name + '技能值是' + girl.skill);
    //有语言值属性，才进行如下打印输出
    girl.saying && console.log(girl.name +'语言值是'+girl.saying);
}
screenResume(girl)
getResum(girl)
```

```
interface LL {
    name: string;
    age: number;
    skill: number;
    // 可选选项 -- ?:
    saying?: number;
    // 直接写东西，而不受任何约束 propname 。且为可选的
    // propname:string 是代表属性名称是字符串类型 属性值是任意类型
    [propname: string]: any;
    say():string
}
​
// Teacher接口 继承 接口LL
interface Teacher extends LL{
    teach():string
}
​
// 类zhh 实现 LL接口
class zhh implements LL  {
    name='张哈哈'
    age=24
    skill=90
    say() {
        return '欢迎光临~'
    }
}
​
const ll = {
    name: '张咔咔',
    age: 20,
    skill: 94,
    saying: 21,
    // [propname: string]: any; 这里用sex代替
    sex: '女',
    say() {
        return "哈哈哈你好呀"
    },
    teach() {
        return "我来教你呀"
    }
}
​
const screenResumes = (ll: LL) => {
    ll.age < 24 && ll.skill >= 90 && console.log(ll.name + '进入面试');
    ll.age > 24 || ll.skill < 90 && console.log(ll.name + '你被淘汰'); 
}
const getResums = (ll: Teacher) => {
    console.log(ll.name + '年龄是' + ll.age);
    console.log(ll.name + '技能是' + ll.skill);
    ll.saying && console.log(ll.name + '语言值是' + ll.saying);
    ll.sex && console.log(ll.name + '性别是' + ll.sex);
    console.log(ll.say());
    console.log(ll.name + '教' + ll.teach());
    
}
screenResumes(ll)
getResums(ll)
```

##### 类的概念和使用

```
// 类的概念和使用
class Lady {
    content = '哈喽'
    sayHello() {
        return this.content
    }
}
​
// 父子关系 继承 extends
class Girl extends Lady{
    // 重写：即覆盖父亲中的方法
    // sayHello(): string {
    //     return 'Hi honey!'
    // }
    sayHello() {
        // super关键字是对父亲中的sayHello进行扩展
        return super.sayHello() + '，你好！'
    }
    sayLove() {
        return 'I love you'
    }
}
​
const goddess = new Girl()
console.log(goddess.sayHello()); //哈喽，你好！
console.log(goddess.sayLove()); // I love you
```

##### 类的访问类型：public protect private

报错：Property 'name' has no initializer and is not definitely assigned in the constructor.(属性'name'没有初始化式，也不会在构造函数中明确赋值。)

原因：

第一种，我们没有明确的设置或者指出本错误所需要的初始化方法或者构造方法。 

第二种，我们没有考虑好我们自己变量的类型究竟是否是string。（注意：undefined与string类型不是同一个类型）

解决：

-   你可以设置 strictPropertyInitialization:false 取消这个限制（不建议）
-   你也可以在构造器里面为变量赋予一个默认值(建议做法）
-   或者，如果你确定自己已经有了初始化方法 ,也许你是通过辅助方法或者依赖注入等动态引入（TypeScript只能处理静态分析） 你可以通过设置最新的修饰符来避免这个错误的抛出

如下解决：

```
//1、 运用 ! 前提是可以知道其为非空
class Person {
    name!: string;
}
const person = new Person()
person.name = 'jspang'
console.log(person.name);

//2、利用构造函数——1
class Person {
    name: string;
    constructor() {
        this.name = ''
    }
}
const person = new Person()
person.name = 'jspang'
console.log(person.name);

// 3、利用构造函数——2
class Person {
    name: string;
    constructor(name:string) {
        this.name = name
    }
}
const person = new Person('jspang')
console.log(person.name);

// 4、利用构造函数——3
class Person {
    constructor(public name:string) {}
}
const person = new Person('jspang')
console.log(person.name);
```

##### 类的构造函数

```
class Person{
    public name: string;
    constructor(name: string) {
        this.name = name
    }
}
//一般 new 出来的都是构造函数
const person = new Person('jspang')
console.log(person.name);
​
//上述代码简化成
class Person {
    constructor(public name:string){}
}
const person = new Person('jspang')
console.log(person.name);
```

**继承：extends**

```
class Person {
    constructor(public name:string){}  
}
class Teacher extends Person{
    constructor(public age: number) {
        // 子类中必须调用父类构造函数
        // 不论父类有没有构造函数，都要在子类中书写super()
        super('jspang')
    }
}
const teacher = new Teacher(18)
console.log(teacher.age);
console.log(teacher.name);
```

##### 类的Getter、Setter 和 static

```
//Getter 和 Setter
class Girl{
    // 类的内部属性一般用下划线表示
    constructor(private _age: number) { 
    }
    // get 实际上是一个属性
    get age() {
        return this._age-10  //可选择性地暴露真实情况。
    }
    set age(age: number) {
        this._age = age + 3
    }
}
​
const zhh = new Girl(28) //18
zhh.age =15  //8
console.log(zhh.age); 
```

```
// static 静态对象。可以直接获取，不需要通过Getter
class Girl{
    static sayLove() {
        return 'I love you!'
    }
}
console.log(Girl.sayLove());
```

##### 抽象类和只读属性的使用

继承抽象类的类必须实现抽象方法！！

```
// 抽象类 abstract
abstract class Girl{
    abstract skill()
​
}
class Waiter extends Girl{
    skill() {
        // 业务逻辑
        console.log('打野');
        
    }
}
class BaseTeacher extends Girl{
    skill() {
        console.log('打怪');
        
    }
}
class SeniorTeacher extends Girl{
    skill() {
        console.log('治疗');
    }
}
```

**只读属性：readonly**

```
// 只读属性
class Person{
    public readonly _name:string
    constructor(name: string) {
        this._name = name
    }
}
const person = new Person('jspang')
// person._name = '张哈哈'  会报错，因为_name是只读属性
console.log(person._name);
```

##### 配置文件

###### 初识 tsconfig.json文件

-   如何生成 tsconfig.json？`tsc -init / tsc`
-   如何将.ts文件生成.js文件？ `tsc demo.ts`

``` 
//tsconfig.json
// 编译开发的时候，去掉注释                 
    "removeComments": true,  
    
// 指定编译生成js的文件(可以使用通配符)
  "include": ["demo.ts"],
  "files":["demo.ts"]
  
  // 除了指定.ts文件，其他.ts文件都编译生成js的文件
  "exclude": ["demo.ts"],
```

###### 初识compilerOption

1. `"strict":true，` 一旦开启，代表.ts要严格书写

    ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7b8c38047b6d43c8805931b1a7847902~tplv-k3u1fbpfcp-zoom-1.image)

2. `"noImplicitAny": false`

    ```
    // "noImplicitAny": false  允许你的注解类型any不用特意声明
    function jspang(name) {
        return name;
    }
    ```

3. `"strictNullChecks": false`

    ```
    // "strictNullChecks": false 允许有null值出现
    const jspang: string = null;
    ```

4. `rootDir` 和 `outDir`

    ```
    //入口文件，存放.ts源文件                                
     "rootDir": "./src", 
    // 出口文件，存放编译后的.js文件
     "outDir": "./bulid", 
    ```

    (src中存放.ts源文件；build中存放编译后的.js文件。在终端执行tsc命令后会自动生成bulid文件夹)

5. `"sourceMap":true` ：源代码到编译代码的映射（生成的.js.map文件存放在build文件夹下）

6. `"noUnusedLocals": true` ：变量定义未使用，提示报错

7. `"noUnusedParameters": true`：方法定义未使用，提示报错

8. `"outFile": "./build/page.js" `： 将多个配置文件打包成一个单文件。同时要求` "module":"amd" `

9. 等等。但在实际开发中，该配置文件只有在项目刚刚开始的初始化配置才会使用到的，了解即可。

##### 联合类型和类型保护（类型守护）

**联合类型**：表示的值可能是多种不同类型当中的某一个。如`A | B`联合类型的某个值就`可能是 A 类型，也可能是 B 类型`。

还有一个叫字面量类型即是 JavaScript 基元类型具体的值。如`type China = 'China'; let country: China = 'China';`

**类型保护**：即一些表达式在运行时检查以确保在某个作用域的类型（如下4种）

**类型推断**：即类型断言，就像是一种类型转化，它把某个值强行指定为特定类型

###### 法1. as 类型断言

```
// 服务员
interface Waiter {
  anjiao: boolean;
  say: () => {};
}
// 技师
interface Teacher {
  anjiao: boolean;
  skill: () => {};
}
​
// 类型联合
function judgeWhoOne(person: Waiter | Teacher) {
  // person.say()  //报错，因为无法识别什么身份
  // 类型守护方法一：as 类型断言
  if (person.anjiao) {
    (person as Teacher).skill();
  } else {
    (person as Waiter).say();
  }
}
```

###### 法2. in

```
function judgeWhoTwo(person: Waiter | Teacher) {
  // 类型守护方法二：in
  if ('skill' in person) {
    person.skill();
  } else {
    person.say();
  }
}
```

###### 法3. typeof

```
function add(first: string | number, second: string | number) {
// 类型守护方法三：typeof
  if (typeof first === 'string' || typeof second === 'string') {
    // 字符串不能直接用+进行相加
    return `${first}${second}`;
  }
  return first + second;
}
```

###### 法4. instacnceof

```
class NumberObj {
  count: number;
}
function addObj(first: object | NumberObj, second: object | NumberObj) {
  // return first.count + second.count; 报错
  // 类型守护方法四：instanceof(只能用在类中的)
  if (first instanceof NumberObj && second instanceof NumberObj) {
    return first.count + second.count;
  }
  return 0;
}
```

##### Enum枚举类型

```ts
// 初中级程序员操作
const Status = {
   MASSAGE: 0,
   SPA: 1,
   BATH: 2,
 };
function getServe(status: any) {
   if (status === Status.MASSAGE) {
     return 'message';
   } else if (status === Status.SPA) {
     return 'SPA';
   } else if (status === Status.BATH) {
     return 'bath';
   }
 }
​
 const result = getServe(Status.BATH);
 console.log(`我要去${result}`);
 
​
// 高级程序员操作
enum Status {
  // 默认第一个元素初始值为0 ，也可以进行修改，要求从1开始索引值，即此时是MASSAGE = 1
  // 这里的常量是用数组进行存储的，即Status[1] = SPA
  MASSAGE,
  SPA,
  BATH,
}
function getServe(status: any) {
  if (status === Status.MASSAGE) {
    return 'message';
  } else if (status === Status.SPA) {
    return 'SPA';
  } else if (status === Status.BATH) {
    return 'bath';
  }
}
​
console.log(Status.MASSAGE); //1
console.log(Status.SPA); //2
console.log(Status.BATH); //3
​
console.log(Status[1]); //SPA
​
// const result = getServe(Status.BATH);
const result = getServe(1);
console.log(`我要去${result}`);
```

##### 泛型

###### 在函数中使用泛型

1.泛型的一般使用

```ts
// 普通需求
function join(first: string | number, second: string | number) {
  return `${first}${second}`;
}
// 可行的
const result = join('jspang', 1);
console.log(result);
​
// 特殊需求：此时要求必须指定传递的值为字符串 --> 使用泛型
function join<JSPang>(first: JSPang, second: JSPang) {
  return `${first}${second}`;
}
// 先用<JSPang>进行占位，在后续进行调用的时候再确认要传递的参数的类型
//join<string>('jspang', '.com');  //字符串类型
join<number>(1, 2); //数字类型
```

2.泛型在数组中的使用

```
// 参数是数组
// 第一种
// function myFun<T>(params: T[]) {
//   return params;
// }
// 第二种
function myFun<T>(params: Array<T>) {
  return params;
}
// 数组中是值是字符串类型
myFun<string>(['123', '456']);
```

3.  指定多种类型的泛型

```ts
function join<T,P>(first: T, second: P) {
  return `${first}${second}`;
}
join<number, string>(1, '2');
```

4.  泛型也支持类型推断，但不推荐

```
function join<T, P>(first: T, second: P) {
  return `${first}${second}`;
}
join(1, '2');
```

###### 在类中使用泛型

1.  基本使用

```
class SelectGirl {
  constructor(private girls: string[]) {}
  getGirl(index: number): string {
     return this.girls[index];
  }
}
 const selectGirl = new SelectGirl(['小张', '小哈', '小卡']);
 console.log(selectGirl.getGirl(1));
​
// 当要求既可以传递名字也可以传递数字 --> 使用泛型
class SelectGirl<T> {
  constructor(private girls: T[]) {}
  getGirl(index: number): T {
    return this.girls[index];
  }
}
// const selectGirl = new SelectGirl<string>(['小张', '小柯', '小卡']);
const selectGirl = new SelectGirl<number>([1, 2, 3]);
​
console.log(selectGirl.getGirl(1));
```

2.  泛型中的继承

```
// 1. 继承后必须有name属性
// 2. 此时的泛型是改为string类型，因为有属性name
// 3. 实例化的时候必须以 对象形式 进行初始化
//（因为接口只能以对象形式进行赋值的，传递的值必须是对象）
interface Girl {
  name: string;
}
class SelectGirl<T extends Girl> {
  constructor(private girls: T[]) {}
  getGirl(index: number): string {
    return this.girls[index].name;
  }
}
const selectGirl = new SelectGirl([
  { name: '小张' },
  { name: '小柯' },
  { name: '小卡' },
]);
console.log(selectGirl.getGirl(1));
```

3.  泛型中的约束

```ts
// 只能传递number或者string类型
class SelectGirl<T extends number | string> {
  constructor(private girls: T[]) {}
  getGirl(index: number): T {
    return this.girls[index];
  }
}
const selectGirl = new SelectGirl<string>(['小张', '小哈', '小卡']);
console.log(selectGirl.getGirl(1));
```
##### 命名空间(namespace)

- src/components.ts（子）

```ts
namespace Components {
 // export 进行暴露
  export class Header {
    constructor() {
      const elem = document.createElement('div');
      elem.innerText = 'This is Header';
      document.body.appendChild(elem);
    }
  }

  export class Content {
    constructor() {
      const elem = document.createElement('div');
      elem.innerText = 'This is Content';
      document.body.appendChild(elem);
    }
  }

  export class Footer {
    constructor() {
      const elem = document.createElement('div');
      elem.innerText = 'This is Footer';
      document.body.appendChild(elem);
    }
  }
}
```

- src/page.ts（父）

```ts
namespace Home {
  export class Page {
    constructor() {
      new Components.Header();
      new Components.Content();
      new Components.Footer();
    }
  }
}
```

在终端执行 tsc：将 ts文件编译成 js 文件。

如何将多个配置文件打包成单个文件，即将上述的 src/components.ts 和 src/page.ts 文件打包编译成 build/page.js？

在 tsconfig.json 中，开启`"outFile": "./build/page.js"` 且` "module":"amd" `即可。

- 入口文件 index.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- <script src="./build//components.js"></script> -->
    // 引入编译后的js文件
    <script src="./build/page.js"></script>
    <title>Document</title>
</head>

<body>
    <script>
        // 页面展示
        new Home.Page();
    </script>
</body>

</html>
```

子命名空间
```ts
namespace Components {
// 子命名空间
  export namespace SubComponents {
    export class Test {}
  }
  export class Header {
    // ...
  }

  export class Content {
    // ...
  }

  export class Footer {
   // ...
}
```

在浏览器的控制台上可以打印出 

输入：Components.SubComponents.Test

输出：class Test {         }


##### 用 parcel 打包 Typescript 代码

- parcel 安装： yarn add --dev parcel@next
- 在 package.json 文件中修改

```json
"scripts": {
    "test": " parcel ./src/index.html"
  },
```

- 在终端执行：yarn test
- 项目自动生成打包上线的dist文件且终端显示的地址即页面显示的东东。