## C/C++ 源文件的编译步骤

1. 预处理：宏定义展开，头文件展开，条件编译。
2. 编译：检查语法，生成编译文件。
3. 汇编：将汇编文件生成二进制目标文件。
4. 链接：将目标文件连接成目标程序。

![](..\picture\编译过程.png)

![](..\picture\编译过程2.png)

## 构建过程

![](..\picture\构建过程.jpg)

​	CMake 是一个构建生成器，提供了强大的领域特定语言(DSL)来描述构建系统应该实现的功能。这是CMake的主要优势之一，它允许使用相同的CMake脚本集生成平台原生构建系统。CMake软件工具集，使开发人员可以完全控制给定项目的生命周期：

- **CMake** 是描述如何在所有主要硬件和操作系统上配置、构建和安装项目，无论是构建可执行文件、库，还是两者都要构建可执行文件、库，还是两者都要构建。
- **CTest** 定义测试、测试套件，并设置应该如何执行。
- **CPack** 为打包需求提供DSL。
- **CDash** 将项目的测试结果在面板中展示。

CMake 管理的项目的工作流发生在许多阶段(time)，我们称之为时序。可以简洁地总结如下图：

![](..\picture\CMake时序图.png)

- **CMake time** 或 **configure time**，是 CMake 运行时的情况。这个阶段中，CMake 将处理项目中的 CMakeLists.txt 文件并配置它。
- **Generation time** 配置成功后，CMake 将生成本地构建工具所需的脚本，以执行项目中的后续步骤。
- **Build time** 这是在平台和工具原生构建脚本上调用原生构建工具的时候，这些脚本以前时由 CMake 生成的。此时，将调用编译器，并在特定的构建目录中构建目标(可执行文件和库)。
- **C Test time** 或 **test time**，运行项目的测试套件，以检查目标是否按预期执行。
- **CDash time** 或 **report time**，将测试结果上传到面板，与其他开发人员共享。
- **Install time**，将项目的目标、源文件、可执行文件和库从构建目录安装到安装位置。
- **CPack time** 或 **packaging time**，将项目打包以便发布，可以是源代码，也可以时二进制代码。
- **Package intall time**，在系统范围内安装新生成的包。

