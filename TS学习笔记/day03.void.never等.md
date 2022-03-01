
- any ：用于描述任意类型的变量，不作任何约束，编译时会跳过对其的类型检查
- unknown ：表示未知类型，即写代码的时候还不知道具体会是怎样的数据类型，不能执行 unknown 的变量的方法
- never ：永不存在的值的类型，常用于表示永不能执行到终点的函数返回值，例如抛出异常或函数中执行无限循环的代码（死循环）的函数返回值类型
- void ：表示无任何类型，没有类型，例如没有返回值的函数的返回值类型
```ts
// void
function func04(): void {
 console.log("我没有返回值");
}

// never
// 抛异常，抛出异常会直接中断程序运行，这样程序就运行不到返回值那一步了，即具有不可达的终点，也就永不存在返回了
function error(msg: string): never {
 throw new Error(msg);
}
// 死循环，同样程序永远无法运行到函数返回值那一步，即永不存在返回
function loopForever(): never {
 while (true) {}
}

// unknown
let any1: any = "1";
let any2: any = 1;
let unknown1: unknown = "2";
let unknown2: unknown = false;
let number1: number = 12;

any1 = unknown1;
any1 = any2;
any1 = null;
any1 = undefined;
any2 = number1;

unknown1 = any1;
unknown2 = number1;
any1.toString();
// unknown1.toString()
// number1 = unknown1;
```