# OS操作系统原理面经

线程是操作系统中运行的一个独立应用程序的实例，线程是进程内的一个执行单元

- 当全局路径和同级目录下有同名dll，程序会加载哪一个？（DLL 加载优先级问题）
1. 应用程序的可执行文件所在的目录：同级目录优先，因此，如果同级目录有同名的 DLL 文件，它会被首先加载。
2. 系统目录：System32 和 System 目录，通常是 C:\Windows\System32 和 C:\Windows\System。
3. 16 位系统目录：C:\Windows\System。
4. Windows 目录：C:\Windows。
5. 当前工作目录：即程序启动时的工作路径，但其优先级低于可执行文件所在目录。
6. 环境变量 PATH 中指定的目录：按 PATH 变量的顺序查找。