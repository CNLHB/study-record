## Flutter

## List 列表

给for循环命名    fist: for()
String name = "flutter";
字符串拼接 ==> "String is $name ";
函数
1、定义参数
2、函数传参
3、函数返回值
4、函数默认返回值为 null
5、箭头函数（无返回值）
6、箭头函数（有返回值）
7、函数参数（可选参数）
8、函数参数（命名） {width: 20, height: 10}   
9、函数参数 赋默认值

异常捕获
1、
try{

} on  异常名{

}
2、
try{

} catch(){

}

3、
try{

} catch(e, s) {

}
4、
try{

} catch(e, s) {

} finally{

}
自定义异常
class DepositException implements Exception {

}
类
1、类的基础知识
2、构造函数
3、构造函数参数
4、定义构造函数

class Student{
    int id;
    String name;
    void study() {

    }
    void sleep() {
        
    }

}

 #### Scaffold容器

### Button

RaiseButton

flatButton

padding: EageInsets.all()

Row()行

摆放：横向摆放，纵向摆放

mainAxisAlignment: MainAxisAlignment.spaceEvenly   

crossAxisAlignment: CrossAxisAlignment.center  纵向  //stretch 拉伸

Column列

 mainAxisAlignment 

flex应用

自定义一个类，然后自己实现

对象形式

代码抽离

定义

```  Datas data;
Datas data;
DataCart(this.data);
```

```dart
//无状态 ，定义的状态在整个周期不会发生改变
//有状态，整个周期可以发生改变//生命周期
/** 
* initState()执行一次 
* Build() 可以重复执行  设置setState()是zhix
* DisPose() */
/**异步 
* Future.delayed(Duration(seconds: 3),(){}) 不阻塞代码 *
* async 
* await 
*/
```



http  ,List  Map  jsop数据转义

```dart
import 'dart:convert' as convert;
import 'package:http/http.dart' as http;

main(List<String> arguments) async {
  // This example uses the Google Books API to search for books about http.
  // https://developers.google.com/books/docs/overview
  var url = "https://www.googleapis.com/books/v1/volumes?q={http}";

  // Await the http get response, then decode the json-formatted responce.
  var response = await http.get(url);
  if (response.statusCode == 200) {
    var jsonResponse = convert.jsonDecode(response.body);
    var itemCount = jsonResponse['totalItems'];
    print("Number of books about http: $itemCount.");
  } else {
    print("Request failed with status: ${response.statusCode}.");
  }
}
```





路由以及路由传递参数

