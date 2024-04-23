# 1、在unity中实际做游戏

在前面，我们系统性地学习了大多数编程语言都会有的功能，包括：算术、函数、变量、赋值，数组/列表，类/结构体，条件判断语句，循环语句，等等。

在讲完了基础知识之后，下面来实际使用它们，看看真正的游戏制作是怎么样的。

***

以unity引擎为例，它用的语言是c#语言，属于c系语法，和python略有不同，但大部分一样。这一点具体看演示即可，基本上一理通百里明。

然后是游戏中最常使用的两个函数，游戏引擎提供给我们的api（下面的案例都是c#代码）：

```csharp
// 当物体被创建出来后调用一次，一个物体只会触发一次
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

```csharp
// 当物体被创建出来后调用一次，一个物体只会触发一次
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

