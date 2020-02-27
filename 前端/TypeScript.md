##  TypeScript

1. 类型注解和编译时类型检查

2. 基于类的面向对象编程

3. 泛型

4. 接口

5. 声明文件

   ![image-20191112163753428](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112163753428.png) 

![image-20191112163819206](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112163819206.png)

![image-20191112163836287](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112163836287.png)

![image-20191112163849278](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112163849278.png)

![image-20191112165205102](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112165205102.png)

*函数重载：以参数数量或者参数类型区分 

```js
// 函数重载：多个同名函数，通过参数数量或者类型不同或者返回值不同
function info(a: { name: string }): string;
function info(a: string): object;
function info(a: any): any {
  if (typeof a === "object") {
    return a.name;
  } else {
    return { name: a };
  }
}
info({ name: "jerry" });
info("jerry");
```



![image-20191112165232878](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112165232878.png)

```js
//Vue项目@Props传递的参数@Props({}) 类型，是否必传，默认值，检验
  @Prop() private msg!: string; // 属性msg必填项，字符串类型
  @Prop({ default: "匿名" }) private foo?: string; // 属性foo必填项，字符串类型
export interface PropOptions<T=any> {
  type?: PropType<T>;
  required?: boolean;
  default?: T | null | undefined | (() => T | null | undefined);
  validator?(value: T): boolean;
}
```

```js
 // 普通的属性相当于组件data
  private features: Feature[] = [];

  // 生命周期
  async created() {
    //...
    const result = await getData<Feature>();
    this.features = result.data;
  }

  // 计算属性
  get featureCount() {
    return this.features.length;
  }
```

#### 多态

```js
//重写父类方法
class Shape {
  readonly foo: string = "foo";
  protected area: number;

  constructor(public color: string, width: number, height: number) {
    this.area = width * height;
  }

  shoutout() {
    return (
      "I'm " + this.color + " with an area of " + this.area + " cm squared."
    );
  }
}

class Square extends Shape {
  constructor(color: string, side: number) {
    super(color, side, side);
    console.log(this.color);
  }
  shoutout() {
    return "我是" + this.color + " 面积是" + this.area + "平方厘米";
  }
}
const square: Square = new Square("blue", 2);
console.log(square.shoutout());
```

存取器getter 和 setter 

```js
class Employee {
  private firstName: string = "Mike";
  private lastName: string = "James";

  get fullName(): string {
    return this.firstName + " " + this.lastName;
  }
  set fullName(newName: string) {
    console.log("您修改了用户名");
    this.firstName = newName.split(" ")[0];
    this.lastName = newName.split(" ")[1];
  }
}
const employee = new Employee();

employee.fullName = "Bob Smith";
```

![image-20191112172555781](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112172555781.png)

类型约束 ---接口

