# Dart 101: ทำความรู้จักภาษาDartฉบับโปรแกรมเมอร์

ปี 2011 กูเกิลได้เปิดตัวภาษาโปรแกรมตัวใหม่ชื่อว่าภาษา Dart (เวอร์ชันแรก)

โครงสร้างของภาษา DART คล้ายกับ C/C++ และ Java โดยที่จะมีความเป็นภาษาแบบ Structure Programming แต่ก็ยังมีความสามารถแบบภาษาประเภท Object Oriented Programming ด้วย นั่นคือมี `class` และ `inheritance` ให้ใช้งาน

เป้าหมายของการสร้างภาษา Dart ขึ้นมา กูเกิลบอกว่าอยากสร้างภาษาเชิงโครงสร้างที่ยืดหยุ่นมากพอ (structured yet flexible language) และเป็นการออกแบบตัวภาษาไปพร้อมกับตัว Engine สำหรับรันภาษาเลยเพื่อแก้ปัญหาโปรแกรมทำงานช้าและกินmemory ซึ่งเป้าหมายของภาษา Dart คือเป็นภาษาที่เรียนรู้ง่าย และทำงานได้บนอุปกรณ์พกพาขนาดเล็ก มือถือ ไปจนถึงserver

> ในตอนนี้ Dart มีออกมาแล้ว 2 เวอร์ชันคือ Dart1 และ Dart2, ในบทความนี้จะพูดถึง Dart2 เป็นหลัก

หากต้องการลองเล่นภาษา Dart ดู สามารถเข้าไปดาวน์โหลดตัว installer ได้ที่ [dart.dev](https://dart.dev/get-dart)
หรือลองเขียนภาษา Dart แบบ online เลยได้ที่ [DartPad](https://dartpad.dartlang.org/)

## Hello World!

ตัวอย่างโปรแกรมของ Dart นั้นหน้าตาคล้ายๆ กับภาษา C มาก ถ้าใครเคยเขียนภาษา C หรือภาษาตระกูล C มาก่อน (เช่น C++, C#, Java) จะคุ้นกับ syntax พวกนี้ทำให้เรียนรู้ได้ไม่ยาก

Dart เป็นภาษากลุ่ม Compiler นั่นคือจำต้อง Compile ก่อนเอาโปรแกรมไปรัน ไม่เหมือนภาษากลุ่ม Script ที่ใช้ interpreter ในการรันตัว source code ตรงๆ

```dart
void main(){
    print("Hello World!");
}
```
ตัวโปรแกรมจำเริ่มทำงานที่ฟังก์ชัน `main` เป็นหลัก เราไม่สามารถเขียน statement นอกฟังก์ชันได้

การแสดงผลมาตราฐานจะใช้คำสั่ง `print` (คำสั่งนี้ auto-newline เสมอนะ)

เรื่องหนึ่งที่ควรจำคือภาษา Dart นั้นการเขียน `;` (semi-colon) ไม่ใช่ optional คือ**จำเป็นต้องใส่ ; ทุกครั้งหลังจบ statement** ไม่สามารถละ `;` ได้แบบภาษาตระกูล C ยุคใหม่ๆ เช่น JavaScript หรือ Kotlin

## Comment
การใส่คอมเมนท์ทำได้เหมือนภาษา C ทุกอย่างคือ
1. `//` สำหรับ inline comment
2. เปิดด้วย `/*` และปิดด้วย `*/` สำหรับ multi-line comment (ไม่สามารถ nested ได้นะ)

```dart
int x; //ตั้งแต่ตรงนี้ไป เป็นส่วนของคอมเมนท์

/*
    ในนี้
    ทั้งหมด
    เป็นคอมเมนท์
*/
```

## Variable และ Data Type
 type | คำอธิบาย | ตัวอย่าง
---|---|---
`int` | เลขจำนวนเต็ม | 0, 1, -5, 86400
`double` | เลขทศนิยม | 0.0, 0.1, 0.14, -12.34
`bool` | ค่าทางตรรกศาสตร์ | true, false
`String` | สายอักขระ (ประโยค) | 'hello world!', "This is a book" <-- ในภาษา Dart สามารถใช้ได้ทั้ง `"` (double quote) และ `'` (single quote)
`dynamic` | ตัวแปรชนิดเปลี่ยนแปลงได้ | 1, 0.14, true, 'Hi!'

ตัวแปรของ Dart ทั้งหมดเป็นแบบ reference type ทั้งหมด ทำให้สามารถมีค่าเป็น `null` ได้ทั้งหมด

```dart
int x;
double d;
bool isDone;
String name;

//ตัวแปรทั้งหมดมีค่าเป็น null เพราะยังไม่ได้กำหนดค่า
```

แต่ใน Dart ยังมีชนิดของตัวแปรแบบพิเศษ ซึ่งไม่จำเป็นต้องประกาศ type เลย แต่ตัวภาษาจะ auto assign ชนิดของตัวแปรให้เอง

 type | คำอธิบาย
---|---
`var` | เป็นการละ type เอาไว้ให้โปรแกรมกำหนดให้ (ตาม value)
`final` | เหมือน `var` แต่ไม่สามารถเปลี่ยนแปลงค่าได้
`const` | ค่าคงที่

**ข้อแตกต่างระหว่าง `dynamic` vs `var` คือ**

`dynamic` เป็นการบอกว่าตัวแปรนี้ เก็บค่าชนิดไหนก็ได้ เปลี่ยนแปลงได้เรื่อยๆ (หากใครเคยเขียนภาษา script น่าจะคุ้นกัน) แน่นอนว่าการใช้ dynamic มีความเสี่ยงทำให้เกิด runtime error! ได้เพราะ Compiler ไม่สามารถช่วยเช็กชนิดของตัวแปรได้เลย

`var` จะเป็นการกำหนดชนิดตัวแปรในจังหวะที่ประกาศตัวแปร โดยดูชนิดตัวแปรจาก value ตอนนั้นเลย หลังจากนั้นตัวแปรจะถูกกำหนดเป็น type นั้นไปตลอด ไม่สามารถเปลี่ยนแปลงได้แล้ว

```dart
dynamic d = 1;      // ตอนนี้ค่า d เก็บค่า int
d = 'new value!';   // Ok! ค่า d เปลี่ยนไปเก็บค่า String แทน
d = true;           // Ok! ค่า d เปลี่ยนไปเก็บค่า bool แทน

var v = 1;          // สร้างตัวแปร v ซึ่ง value ในด้านขวาเป็น int ดังนั้นจะมีผลเท่ากับการเขียนว่า int v = 1; นั่นเอง
v = 'new value';    // Error: A value of type 'String' can't be assigned to a variable of type 'int'
```

**ข้อแตกต่างระหว่าง `final` vs `const` คือ**

`final` เป็นการกำหนดว่าตัวแปรนี้ ไม่สามารถเปลี่ยนแปลงค่าได้ กำหนดค่าแล้วกำหนดเลย (immutable) ซึ่งเป็นตัวแปรประเภท runtime ดังนั้นเราสามารถกำหนดค่า final จากตัวแปรหรือฟังก์ชันอื่นได้

`const` เป็นการประกาศค่าคงที่ โดยค่าที่กำหนดให้จะต้องเป็น literal เท่านั้น (เช่น 10, 'value') เพราะเป็นตัวแปรที่กำหนดค่าตั้งแต่ตอน compile-time

```dart
int x = 10;

final int f1 = 1;       //กำหนดตัวแปร int ให้เป็นค่าคงที่
final f2 = 'final-val'; //ใช้เหมือน var คือไม่กำหนด type ก็ได้
final f3 = x + 20;      //กำหนดค่าจากกโดยคำนวณมาจากตัวแปรอื่นอีกที

const int c1 = 1;       //กำหนดตัวแปร int ให้เป็นค่าคงที่
const c2 = 'const-val'; //ใช้เหมือน var คือไม่กำหนด type ก็ได้
const c3 = x + 20;      //Error: Not a constant expression. เพราะ x เป็นตัวแปรที่ value มาตอน runtime ไม่สามารถกำหนดให้ const ได้

```
## Math Operation
การใช้ `+`, `-`, `*`, `/` และ `%` เหมือนกับภาษาอื่นๆ แต่มีข้อควรระวังที่ตัว `/`

สำหรับภาษาอื่นถ้าเรานำ `int / int` ผลที่ออกมาจะได้เป็น `int` แน่นอน แต่สำหรับ Dart นั้นการหารจะได้ค่าออกมาเป็น `double` เสมอ
```dart
int x = 4 / 2;        // Error: A value of type 'double' can't be assigned to a variable of type 'int'.

int y = (int)(4 / 2); // Error: case แบบภาษา C ไม่ได้ด้วยนะ
```
วิธีการแก้คือใช้ operation `~/` คือการหารแล้วปัดจุดทิ้ง หรือใช้คำสั่ง `as` หรือจะใช้คำสั่ง `toInt()` ก็ได้
```dart
int x = 4 ~/ 2;             // Ok! แบบนี้ได้
int x = 4 / 2 as int;    // Ok! แบบนี้ได้
int x = (4 / 2).toInt();    // Ok! แบบนี้ได้
```
**คำเตือน!** ระวังสับสนกับคำสั่ง `int.parse()` กับ `int.tryParse()` ที่ใช้แปลง String --> int, เราไม่สามรถใช้ 2 คำสั่งนี้ในการแปลง double --> int ได้นะ


## String Concatenate การต่อสตริง
การต่อสตริงใช้เครื่องหมาย `+` เหมือนภาษาทั่วๆ ไป แต่ก็มีข้อควรระวัง (อีกแล้ว!) คือไม่สามารถต่อสตริงกับตัวแปรที่ไม่ใช่สตริงได้!
```dart
int x = 100;
print('x is ' + x);     // Error: A value of type 'int' can't be assigned to a variable of type 'String'.
```
เราจะต้องแปลงตัวแปรที่ต้องการจะต่อสตริงให้เป็น String ซะก่อน หรือทำ String Interpolation ซะก่อน โดยใช้ตัว `$` เพื่อระบุว่าตรงนี้เป็นตัวแปร (ถ้ามี expression ด้วยให้ครอบด้วย `${}`)

```dart
int x = 100, y = 200;
print('x is ' + x.toString());     // x is 100
print('x is $x');                  // x is 100
print('x is ${x}');                // x is 100

print('x + y is ${x + y}');        // x + y is 300
```

## Null Handling

ตัวแปรใน Dart เป็นแบบ reference ดังนั้นเลยสามารถเป็นค่า `null` ได้ทุกตัวเลย ภาษาDartเลยมี operation สำหรับจัดการค่า `null` พวกนี้มาให้เราใช้งานด้วย

### `??` Null Coalescing
เป็นการเช็กว่าตัวแปรตัวนี้ ถ้ามีค่าเป็น `null` ให้ใช้ค่า default ที่กำหนดให้แทน
```dart
output = input ?? defaultValue;

// เป็น short-hand ของ...

if (input != null) {
    output = input;
} else {
    output = defaultValue;
}
```
เช่น
```dart
int number = ...;

int x = number ?? 1; // กำหนด x = number แต่ถ้า number เป็น null ให้กำหนด x = 1 แทน
```


### `?.` Null Conditional
หากตัวแปรของเราเป็น object ซึ่งสามารถเรียกใช้งาน method ต่างๆ ได้ ... แต่ถ้า object ตัวนั้นเป็น `null` ก็จะเกิดปัญหา Null Pointer Exception ได้
```dart
object?.action();

// เป็น short-hand ของ...

if (object != null) {
    object.action();
}
```
เช่น
```dart
class People{
    void sayHi(){ print("hi!"); }
}
void main(){
    People people = ...;
    people?.sayHi();    // ถ้า people เป็น object ก็จะมีการปริ้นค่า "hi!" ออกมา แต่ถ้า people เป็น null คำสั่งนั้นก็จะไม่ถูกสั่งให้ทำงานเลย
}
```


### `??=` Null Coalescing Assignment
หากไม่ชัวร์ว่าตัวแปรตัวนั้นเป็น `null` รึเปล่า สามารถใช้ `??=` กำหนดค่า default ลงไปได้
```dart
variable ??= defaultValue

// เป็น short-hand ของ...

variable = variable ?? defaultValue;

// หรือใช้ Ternary Operator

variable = variable != null ? variable : defaultValue;

// หรือเขียนแบบ if-else

if (input == null) {
    output = defaultValue;
}
```

## Flow Control
### if-else
```dart
if (condition) {
    // TODO
} else {
    // TODO
}
```
### switch case
```dart
switch (command) {
  case 'PENDING':
    executePending();
    break;
  case 'APPROVED':
    executeApproved();
    break;
  case 'DENIED':
    executeDenied();
    break;
  default:
    executeUnknown();
}
```
**ข้อควรระวัง!** switch ในภาษา Dart ต้องมี `break` ตอนจบ case ทุกครั้ง ถ้าไม่ใส่ลงไป โปรแกรมจะไม่หยุดทำงาน แล้วรันคำสั่งบรรทัดต่อไปต่อเลย
### Loop: while, do-while
```dart
while (!isDone()) {
  doSomething();
}

do {
  printLine();
} while (!atEndOfPage());
```
เมื่อภาษาทั่วๆ ไป มีตัวcontrolเสริมคือ `break` และ `continue` ให้ใช้งานด้วย

### Loop: for
```dart
for (var i = 0; i < 5; i++) {
  print(i);
}
// output: 0 1 2 3 4
```
หรือใช้งานแบบ for-each สำหรับวนลูปทุก element ใน list
```dart
var numbers = [0, 1, 2, 3, 4];
for (var number in numbers) {
  print(number);
}
// output: 0 1 2 3 4
```

## Function
การสร้างฟังก์ชันในภาษา Dart มี syntax เหมือนภาษา C แต่สามารถละ type ทิ้งไปได้

เช่น
```dart
int add(int x, int y) {
    return x + y;
}

// สามารถเขียนย่อได้ว่า

add(x, y) {
    return x + y;
}
```
### Arrow Function
และหากเคยเขียนภาษา JavaScript มา มีหลายครั้งที่เราสร้างฟังก์ชันที่มี return statement เดียวเท่านั้น เราก็สามารถเขียนย่อโดยใช้ Arrow Function ได้ ... และแน่นอน Dart ก็ทำได้เหมือนกัน โดยใช้ `=>`
```dart
int add(int x, int y) {
    return x + y;
}

// สามารถเขียนย่อได้ว่า

add(x, y) => x + y;
```
### Optional Parameter
เราสามารถกำหนดค่าเริ่มต้นให้ parameter ได้โดยใช้ `[]` ครอบ parameter ที่อยากประกาศให้เป็น optional
```dart
int add(int x, [int y = 1]) {
    return x + y;
}

add(10, 20);    // result: 30
add(10);        // ไม่เซ็ตค่า y, ดังนั้น y = 1 result: 11
```

### Named Parameter
บางกรณี การสร้างฟังก์ชันที่มี parameter เยอะมาก ตอนที่เรียกใช้ฟังก์ชันอาจจะงงเรื่องลำดับตัวแปรได้
```dart
int setConfig(
    String basePath,
    String appPath,
    int retry,
    int maxThread,
    String defaultController
) {
    // TODO
}

setConfig("/", "/app", 10, 4, "Main");
```
ในกรณีนี้เราสามาร้ถตั้งชื่อ parameter แต่ละตัวได้ โดยใช้ `{}`
```dart
int setConfig({
    String basePath,
    String appPath,
    int retry,
    int maxThread,
    String defaultController
}) {
    // TODO
}

setConfig(
    basePath: "/", 
    appPath: "/app", 
    retry: 10, 
    maxThread: 4, 
    defaultController: "Main"
);
```
ซึ่งตัว parameter ทั้งหมด สามารถสลับตำแหน่งกันได้

**ข้อควรระวัง!** ตอนประกาศฟังก์ชันต้องมี `{}` ครอบตัวแปร แต่ตอนเรียกใช้งานฟังก์ชัน ห้ามใส่ `{}` ลงไปนะ

การใช้งาน Named Parameter จะถือว่าเป็น optional ทั้งหมด (แปลว่าไม่ใส่ค่าก็ได้) ซึ่งก็จะได้ค่าเป็น `null`

หากต้องการให้เวลาเรียกใช้งานฟังก์ชัน จำเป็นต้องใส่ค่านั้นลงไปเสมอจะต้องใช้ annotation `@required` เข้ามาช่วย

ซึ่ง `@required` นั้นอยู่ใน package ชื่อ `meta` ที่ต้องติดตั้งเพื่อก่อนจะใช้งาน โดยการเพิ่ม dependency ในไฟล์ `pubspec.yaml`
```yml
dependencies:
  meta: ^1.1.8
```
เวลาใช้งานก็...
```dart
import 'package:meta/meta.dart';

int setConfig({
    @required String basePath,
    @required String appPath,
    int retry,
    int maxThread,
    String defaultController
}) {
    // TODO
}
```
แบบนี้หมายความว่า parameter `basePath` และ `appPath` นั้นจำเป็นต้องใส่ทุกครั้งที่เรียกใช้งานฟังก์ชัน

## First Class Function
ตามสไตล์ภาษาสมัยใหม่ เราสามารถจับฟังก์ชันใส่ตัวแปรได้
```dart
int getNumber() => 123;

void main(){
    var func = getNumber;   // ไม่ใช่ getNumber() นะ,ไม่มี () 
    print(func());          // output: 123
}
```
หรือเราจะกำหนดว่าตัวแปรฟังก์ชันจะเป็น type อะไรและมี parameter อะไรบ้างก็ได้
```dart
void func1(){ ... }
int func2(){ ... }
String func3(int x){ ... }

void main(){
    void Function() f1 = func1;
    int Function() f2 = func2;
    String Function(int) f3 = func3;
}
```
และยังใช้ได้กับ method อีกด้วย เช่น
```dart
class People{
    String sayHi() => "Hi!";
}

void main(){
    People p = People();
    String Function() f = p.sayHi;
    print(f());     // output: Hi!
}
```

# สรุป
บทความนี้ได้แนะนำภาษา Dart ซึ่งเราจะเห็นว่าภาษานี้นั้นให้อารมณ์เหมือนภาษาตระกูล C ที่มีการปรับอะไรให้เป็นภาษาสมัยใหม่มากขึ้น แต่ก็ยังไม่ทิ้งความเป็น Structure Language อยู่ 

หากใครเขียน C หรือ Java ว่าน่าจะพบว่ามันมีความคล่องตัวในการเขียนมากขึ้น แต่ถ้าเอาไปเทียบกับภาษายุคใหม่อย่างเช่น Kotlin อาจจะมีอะไรขัดใจอยู่บ้าง

ในบทต่อไปเราจะมาดู Data Structure ในภาษา Dart กันต่อ
