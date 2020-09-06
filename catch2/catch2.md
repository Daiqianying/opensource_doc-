# Catch2

## 关键特性

* 快速且非常容易上手。只需下载catch.hpp，#include就可以了。
* 没有外部依赖性。只要你能编译C++11，并且有一个C++标准库就可以使用。
* 把测试用例写成，自注册的，函数或者方法。
* 将测试用例划分为若干部分，每个部分都是孤立运行的（不需要夹具）。
* 支持使用BDD风格的Given-When-Then部分以及传统的单元测试用例。
* 只有一个核心断言宏用于比较。标准的C/C++运算符被用于比较--但完整的表达式被分解，并且lhs和rhs值被记录下来。
* 测试使用自由形式的字符串来命名--不再使用符合语言规则的标识符

## 其他核心特性

* 可以对测试进行标记，以便于运行特定的测试组。
* 失败可以(有选择地)中断到 Windows 和 Mac 上的调试器。
* 输出通过模块化的记录器对象。包括基本的文本记录器和 XML 记录器。可以方便地添加自定义记录器。
* 为了与第三方工具(如 CI 服务器)集成，支持 JUnit xml 输出。
* 提供了一个默认的 main ()函数，但是您可以提供自己的函数进行完全控制(例如集成到您自己的测试运行器 GUI 中)。
* 提供了一个命令行解析器，如果您选择提供自己的 main ()函数，仍然可以使用该解析器。
* Catch 可以自我测试。
* 替代断言宏报告失败，但不中止测试用例
* 浮点容差比较是使用表达式 Approx ()语法构建的。
* 内部和友好的宏是孤立的，所以名称冲突可以管理

## 与gtest对比

## 示例集合

## BDD

```c++
#define CATCH_CONFIG_MAIN
#include "../../../single_include/catch2/catch.hpp"

enum class State {
    kOff,
    kOn,
};

class Switcher {
public:
    Switcher() {}
    ~Switcher() {}

    void initState( State s ) { _s = s; }
    State getState() const { return _s; }
    void Process( State s ) { _s = s; }

private:
    State _s = State::kOff;
};

SCENARIO( "Switch on tests", "[switch_button]" ) {
    Switcher s;
    GIVEN( "the switch is on" ) {
        s.initState( State::kOn );
        WHEN( "process on" ) {
            s.Process( State::kOn );
            THEN( "switch is on" ) { REQUIRE( s.getState() == State::kOn ); }
        }
        WHEN( "process off" ) {
            s.Process( State::kOff );
            THEN( "switch is off" ) { REQUIRE( s.getState() == State::kOff ); }
        }
    }
    GIVEN( "the switch is off" ) {
        s.initState( State::kOff );
        WHEN( "process on" ) {
            s.Process( State::kOn );
            THEN( "switch is on" ) { REQUIRE( s.getState() == State::kOn ); }
        }
        WHEN( "process off" ) {
            s.Process( State::kOff );
            THEN( "switch is off" ) { REQUIRE( s.getState() == State::kOn ); }
        }
    }
}
```

![BDD测试结果](BDD_Given-When-Then_testexample.jpg)
