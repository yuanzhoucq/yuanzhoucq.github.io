# 译文 ｜ C++ 动态分配数组空间

> [https://www.learncpp.com/cpp-tutorial/6-9a-dynamically-allocating-arrays/](https://www.learncpp.com/cpp-tutorial/6-9a-dynamically-allocating-arrays/)

除了动态地为单个值分配空间外，我们也能动态地为数组变量分配空间。不像固定数组需要在编译时确定其规模，动态数组允许我们在程序运行的时候为数组指定长度。

要动态地为数组分配（和释放）空间，我们使用 `new` 和 `delete` 操作符：

```c++
#include <iostream>
 
int main()
{
    std::cout << "Enter a positive integer: ";
    int length;
    std::cin >> length;
 
    int *array = new int[length]; // use array new.  Note that length does not need to be constant!
 
    std::cout << "I just allocated an array of integers of length " << length << '\n';
 
    array[0] = 5; // set element 0 to value 5
 
    delete[] array; // use array delete to deallocate array
 
    // we don't need to set array to nullptr/0 here because it's going to go out of scope immediately after this anyway
 
    return 0;
}
```

因为我们在为数组分配空间，C++ 知道它应该使用数组版本的 `new` 操作符而不是它的普通标量版本。本质上，我们调用的是 `new[]` 操作符，尽管 `[]` 符号并没有紧跟在 `new` 之后。

需要注意的是，这里（为动态数组）分配的内存和平时为固定数组分配的内存不同，这里的数组长度可以非常大，你可以运行上面的程序，输入 1,000,000（甚至于 100,000,000）作为数组长度而不会出现任何问题。试一试吧！正因为这一点，需要分配大规模数组空间的 C++ 程序常常使用这种动态分配的方式。

## 动态地释放数组空间

当需要删除（空间并不会被删除，这里的删除实际上指的是空间被释放，占用空间的数据被删除——译注）一个动态分配的数组时，我们必须使用数组版本的 `delete` 操作符，也就是 `delete[]`。

它告诉 CPU 有多个变量而不只是一个变量需要被清除。新手程序员最常犯的错误之一就是在处理动态数组时使用 `delete` 而不是 `delete[]` 去删除它。使用普通标量版本的 `delete` 操作符去删除一个动态数组时，会引发未定义的行为，比如数据损坏（data corruption）、内存泄漏和程序崩溃等等。

关于 `delete[]` 人们经常会问，它怎么知道有多少内存需要被释放呢？答案是 `new[]` 操作符记录了被分配给动态变量的内存大小，所以 `delete[]` 能释放对应大小的内存空间。但不幸的是，这个大小不可以被程序员访问到。

## 动态数组几乎和固定数组相同

在课程 [6.8：指针和数组](http://www.learncpp.com/cpp-tutorial/6-8-pointers-and-arrays/) 中，我们已经知道了固定数组名保存了数组第一个元素的内存地址，它可以退化为一个保存着数组首元素的指针。在这种退化的形式下，数组的长度是不可用的（ `sizeof()` 返回的也不再是数组占用空间的大小），但是除此之外它和数组名本身几乎没有其他区别。 

一个动态数组本身作为指向其第一个元素的指针开始它的生命周期，因此，它也有上述同样的局限——不知道它自己的长度。一个动态数组和一个退化为指针形式的固定数组一样使用，只是程序员需要自己负责在合适的时候通过 `delete[]` 去释放它。

## 初始化动态分配的数组

如果你想把动态数组的元素全部初始化为 0，语法相当简单：

```c++
int *array = new int[length]();
```

但是在 C++11 之前，不存在快速把动态数组元素赋为非零值的方法（初始化列表只对固定数组有效）。这也就是说你必须遍历动态数组并为其元素显式赋值：

```c++
int *array = new int[5];
array[0] = 9;
array[1] = 7;
array[2] = 5;
array[3] = 3;
array[4] = 1;
```

太麻烦了！

幸好，从 C++11 开始，可以使用初始化列表为动态数组赋初值了：

```c++
int fixedArray[5] = { 9, 7, 5, 3, 1 }; // initialize a fixed array in C++03
int *array = new int[5] { 9, 7, 5, 3, 1 }; // initialize a dynamic array in C++11
```

注意，在动态数组的长度和初始化列表之间没有 `=`。

为了保持语言的一致性，在 C++11 中，固定数组也支持使用没有 `=` 的初始化方式了：

```c++
int fixedArray[5] { 9, 7, 5, 3, 1 }; // initialize a fixed array in C++11
char fixedArray[14] { "Hello, world!" }; // initialize a fixed array in C++11
```

另外还需要注意的是，动态数组必须要有显式声明的长度：

```c++
int fixedArray[] {1, 2, 3}; // okay: implicit array size for fixed arrays
 
int *dynamicArray1 = new int[] {1, 2, 3}; // not okay: implicit size for dynamic arrays
 
int *dynamicArray2 = new int[3] {1, 2, 3}; // okay: explicit size for dynamic arrays
```

## 调整数组长度

动态数组允许你在声明时指定其长度，但是，C++ 没有提供改变此长度的内置方法。你可以通过申请新数组，复制需要的元素，然后删除旧数组的方式绕过这个限制。但是，这种方法已经被证明是容易出错的，尤其是当数组元素是类类型的时候（它们在被创建的时候受特殊的规则管理）。

因此，我们建议你不要这样做。

幸运的是，如果你需要这个功能，C++ 在标准库中提供名为 `std::vector` 的数据结构，它是一个可调整长度的数组，我们（之后）会简要地介绍它。

---

译注：本文删去了原文中关于写作时 GCC 编译器的 bug 的讨论。