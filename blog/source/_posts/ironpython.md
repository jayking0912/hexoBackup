---
title: ironpython3 安装
date: 2017-09-19 20:48:51
tags: vs python
---



VS2013安装 ironpython3，没有教程，全程摸索

git clone --recurse https://github.com/IronLanguages/ironpython3

一定要加 recurse

然后 用vs2017打开，生成 ironpython 在debug下

将其中 ipy文件所有目录文件考到文件夹下

设置 ipy所在的环境 （我的电脑属性-高级设置-系统环境）

创建项目 添加两个引用

Ironpython.dll 和 microsoft.scripting.dll

调用。py前

using IronPython.Hosting;
using Microsoft.Scripting.Hosting;

例子

static void Main(string[] args)

​        {

​            try

​            {

​                ScriptEngine engine = Python.CreateEngine();

​                ScriptScope scope = engine.CreateScope();

​                ScriptSource script = engine.CreateScriptSourceFromFile(@"text.py");

​                var result = script.Execute(scope);

​            }

​            catch (Exception e)

​            {

​                Console.WriteLine(e.Message);

​            }

​            Console.Read();

​        }

text.py放项目 debug目录下