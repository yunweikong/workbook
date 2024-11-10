# cmake入门
推荐书籍：https://365.kdocs.cn/l/chDzFjAgchdM
https://www.kancloud.cn/csyangbinbin/cmake-cookbook1/2157909

### cmake简介
管理软件build过程的工具，它并不会直接build出软件可执行文件本身，而是制作出可以build出软件本身的全部工程文件，比如makefiles、msvc的工程文件，然后我们可以通过执行这些工程文件，完成最终的编译。 
- 为何要用cmake？
    - 跨平台代码，提供强大的泛用性
- cmake构建过程
    - 编写CMakeLists.txt
    - 生成平台相关工程文件：`cmake <source_dir> -B <build_dir> -G <generator>`
        - 源代码路径；构建系统的输出目录；指定生成的构建文件系统文件生成器"Unix Makefiles"/"Visual Studio 16 2019"...
        - 其他常用选项：`-D  <var>=<value>`: 这个选项用来设置 CMake 变量的值。例如`-DCMAKE_BUILD_TYPE=Release`设置构建类型为Release
    - 编译制作出的工程文件，得到最终结果文件：`cmake --build ...（平台相关的编译命令）`
```shell
## 文件夹结构
HelloWorldProject/
├── CMakeLists.txt
└── main.cpp
##
# 配置和生成项目
mkdir build
cd build
cmake .. -G "Visual Studio 16 2019"
# 在build文件夹中编译项目
cmake --build . --config Debug / cmake --build . --config Release
```

### cmake概念
- **目录树形结构**：通常，一个项目的代码会分布在多个文件和文件夹中，为了更好地组织这些文件，我们可以使用“目录树”来分层管理文件。
    - `add_subdirectory`：你可以在主目录的 CMakeLists.txt 文件中用 `add_subdirectory(src)` 把 src 目录（子文件夹）加到构建流程中；CMake就会自动去 src 目录找那里的 CMakeLists.txt，按照你在 src 的 CMakeLists.txt 中的指示去构建
- 对象：在CMake中，所有构建的内容都叫对象，主要有以下两种
    - **Target（目标）**：最终的生成物。在CMake中，我们使用 `add_executable` 或 `add_library` 来定义一个目标。生成目标时也会产生相应的配置文件
    - **File（文件）**：用作构建的文件
- 对象之间的关系
    - Target和Target之间的关系
        - `link_libraries`：假如 targetA 需要用到 targetB，你就需要把 targetB 加入到 targetA 的链接中，以保证 targetA 能正常找到 targetB 的代码。CMake用 `target_link_libraries(targetA targetB)` 处理这种依赖关系。
        - `dependencies`：有时候，你想确保 targetA 编译前 targetB 已完成编译，就可以在 targetA 上声明对 targetB 的依赖关系。这确保了编译顺序的正确性。
    - Target和File之间的关系
        - sources：用来把源文件与目标绑定。假设你定义了一个 `add_executable(HelloWorld main.cpp)`
    - File和File之间的关系
        - Custom Command：可以用自定义命令 `add_custom_command` 来生成新的文件
- Command规则（Custom Command）
    - File关联Command：`outputs`
    - Project关联Command：`PRE_BUILD(PRE_LINK), POST_BUILD`提供了在构建不同阶段插入操作的能力。

### cmake构建
- 指定 cmake 的最小版本
    - `cmake_minimum_required(VERSION 3.4.1)`
- 设置项目名称（如下）
    - 当你定义了项目名称之后，CMake 会自动生成以下两个变量
        - 二进制输出目录和源代码目录`demo_BINARY_DIR`,`demo_SOURCE_DIR`
        - 两个更通用的变量`PROJECT_BINARY_DIR`,`PROJECT_SOURCE_DIR`
```CMake
project(
    Demo 
    LANGAGES CXX C
    DESCRIPTION "My own game code"
    VERSION 0.1.0)
```
- `add_executable(<name> <options>... <sources>...)`
    - 生成的可执行文件的名称，并且也将用于在 CMake 中引用该目标。
    - 可以使用 -D 选项定义预处理宏，或者使用 -I 选项指定额外的包含目录等。
    - 可以是一个或多个源文件，可以包括 C、C++、汇编等类型的源文件

* set设定变量值是更好的选择
    * `set(CMAKE_CXX_STANDARD 11) // 设置使用 C++ 11 标准`
* `message([<mode>] "message text" [arg1 [arg2 ...]])`
    * 在 cmake 中打印相应的信息，常见的是STATUS普通模式

- 常用/好用的命令
```CMake
# CMAKE_CURRENT_SOURCE_DIR表示当前 CMakeLists.txt 文件所在的路径
set(SOURCES_FILE  ${CMAKE_CURRENT_SOURCE_DIR}/../Person/src/person.cpp)
# 设置头文件所在的目录路径
set(HEADER_DIR
    ${CMAKE_CURRENT_SOURCE_DIR}/../Person/include
)

# 设置默认构建类型为 Debug
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

# 将头文件路径添加到该目标的 include 路径中
target_include_directories(${PROJECT_NAME} PRIVATE ${HEADER_DIR})
# 显式添加头文件，使其在 IDE 中可见
target_sources(${PROJECT_NAME} PRIVATE ${HEADERS_FILE})
```

```shell
# 独立的命令行中进行编译时vcvars*.bat 来设置环境
call "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\VC\Auxiliary\Build\vcvarsamd64_x86.bat"
# 进入debug
mkdir Debug & cd Debug 
# 把代码构建xx.sln文件（指定目标架构为 x64；指定项目的 CMakeLists.txt 文件所在路径。）
cmake  -G "Visual Studio 16 2019"  -A x64 -DCMAKE_BUILD_TYPE=Debug ../PersonMain

# 利用msvc编译xx.sln 生成xx.exe
msbuild /m PersonMain.sln /p:Platform=x64 /p:Configuration=Debug
## /m：启用多线程编译，提高编译速度
## PersonMain.sln：指定要编译的 Visual Studio 解决方案。
##/p:Platform=x64：定义平台架构。/p:Configuration=Debug：定义构建配置为 Debug。
```

- `aux_source_directory(<dir> <variable>)`:发现所有文件
- `include_directories([AFTER|BEFORE] [SYSTEM] dir1 [dir2 ...])`:包含要指定的头文件
- `add_subdirectory(source_dir [binary_dir] [EXCLUDE_FROM_ALL])`:添加子文件


### 工程模板
我们可以通过工程模板来简化操作
```bat
mkdir Debug
cd Debug
call "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\VC\Auxiliary\Build\vcvarsamd64_x86.bat"
cmake -G "Visual Studio 16 2019" -A x64 -DCMAKE_BUILD_TYPE=Debug ../KDevelop-Training
@rem for %%i in (*.sln) do ... 遍历 Debug 目录中生成的所有 .sln 文件，并使用 msbuild 编译每个解决方案。
for %%i in (*.sln) do msbuild /m "%%i" /p:Platform=x64 /p:Configuration=Debug
cd ../
pause
```