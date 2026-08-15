⚠️⚠️⚠️ 注 意 ⚠️⚠️⚠️
---
本项目暂未完工，请勿使用
---

# Yumo 窗口库

Windows独占的C++窗口库，设计上致力于效仿易语言

Yumo窗口库是一个重要的项目，其中的一些概念将会延伸到未来的编程语言项目中（当然，这种项目少说得等个五年）

下面是一段（概念性的）示例程序

```cpp
#include<yumo-win32>
/*
yumo window的每个参数值都采取类似rust的枚举
的风格，可以是一个指定的值或者是yumo::default_init、
yumo::auto_init，属于一个模板类的多种呈现状态
*/
using yumo::default_init;
using yumo::auto_init;
using yumo::color;

yumo::window mainWindow(
    L"演示窗口",200,100,
    default_init,default_init,
    color::white
);
yumo::element::label welcome(
    mainWindow,L"你好！这是Yumo Windows库的演示程序",
    yumo::auto_init,yumo::auto_init,
    20,10,color::white
);
// ...其他控件，不再演示（懒得写了）

void labelMouseMoving(int x, int y);

int yumoMain(const std::vector<std::wstring>& args) {
    // 其实是window.eventCallbackTable
    // 不过设计上考虑给个简写的选择
    welcome.ect.mouseMoving = labelMouseMoving;
    
    // 设计上想要让窗口启动后自动通知子组件
    mainWindow.start();
    
    yumo::runLoop();
    return 0;
}

void labelMouseMoving(int x,int y){
    // 默认输出到“./log.txt”
    yumo::log << L"moving！（"<< x << L"," << y << L"）\n";
}
```