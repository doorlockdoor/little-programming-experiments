# 基础语法

####

####

#### 6、数据类型

这一小节会简单一些，补充一点基础知识。

主要是为之后更复杂的例子做铺垫。然后大家准备好，从下一节开始，因为要加入了if语句，所以代码复杂度会开始加速，一些更贴合实际的案例会出现。

由于变量是绑定数据的，所以它也会有对应的数据类型。虽然计算机的底层是二进制，所有数据都是0101，但在实际使用过程中，不同的0101往往有不同的含义，例如图片、文档、音频等等。

在python中，有4种基础数据类型（其他大多数类型都是它们的排列组合）：

* **整数型**，**int**，例如1、24、-321。整数会用专门的整数运算器进行计算。
* **浮点型**，**float**，例如-0.1、3.14、192.98123。浮点数会用专门的浮点数运算器进行计算。评测cpu性能时主要就用到了32位浮点数（单精度浮点数性能），和64位浮点数（双精度浮点数性能）。
* **字符型**，**string**，例如"abc"，"中文字符也可以"，这一串字符也被称为字符串。字符串通常使用英文双引号括起来，表示双引号内部的都是文本。
* **布尔型**，**bool**，只包含true（真）和false（假）两种值。用来进行条件判断（后面我们会用到）。 在python中写法如下：

```python
name = "名字"
age = 10
height = 99.9
is_boy = True
```

也可以这么写：

```python
name: str = "名字"
age: int = 10
height: float = 99.9
is_boy: bool = True
```

在c/c++中它的写法类似于：

```c++
string name = "名字";
int age = 10;
float height = 99.9;
bool is_boy = true;
```

python可以不显式地写数据类型，而是交给编译器自动推断。而例如c/c++则必须显式书写类型，这主要是得益于近些年编译器技术的进步，使其可以灵活判断，在现代语言中，或多或少都会提供隐式书写类型的功能。

对于python来说，如果只是小型项目，可以不显式地写类型（由编译器推断）。但如果是大型项目，则强烈推荐把类型标注上，否则代码量庞大到一定程度，aabb是什么类型会非常混乱。

从代码规范上来说，显式书写类型是多人合作写代码的必要准则之一。

但就本教程而言，由于代码量非常少，所以可以不显式标注类型（也就是使用第一种写法）。

**6-1、练习题**

练习1：

```python
# 请书写一个角色卡，包含游戏昵称，等级，职业，主技能，角色高度，是否为人类等等。
```

练习2：

```python
# 请自行搜索python的各个基础数据类型是如何相互转化的。
```

#### 7、条件判断语句

本小节开始介绍前面提到的if条件判断语句。

除了常规的计算外，我们还有各种程序控制语句，包括条件分支、循环执行等。其实在写例子时也能感觉到，只有过程，而没有条件判断，其实做不了太繁复的事情，例如检测键盘输入、如果按下移动键、角色向前移动，如果玩家血量小于0、则触发死亡动画等等。

例如：

```python
key = input()
if key == "w"：
    print("玩家向前移动")

hp = 20
if hp <= 0:
    print("玩家死亡")
else:
    print("玩家血量健康")
```

它的语法规则是：

```python
if 判断表达式:
    如果为真，则执行这段代码
else:
    如果为假，则执行这段代码
```

判断表达式和算术表达式类似，只不过判断表达式只能返回true或false，其中我们需要用到比较符号：

* \==，等于
* !=，不等于
* \>=，大于等于
* <=，小于等于
* \>，大于
* <，小于 例如：

```python
# 新建变量
x = 10

# 可以只有if，没有else
if x != 10:
    print("x不等于10")

# 也可以既有if又有else，意为如果...否则...
if x == 10:
    print("x等于10")
else:
    print("x不等于10")
  
# 还可以是if-elif-else，如果...再如果...再如果...否则...
if x < 0:
    print("低于0分？")
elif x < 60:
    print("不及格")
elif x < 80:
    print("及格")
elif x < 90:
    print("优秀")
elif x <= 100:
    print("卓越")
else:
    print("突破100分？")

# 嵌套使用（注意缩进，同一缩进的为同一个代码块）（其实所有的语句都可以嵌套使用）
if x >= 10:
    if x >= 20:
        print("x大于等于20")
    print("x大于等于10")

# 也可以把判断表达式写在外面
flag = x >= 10    # 这里flag的数据类型是bool布尔类型，只有ture和false两种可能
if flag:
    print("判断为真")
else:
    print("判断为假")
```

除此之外还有逻辑运算符：

* and，并且
* or，或者
* not，取反

```python
x = 10
if x >= 0 and x <= 99:
    print("x大于等于0并且x小于等于99")
else:
    print("x小于0或者x大于99")

if x < 100 or x > 200:
    print("x小于100或者x大于200")
else:
    print("x大于等于100并且x小于等于200")

if not x == 10:
    print("x不等于10")
else:
    print("x等于10")
```

if语句的规则确实多，稍微看看就行了。

然后我们来实践一下， 稍微施加点魔法。

一个小游戏：随机扔一个0-99的骰子，然后用键盘输入一个数字，和骰子比大小。

```python
# 导入random代码库
import random

# 接收键盘输入值，并将键盘输入值（字符串类型）转化为数字（整数类型）
input_text = input()
input_number = int(input_text)

# 随机生成一个int整数，范围0-99
random_number = random.randint(0, 99)

# 键盘值和随机值比大小
if input_number < random_number:
    print(f"输入值{input_number}，比骰子小，骰子{random_number}")
elif input_number > random_number:
    print(f"输入值{input_number}，比骰子大，骰子{random_number}")
else:
    print(f"输入值{input_number}，和骰子相等，骰子{random_number}")
```

由于在线运行不支持实时检测键盘输入（可能是考虑到安全），所以我们使用提前输入框，将键盘猜测提前写在输入框内，然后运行代码，查看结果：

关于import导入代码库，random库的randint随机函数，内置的input输入函数、int整数转换函数等等，我们不会详细解释，遇到了搜索引擎问一下就行，由于python非常流行所以这方面的教程也非常多，不再赘述。

上面这个例子只能输入一次，和真实的游戏不太一样，下面我们给一个真实的案例。

如果各位本地装有vscode编辑器和python运行环境，则可以试试以下代码。因为是本地运行、所以可以实时检测键盘输入，并猜测骰子，更接近实际的游戏。

```python
# 导入random代码库
import random

# 随机生成一个int整数，范围0-99
random_number = random.randint(0, 99)

# 循环99次，一共99次机会
for i in range(99):
    # 每一次循环时，检测一次键盘输入
    input_number = int(input("请输入猜测的数字："))
    # 和骰子进行比较
    if input_number < random_number:
        print(f"比骰子小")
    elif input_number > random_number:
        print(f"比骰子大")
    else:
        print(f"和骰子相等，骰子{random_number}，数字{input_number}")
        print("猜中了！！")
        break
```

运行结果：&#x20;

**7-1、练习题**

练习1：

```python
# 已知input为官方自带的键盘输入函数。
# 请书写代码，实现以下功能：当输入w/a/s/d时，打印玩家向前/后/左/右移动。
```

练习2：

```python
# 已知导入随机数代码库为import random，随机数生成函数为random.randint(n, m)
# 接着上一个例子，设置玩家的初始坐标为x=0，y=0，然后用随机数生成一个随机坐标，其数值为-1到1之间的整数，例如x=1，y=-1；或x=0，y=1等等。
# 然后加入以下判断：当输入w/a/s/d时，玩家的坐标向前/后/左/右移动。并和随机坐标进行比较，是否相等，如果相等，打印到达坐标xxx；否则，打印与随机坐标之间的距离。
```

#### 8、复合类型与循环语句

在上一节的例子中，我们有一闪而过用到for循环语句。没有循环语句，我们就无法连续猜测骰子，因此本小节重点讲解它。

不过在讲循环之前，要先介绍一下复合数据类型。在之前的练习题中，不知道大家是怎么把那4颗树放在一起的（求最高的树和最低的树之间的差值），如果是10颗、100颗呢？显然，我们希望能有一个变量，直接引用那一堆数据，例如图片images=一堆东西，又例如树trees=一堆东西。这就是复合数据类型。

本次先介绍把一组相同类型的数据复合在一起的方法，称为数组/列表。

然后下一节会介绍把不同类型的数据组合在一起并抽象成一个对象的方法，称为结构体/类。

数组/列表：

```python
trees = [2.5, 8.53, 9.01, 14.15]
```

访问时如下使用：

```python
print(trees[0])    # 第一个数据
print(trees[1])    # 第二个数据
print(trees[2])    # 第三个数据
print(trees[3])    # 第四个数据
```

> 备注：这被称为下标索引，索引值程序员习惯从0开始，到n-1结束。索引值需要在其数组长度之内，超出长度会报错。

数组和列表在概念上的区别是：

* 数组一般是固定长度的一组数据，不能随意增删，例如一张1920\*1080的图片，像素点只能置零，不能删除或增加。
* 列表一般是可变长度的一组数据，可以增加和删除节点，例如音乐播放歌单，加入播放列表或移除歌曲。

当然，不同的语言有不同的实现原理，具体细节千差万别。本教程就笼统介绍，以数组/列表来统称这一复合类型，我们以介绍概念为主，不以具体的语言为桎梏。

然后我们还有一种更方便的访问一组数据的方式，那就是for循环（不同语言的for循环写法可能不一样，需要注意一下）：

```python
trees = [2.5, 8.53, 9.01, 14.15]
for i in trees:
    print(i)
```

实现的效果是，循环访问一个数组/列表。语法规则是：

```python
for 临时变量 in 数组/列表:
    依次访问数组/列表中的元素
```

随着语句越来越多，花样也越来越多。

例如我们可以实现这样的效果：

```python
# 自定义一个max函数
def max(numbers):
    result = numbers[0]
    for number in numbers:
        if number > result:
            result = number
    return result

# 使用它
foo = [0, 5, -20, 40, 13, 2]
print(max(foo))
```

我们自定义了一个max函数，虽然和原版的不太一样（它们使用了另外的功能），但效果是相同的，即找出一堆数据中最大的那一个。大家读一读这个max函数的实现，应该能读懂检测的逻辑。

如法炮制，我们可以制作不使用官方函数就完成所有自己练习题的例子（print函数除外）。这也算是一种去魅了，现在我们来剥离max和min的魔法：

```python
# 有4颗树，高度分别为2.5，8.53，9.01，14.15
# 请写一段代码，它的功能是：得出最高的树和最低的树之间的高度差，并计算在该差值内间隔1.5放置一个圣诞树灯泡，一共可以放置几个。

# 自定义一个max函数
def max(numbers):
    result = numbers[0]
    for number in numbers:
        if number > result:
            result = number
    return result

# 自定义一个min函数
def min(numbers):
    result = numbers[0]
    for number in numbers:
        if number < result:
            result = number 
    return result 

trees = [2.5, 8.53, 9.01, 14.15]
height = max(trees) - min(trees)
count = int(height / 1.5)
print(count)
```

**8-1、练习题**

练习1：

```python
# 已知官方内置的range函数可以生成数组/列表，用法是：
# range(0, 5)返回[0, 1, 2, 3, 4]
# range(10, 15)返回[10, 11, 12, 13, 14]
# range(5)等效于range(0, 5)，返回[0, 1, 2, 3, 4]
# range(10)等效于range(0, 10)，以此类推...

# 例如：for i in range(5):
#          print(i)
# 打印：0 1 2 3 4

# range函数和正常的函数没区别，它也可以嵌套变量，例如：
# n = 5
# for i in range(n):
#     print(i)
# 打印：0 1 2 3 4

# 请书写一段代码，功能是打印0-100内所有的奇数。（奇数可以用取余2时余数等于1来判断）
```

练习2：

```python
# 已知for循环是可以嵌套for循环的（其实所有的语句都可以嵌套）。
# 嵌套两层被称为双重循环，三层被称为三重循环。
# 在双重循环中，我们假设第一层循环变量为i、第二层循环变量为j，例如：
# for i in ...:
#    for j in ...:
#        ...
# 而在嵌套时，range等所有函数也是可以使用循环变量的，这是解题的关键。

# 请书写一个双重循环，功能是打印99乘法表，打印函数我们提前给出来是：
# print(f"{i} * {j} = {i * j}")

# 要求输出结果如下：
1 * 1 = 1

2 * 1 = 2
2 * 2 = 4

3 * 1 = 3
3 * 2 = 6
3 * 3 = 9

4 * 1 = 4
4 * 2 = 8
4 * 3 = 12
4 * 4 = 16

5 * 1 = 5
5 * 2 = 10
5 * 3 = 15
5 * 4 = 20
5 * 5 = 25

6 * 1 = 6
6 * 2 = 12
6 * 3 = 18
6 * 4 = 24
6 * 5 = 30
6 * 6 = 36

7 * 1 = 7
7 * 2 = 14
7 * 3 = 21
7 * 4 = 28
7 * 5 = 35
7 * 6 = 42
7 * 7 = 49

8 * 1 = 8
8 * 2 = 16
8 * 3 = 24
8 * 4 = 32
8 * 5 = 40
8 * 6 = 48
8 * 7 = 56
8 * 8 = 64

9 * 1 = 9
9 * 2 = 18
9 * 3 = 27
9 * 4 = 36
9 * 5 = 45
9 * 6 = 54
9 * 7 = 63
9 * 8 = 72
9 * 9 = 81
```

#### 9、对象

前面我们介绍了一组同类型的数据，数组/列表。现在我们来介绍一组不同类型的数据，并将其抽象为一个对象，称为结构体/类。

或许有读者会问，为什么上面这句话多了一句“并将其抽象为一个对象”，如果删掉它会怎么样。我们先看看只是把一组不同类型的数据放在一起的样子，能不能像这样摆放：

```python
list = ["文字", 123, 99.8, "文字2"]
```

答案是可以的，不同语言或多或少都支持类似功能的复合类型。但这种数据的实用意义不大，至少相比于真正常用的那些不大。

真正常用的其实是这种：

```python
character = Character(
    name = "小A",
    id = 123,
    height = 99.8,
    role = "弓箭手"
)
```

不同类型的数据之间往往有含义，而这些含义共同组成了一个对象，例如这里的角色，包含角色的姓名、角色的编号、角色的职业等等。各种数据并非独立存在，而是处于一个整体之中。这就是我们本次要介绍的复合数据类型：结构体/类。

不过在此之前，我们要解释【对象】这一概念，结构体/类也将是大家目前为止学到的最复杂的类型。

我们先提一个问题：假设有这样一个角色，他包含血量、攻击力、防御力，然后还具有攻击能力（函数）。接着我们创建两个角色，让这两个角色相互攻击，直到某一方死亡，得出胜利者。

有了以上需求，我们该如何写代码呢？

是长这样吗？

```python
def attack_character(hp, attack, defense):
    return hp - (attack - defense)
    
# 角色1
hp_1 = 20
attack_1 = 10
defense_1 = 5

# 角色2
hp_2 = 30
attack_2 = 15
defense_2 = 1

# 循环攻击直至出现胜利者
...
```

按照我们已学的知识点，确实只能这么摆，把一个角色的血量放一边，把另一个角色的血量放另一边。但这样的代码绝对说不上优美，也让人感觉哪里有什么地方不对劲。

到底是哪里不对劲呢？

和我们之前遇到的例子都不同，本小节有了一个新的事物——物体，或者叫对象（object）。在游戏中，多个物体之间的交互可以说是再正常不过，因此该问题非常现实。当我们把世界划分为一个个物体并尝试相互影响、修改时，我们就会遇到“如何描述物体”的问题。

解决方法在前面也有暗示：那就是复合类型。把若干小数据组合成一个大数据，我们不是在计算零散的血量和攻击，而是在计算角色A的血量、角色B的攻击、角色A的防御。而角色A有自己的各种数值，角色B也有他的数值，它们共享一个角色模板，区别在于参数不同。

这便是结构体/类，它们的内部会存储两个东西，一个是数据、一个是与数据绑定的名称，例如当我们访问角色的"姓名"时，它会指向数据"小A"。而更妙的是，它们不仅可以包含变量，还可以包含函数，函数也可以理解为绑定了一堆过程的名称，通过角色对名称的访问，我们不仅可以获得姓名，还可以获得行为。这一点将改变我们对复合类型的一般认知，因为它将迎来质变。

在结构体/类中，内置变量可以称为属性，内置函数可以称为方法。例如我们为角色增加一个内置函数，名为talk：

```python
# 声明一个类，名为Character
class Character:
    name: str
    id: int
    height: float
    role: str
    
    def talk(self):
        print(self.name)

# 实例化这个类，创建一个角色
character = Character()
character.name = "小A"
character.id = 123
character.height = 99.8
character.role = "弓箭手"

# 访问角色的属性（使用“.”操作符）
print(character.name)
print(character.id)
print(character.height)
print(character.role)

# 访问角色的方法（使用“.”操作符）
character.talk()
```

语法规则是：

```python
class 类名:        # 类名默认使用帕斯卡命名法，和变量名做区分
    属性1: 类型
    属性2: 类型
    def 方法1: ...
    def 方法2: ...

变量名 = 类名()      # 类的创建函数，该函数名与类名相同
变量名.属性          # 通过“.”点操作符访问类的属性和方法
变量名.方法
```

除此之外，它还可以增加构造函数，实现快速初始化：

```python
# 声明一个类，名为Character
class Character:
    name: str
    id: int
    height: float
    role: str
    
    # 官方的特殊函数，用来初始化
    def __init__(self, name, id, height, role):
        self.name = name
        self.id = id
        self.height = height
        self.role = role
    
    # 我们自定义的函数
    def talk(self):
        print(self.name)

# 使用构造函数快速地创建角色
character = Character(
    name = "小A", 
    id = 123, 
    height = 99.8, 
    role = "弓箭手"
)
print(character.name)
```

结构体/类是一种特殊的复合类型，它不仅可以内置变量、还可以内置函数。

因此【对象】相比于单独的数据，迎来了质变。

这就是面向对象思想的开始，将世界划分为一个个物体，这些物体拥有属性、拥有行为，无数的物体彼此相互交互，形成一个巨大的世界。关于更多面向对象的思维，我们会在下一节介绍，本小节仅举例一些基本案例。

现在我们来写一个实际的例子。例如之前7-1的练习题2，有一个坐标的案例，这个二维坐标其实就可以包装为一个整体、抽象为一个对象：

```python
# 已知导入随机数代码库为import random，随机数生成函数为random.randint(n, m)
# 接着上一个例子，设置玩家的初始坐标为x=0，y=0，然后用随机数生成一个随机坐标，其数值为-1到1之间的整数，例如x=1，y=-1；或x=0，y=1等等。
# 然后加入以下判断：当输入w/a/s/d时，玩家的坐标向前/后/左/右移动。并和随机坐标进行比较，是否相等，如果相等，打印到达坐标xxx；否则，打印与随机坐标之间的距离。
import random
import math

# 声明一个类
class Position:
    x: int
    y: int
    
    # 官方的特殊函数，用来初始化
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    # 我们自定义的函数，用来计算两个坐标之间的距离
    def distance(position1, position2):
        diff_x = abs(position1.x - position2.x)
        diff_y = abs(position1.y - position2.y)
        return math.sqrt(diff_x ** 2 + diff_y ** 2)
    
    # 我们自定义的函数，移动坐标
    def move(self, input_key):
        if input_key == "w":
            self.y += 1
        elif input_key == "s":
            self.y -= 1
        elif input_key == "a":
            self.x -= 1
        elif input_key == "d":
            self.x += 1

# 创建坐标
player_position = Position(0, 0)
random_position = Position(random.randint(-1, 1), random.randint(-1, 1))

# 移动
input_key = input()
player_position.move(input_key)

# 判断位置
distance = Position.distance(player_position, random_position)
if distance == 0:
    print(f"到达坐标{random_position.x, random_position.y}")
else:
    print(f"距离随机坐标还有{distance}")
```

**9-1、练习题**

练习1：

```python
# 已知在函数中传递复合类型时，我们会传递的它的引用，因此在函数内对复合类型的修改会同步影响到外部，而基本数据类型，例如int、float等等，内部的修改不会影响到外部。
# 例如：
# def attack(character, list):
#     character.hp = 1      # 不需要返回，即可影响数据本体
#     list[0] = 1           # 不需要返回，即可影响数据本体
# 
# def attack(hp):
#     return hp             # 基础数据类型传递拷贝，而不是引用，因此需要返回

# 自己写一个角色类，包含以下属性：血量、攻击力、防御力，包含以下方法：攻击敌人。
```

练习2：

```python
# 已知while循环的写法是：
# while 判断表达式:
#     如果判断为真，则一直循环
# 整体上和if语句类似

# 又知break关键字可以提前跳出循环，continue关键字可以提前开启下一次循环
# 适用于所有的循环语句，包括for、while还有其他，写法类似于:
# while x > 0:
#     if x == 1:
#         break
#     if x == 2:
#         continue

# 接着上面的练习1继续往下写，创建两个角色，加入循环和角色相互攻击，当双方血量大于0时循环继续，直至某一方的血量小于等于0，结束战斗，打印胜利者。
```

#### 10、面向对象与抽象

在看上一节的案例，以及做练习题时，不知道大家有没有这样的疑问：那就是多了对象这一种东西，代码行数好像变多了、也更复杂了，它的好处是什么呢？

如果我们写代码只是写50行100行，那加入结构体/类可能好处并没有那么大。

但现实中的项目动辄上万行，多的有几百万行。之前我们书写的所有例子和练习题，其实都严重偏离真正的项目，也和真实的游戏不一样，其中的一个关键区别就在于：它们的抽象程度不够。下面我们来为大家列举一个实际的例子，来看看为什么前面的例子“抽象程度不够”。

例如：

```python
# 我们有一个物体的坐标信息
class Position:
    x: float
    y: float
    z: float

# 然后我们还有一个物体的旋转信息
class Rotation:
    x: float
    y: float
    z: float
```

它们两者在结构上是一致的，其数学本质也相同，因此可以统一抽象为一个物体，那就是向量：

```python
class Vector3:
    x: float
    y: float
    z: float
```

下面我们来实际创建一个角色：

```python
class Vector3:
    x: float
    y: float
    z: float
    
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
    
class Character:
    name: str
    position: Vector3
    rotation: Vector3
    
    # 构造函数
    def __init__(self, name, position, rotation):
        self.name = name
        self.position = position
        self.rotation = rotation
    
    # 移动功能，在当前坐标上相加移动向量
    def walk(self, move_vector):
        self.position += move_vector

# 创建角色
character = Character(
    name = "A", 
    position = Vector3(0, 0, 0), 
    rotation = Vector3(0, 0, 0))

# 移动一步
character.walk(Vector3(1, 1, 1))
```

但此处又遇到了一个问题，那就是position是我们自定义的类型Vector3，是完完全全的白板类型。它没有加减乘除这些功能，因为我们没有写，所以计算机不知道怎么运行。如果你实际运行上面这段代码，会发现它会报错，错误就在第24行的“+=”操作符。

这就是在设计大量内容时我们会遇到的问题，每一个自定义类型一开始都是一张白纸，它们之间应该如何交互？每一个属性，每一个行为，我们都需要精心设计，就像是在编织一张巨大的网，哪一个节点要是没有与其他节点相连，它就会断开，出现错误。

为了解决这一问题，我们需要为向量增加加减功能：

```python
class Vector3:
    x: float
    y: float
    z: float
    
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
        
    def append(self, vector):
        self.x += vector.x
        self.y += vector.y
        self.z += vector.z

class Character:
    name: str
    position: Vector3
    rotation: Vector3
    
    # 构造函数
    def __init__(self, name, position, rotation):
        self.name = name
        self.position = position
        self.rotation = rotation
    
    # 移动功能，在当前坐标上相加移动向量
    def walk(self, move_vector):
        self.position.append(move_vector)

# 创建角色
character = Character(
    name = "A", 
    position = Vector3(0, 0, 0), 
    rotation = Vector3(0, 0, 0))

# 移动一步
character.walk(Vector3(1, 1, 1))
print(character.position.x)
print(character.position.y)
print(character.position.z)
```

向量加减，位置移动的功能有了。但好像显示向量还不方便，不过这里我们就不添加了，读者可以自行添加向量的显示函数。下面我们继续写例子。

创建一个角色系统，用来管理、访问所有的角色，新增一个游戏功能：让角色（npc）随机在地图中乱逛。

```python
class Vector3:
    ...

class Character:
    ...

class CharacterSystem:
    character_list: list
    
    # 创建角色
    def create(self, number):
        character_list = []
        for i in range(number):
            character = Character(
                name = name_library.random(), 
                position = Vector3(0, 0, 0), 
                rotation = Vector3(0, 0, 0)
            )
            self.character_list.append(character)
    
    # 按名字寻找角色
    def find(self, name):
        for i in character_list:
            if i.name == name:
                return i
        return None
      
    # 新增游戏功能，让角色（npc）随机在地图中乱逛
    def wander(self):
        for npc in character_list:
            x = random.randint(-1, 1)
            y = random.randint(-1, 1)
            z = random.randint(-1, 1)
            npc.walk(Vector3(x, y, z))

# 启动角色系统
character_system = CharacterSystem()
character_system.create(100)
character_system.wander()
```

下面增加一个动画系统，动画系统分为：角色拥有骨骼，骨骼拥有坐标和旋转信息，动画文件拥有骨骼的帧偏移数据。

当角色移动时，动画系统负责播放移动动画（动画效果）。

```python
# 向量
class Vector3:
    ...

# 骨骼
class Bone:
    position: Vector3
    rotation: Vector3
    # 根据数据适配骨骼节点
    def apply(self, data):
        ...

# 角色
class Character:
    ...
    bones: list
    
    # 适配骨骼
    def create_bones(self, bones_data):
        bones = []
        for data in bones_data:
            bone = Bone(Vector3(0, 0, 0), Vector3(0, 0, 0))
            bone.apply(data)
            self.bones.append(bone)
    
    # 移动功能，自动播放动画
    def walk(self, move_vector):
        self.position.append(move_vector)
        animation = animation_system.find("move")
        animation.play(self.bones)
        
# 角色系统
class CharacterSystem:
    ...
    def create(self, number):
        # 在创建角色时，创建骨骼
    
    def wander():
        # 在移动角色向量时
        for npc in character_list:
            x = random.randint(-1, 1)
            y = random.randint(-1, 1)
            z = random.randint(-1, 1)
            npc.walk(Vector3(x, y, z))  # 移动时自动播放动画

# 动画文件
class Animation:
    name: str
    time: float
    offset_data: list
    
    # 根据动画帧数据和目标骨骼，偏移变换节点
    def play(self, bones):
        init = bones.clone()
        current_time = 0
        for data in offset_data:
            for bone in bones:
                bone.apply(data)
            current_time += 1
            if current_time > time:
                break;
        bones = init

# 动画系统
class AnimationSystem:
    animation: list
    # 寻找对应名称的动画文件
    def find(self, name):
        for i in animation:
            if i.name == name:
                return i
        return None
```

然后我们还需要添加一个主系统，按照游戏帧渲染，一帧帧驱动角色系统的移动和动画系统的播放（帧播放），例如一些早期的主机游戏都是固定30帧执行游戏（逻辑运算）。不过这里就不举例了，实际上我们编写游戏时不需要从底层重新写，因为大部分功能现代的游戏引擎都准备好了。

此处仅为一个例子，就像搭建一张巨大的网，将每个节点一一连接。

在这之中我们只需要注意一点：那便是【复杂度的抽象】。

当我们设计出Vector3这一类时，向量其实还有加减、点乘、叉乘、单位向量、规范化等等功能，这些都归属于向量本身。就像是一个黑盒子，内部装有各种功能，而外人只要按照约定使用即可，无需关心它具体的数学公式是什么。例如：

```python
class Vector3:
    x: float
    y: float
    z: float
    
    def __init__(self, x, y, z): ...
    def append(self, vector): ...
    def dot(self, vector): ...
    def mul(self, vector): ...
    def normalize(self): ...
    def zero(): ...
    def one(): ...
```

同理，面对骨骼，动画文件，角色，角色系统，动画系统等等，我们也只需要关心他们暴露在外面的公共方法/属性，而不需要关心他们内部自己的实现。

```python
class Bone:
    def apply(self, data): ...
    
class Character:
    def create_bones(self, bones_data): ...
    def walk(self, move_vector): ...

class CharacterSystem:
    def create(self, number): ...
    def find(self, name): ...
    def wander(self): ...

class Animation:
    def play(self, bones): ...

class AnimationSystem:
    def find(self, name): ...
```

这就是通俗意义上的接口，也就是api的思想（Application Programming Interface），一种程序对接的约定。

它们构成了功能的基石，例如向量，后续无论是角色移动、旋转，还是播放动画（动画骨骼的移动和旋转），还是UI的弹窗、镜头的晃动、下落的雨雪等等，其底层都是已经封装好所有功能的向量。（当然，实际使用中我们会用别人写好的第三方库，它们更全面，但底层思想是一致的）

衍生开来，其实在访问操作系统的时候也是如此，在控制台输出信息，借用的就是操作系统提供的接口。这些接口就是一系列的函数，例如刷新窗口、传输字符等等。但我们不需要关心，因为python官方已经把它们封装为了一个简单的函数，print。

这样一层层的抽象，最终就构成了极其庞大的游戏引擎和各种基础功能。我们实际使用移动时，也不需要像本案例一样重复造轮子，而是直接用现成的坐标和旋转功能，需要完全自定义的也就是我们自己的玩法，例如攻击伤害、角色对话、ai行为、按键映射等等。

至此，我们所有基础内容的章节就结束了。下面是一些简单的练习题，然后下一大章就不再有练习了，直接现场演示在游戏引擎中编程，原理是相通的。

**10-1、练习题**

练习1：

```python
# 还记得最上面那个案例我们说显示向量不太方便吗，请在Vector3类中添加一个显示函数：
# 具体写法随意，目标是让Vector3类打印信息，例如：(1, 1, 1)
```

练习2：

```python
# 自己设计一个角色类Character、背包类Backpack、以及物品类Item，它们的关系为：
# 角色拥有背包，背包装载物品，物品拥有名称、坐标和旋转
# 角色拥有查看背包的功能view_backpack
# 背包拥有查看物品的功能view_item
# 物品拥有显示信息的功能print_info
# 请书写一段代码，创建角色、背上背包、塞入物品，最终触发角色查看背包，显示所有物品
```

### 小游戏

#### 1、在unity中实际做游戏

在前面，我们系统性地学习了大多数编程语言都会有的功能，包括：算术、函数、变量、赋值，数组/列表，类/结构体，条件判断语句，循环语句，等等。

在讲完了基础知识之后，我们来实际使用它们，看看真正的游戏制作是怎么样的。

我们以unity引擎为例，它用的语言是c#语言，属于c系语法，和python略有不同，但大部分一样。这一点具体看演示即可，基本上一理通百里明。

然后是游戏中最常使用的两个函数，游戏引擎提供给我们的api（下面的案例都是c#代码）：

```c#
// 当物体被创建出来后调用，一个物体只会触发一次
void Start()
{

}

// 此后游戏运行的每一帧，重复执行该函数
void Update()
{

}
```

这是unity引擎提供的基础功能，特殊函数Start和Update，由于游戏是每一帧循环执行，所以它的脚本也分为第一次执行和每一帧执行。这是最为基础的能力，没有这种生命周期函数（游戏运行的每一帧），我们就无法真正控制游戏。

具体的使用效果如下：

```c#
// 当物体被创建出来后调用，一个物体只会触发一次
void Start()
{
    // 实例化玩家
    Character player = new Character();
}

// 此后游戏运行的每一帧，重复执行该函数
void Update()
{
    // 获取玩家的上下左右操作（包括摇杆和键盘）
    float horizontal = Input.GetAxis("Horizontal");
    float vertical = Input.GetAxis("Vertical");
    
    // 如果有移动向量，则驱动玩家走路
    Vector3 moveVector = new Vector3(horizontal, 0, vertical);
    player.Walk(moveVector);
    
    // 如果按下F键，则触发角色对话
    if (Input.GetKeyDown(KeyCode.F))
    {
        player.Dialog();
    }
}
```

上述代码仅供示例，并不能直接运行，因为它还没有与游戏场景中具体的角色物体绑定，各个类也还没有实际编写。

但原理是相通的，下一节我们将实际演示游戏的运行画面。

#### 2、提问做什么小游戏，现场演示做完

在文档中写例子的话太长了，并且泛用性不够。

不如当场提问，想做什么小游戏，直接演示做完。除开美术表现，至少代码逻辑是一致的。简单的小游戏在2小时之内做完，视其逻辑复杂度决定（抛开美术的话），快的话十几分钟就行。

### 扩展阅读

#### 1、代码美学

[﻿【熟】代码美学：在代码中取名\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1nP4y1v7ww/?spm\_id\_from=333.788\&vd\_source=aa47e4add5d6bd0095815c6b15677bb4)

#### 2、三个问题

每当我们学习一门新的编程语言，也就是一门新的魔法咒语时，需要问3个问题：

* 一，构成它们的基本元素（primitives）是什么？
* 二，如何组合（combination）这些元素？
* 三，如何抽象（abstraction）这些元素为新的基本元素？
