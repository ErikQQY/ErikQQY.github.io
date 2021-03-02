---
tags: C++
---
# 关于C语言中的cin.get()和cin.getline()

C++中istream类中有两个接受键盘输入的函数，即get()和getline()成员函数想笔者这样的小白也许会在下面的代码的运行中感到困惑：

```C++
#include<iostream>
int main()
{
    using namespace std;
    const int ArSize=20;
    char name[ArSize];
    char dessert[ArSize];
    cout<<"Enter your name:\n";
    cin.get(name,ArSize);
    cout<<"Enter your favorite dessert:\n";
    cin.get(dessert,ArSize);
    cout<<"I have some delicious "<<dessert;
    cout<<" for you,"<<name<<".\n";
    return 0;
}
```
才刚打入名字程序就结束了 :frowning:？？？？  
其实，这就涉及到了get()和getline()方法的区别了  
<!--more-->
cin.get()把<kbd>Enter</kbd>键生成的换行符留在了计算机的输入队列中  
cin.getline()把<kbd>Enter</kbd>键生成的换行符从输入队列中删去了  
从而导致在第二次`cin.get()`时读到了'\n'导致系统认为有一个空行直接跳过了去  
知道getline()方法的问世，才是的输入方式更加简洁  

```C++
#include<iostream>
int main()
{
    using namespace std;
    const int ArSize=20;
    char name[ArSize];
    char dessert[ArSize];
    cout<<"Enter your name:\n";
    cin.getline(name,ArSize);
    cout<<"Enter your favorite dessert:\n";
    cin.getline(dessert,ArSize);
    cout<<"I have some delicious "<<dessert;
    cout<<" for you,"<< name<<".\n";
    return 0;
}
```
当然如果执意要用get()方法的话，可以在get方法后再来一个get方法,起缓冲作用，缓冲掉'\n'

```C++
#include<iostream>
int main()
{
    using namespace std;
    const int ArSize=20;
    char name[ArSize];
    char dessert[ArSize];
    cout<<"Enter your name:\n";
    cin.get(name,ArSize).get();
    cout<<"Enter your favorite dessert:\n";
    cin.get(dessert,ArSize);
    cout<<"I have some delicious "<<dessert;
    cout<<" for you,"<< name<<".\n";
    return 0;
}
```