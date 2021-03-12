---
title: C++库函数
date: 2020-02-18 19:53:55
tags: C++
---

# 类型转换
## string转数值
```c++
#include<string>
``` 
string和数值转换 | 转换类型
-|-
stoi(s,p,b) | 把字符串s从p开始转换成b进制的int
stol(s,p,b) | 把字符串s从p开始转换成b进制的long
stoul(s,p,b) | 把字符串s从p开始转换成b进制的unsigned long
stoll(s,p,b) | 把字符串s从p开始转换成b进制的long long
stoull(s,p,b) | 把字符串s从p开始转换成b进制的unsigned long long
stof(s,p) | 把字符串s从p开始转换成float
stod(s,p) | 把字符串s从p开始转换成double
stold(s,p) | l把字符串s从p开始转换成long double

## char*和char数组转数值

```c++ 
#include <cctype>
#include <cstdio>
#include <cstdlib>
``` 
字符串和数值转换 | 作用
-|-
atof(s) | 将字符串s[n]转换为双精度浮点型值。
atoi(s) | 将字符串s[n]转换为整型值。
atol(s) | 将字符串s[n]转换为长整型值。
strtod(s,*p,b) | 将字符串s[n]转换为b进制双精度浮点型值，到p停止,并报告不能被转换的所有剩余数字。
strtol(s,*p,b) | 将字符串s[n]转换为b进制长整值，到p停止,并报告不能被转换的所有剩余数字。
strtoul(s,*p,b) | 将字符串s[n]转换为b进制无符号长整型值，到p停止,并报告不能被转换的所有剩余数字。

## 数值转为字符串

(1) 用stringstream即可把多种数值类型转换为String类型的字符串

```c++ 
#include <string>
#include <sstream>
#include <iostream> 
using namespace std;
int main(){
    double a = 123.32;
    string res;
    stringstream ss;
    ss << a;
    ss >> res;
    cout<<res; 
    return 0;
}
``` 
(2) 用to_string转换

```c++ 
#include<iostream>
#include<string>
using namspace std;
int main(){
    string s;
    int a =30
    cout<<to_string(a)<<endl;
}
``` 

## 进制之间转换
(1) 10进制转2进制 bitset
```c++ 
#include<iostream>
#include<bitset>
using namspace std;
int main(){
    int c=121312;
    bitset<32> b = c;//将c转换为32位2进制数
    cout<<b<<endl;
}
``` 
(2) 16进制转换
```c++ 
#include<iostream>
#include<sstream>
#include<string>
#include<iomanip>
using namspace std;
string dec2hex(int i){
    stringstream ioss;
    string s_temp;
    ioss<< setiosflags(ios::uppercase)<<hex<<i;
    ioss>>s_temp;
    return s_temp;
}
``` 

```c++ 
#include<iostream>
#include<sstream>
#include<string>
#include<iomanip>
using namspace std;
unsigned int hex2dec(string str){
    unsigned int x;
    stringstream ss;
    ss << hex << str;
    ss >> x;
    return x;
}
``` 