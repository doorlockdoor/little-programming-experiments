# 5-1、函数

在写前面的练习题时，代码功能一多，代码行数一多，好像又显得有些“拥挤”了。这是因为我们没有划分代码之间的功能，使得所有过程都挤在了一起。

而把过程分离成一个个模块，这就是函数。

如果说变量是把一个数据与一个名称绑定，那么函数就可以是把一堆过程与一个名称绑定在一起，并提供了输入和输出。我们也可以说，函数是对过程的抽象，例如：

```python
# 定义函数
def get_area(r):
    pi = 3.14
    area = pi * r * r
    return area

def get_price(hkd):
    return hkd * 0.92

# 使用函数
area = get_area(0.1)
cny = get_price(area * 2340)
print(cny)
```

<figure><img src="../.gitbook/assets/图片-20240422210643-mrxqicc.png" alt="" width="375"><figcaption></figcaption></figure>

语法规则为：

```python
# 定义函数
def 函数名(形参):
    过程
    return 返回结果

# 使用函数，其实就是我们前面提到的调用表达式
函数名(实参)
```

像前面例子中用到的max和min等官方内置函数，它们的def定义就写在内置模块中，程序运行后可以自动使用，不需要我们再重复定义一遍。如果想要引用更多别人写好的函数（功能），还可以引用官方库或第三方库，后文的条件语句章节有实际案例。

其中，函数在写法上也可以没有参数，例如get\_today()，或没有返回值，例如print()，或既没有参数也没有返回值，例如stop()等等。

而和前面的所有功能一样，函数内部也可以嵌套表达式和语句。而函数内部的变量被我们称为【局部变量】，名称和外部不冲突，当函数运行完成后它就会被释放（消失），因此最后我们需要把结果给return回去（如果需要返回值的话）。

例如：

```python
def get_today():
    return "2024/4/1"

# 接收函数的返回值（如果有），绑定到一个名称上，最后打印日期
today = get_today()
print(today)
```

又例如：

```python
def print_today():
    today = "2024/4/1"
    print(today)

# 没有返回值，直接触发函数
print_today()
```

<figure><img src="../.gitbook/assets/屏幕截图 2024-04-23 154235.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/屏幕截图 2024-04-23 154344.png" alt="" width="375"><figcaption></figcaption></figure>

**5-1、练习题**

题目1：

{% code overflow="wrap" %}
```python
# 现在我们再来实现一遍这个例子，加入函数，把各个代码功能划分清晰：
# 我们有4颗树，高度分别为2.5，8.53，9.01，14.15，我们需要在最高的树和最低的树之间（高度差），按照1.5的间隔放置圣诞树灯。每个球形灯泡的价格与其横截面面积有关，假设该灯泡半径为0.1，每1单位的横截面积的价格与一台港版任天堂ns主机的2340港元相当。请计算出我们一共需要几个灯泡，每个灯泡多少人民币，一共需要几人民币。
```
{% endcode %}

