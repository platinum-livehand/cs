## 构造函数

### 默认构造函数(Default Constructor)

默认构造函数是在对象创建时被调用的构造函数，它没有任何参数。如果你没有为类定义构造函数，编译器会提供一个默认构造函数。默认构造函数的作用是初始化对象的成员变量，确保对象在创建时处于一个合理的状态。

```c++
class MyClass {
public:
    // 默认构造函数
    MyClass() {
        // 进行成员变量的初始化工作
    }
};
```

### 带参数的构造函数(Parameterized Constructor)

带参数的构造函数允许在创建对象时传递参数，用于对对象的成员变量进行初始化。通过带参数的构造函数，可以在创建对象时传入不同的参数值，从而**创建具有不同初始状态的对象**。

```c++
class MyClass {
public:
    // 带参数的构造函数
    MyClass(int val) {
        // 使用传入的参数对成员变量进行初始化
    }
};
```

### 拷贝构造函数(Copy Constructor)

拷贝构造函数是用于在创建对象时以另一个对象的副本进行初始化。它通常用于对象之间的赋值和传递。**如果没有显式定义拷贝构造函数，编译器会提供一个默认的拷贝构造函数，它会执行浅拷贝（对于简单数据类型）或复制指针（对于指针成员变量）。**

```c++
class MyClass {
public:
    // 拷贝构造函数
    MyClass(const MyClass& other) {
        // 进行深拷贝或者复制指针
    }
};
```

### 移动构造函数(Move Constructor)

移动构造函数是C++11引入的新特性，用于将临时对象的资源转移到另一个对象，通常用于提高性能和避免不必要的拷贝。**移动构造函数接受一个右值引用作为参数，并将资源从右值参数“窃取”到新创建的对象中。**

```c++
class MyClass {
public:
    // 移动构造函数
    MyClass(MyClass&& other) noexcept {
        // 将资源从右值参数中移动到新对象中
    }
};
```

### 委托构造函数(Delegating Constructors)

委托构造函数允许一个构造函数调用同一个类的其他构造函数，从而避免代码重复。通过使用完美转发，我们可以更高效地在构造函数间传递参数。

```c++
class MyString {
public:
    template <typename... Args>
    MyString(Args&&... args) : _data(std::forward<Args>(args)...) {
    }

private:
    std::string _data;
};

int main() {
    MyString s1("Hello, world!"); // 调用 std::string 的构造函数
    MyString s2(s1); // 调用 std::string 的拷贝构造函数
    MyString s3(std::move(s2)); // 调用 std::string 的移动构造函数
}
```

