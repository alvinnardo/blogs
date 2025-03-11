---
title: Centos8 配置 C++20 环境
date: 2025-03-11 15:59:31
tags:
---



### 背景

- 在 Centos8 环境上测试 C++20 等标准库，发现系统是 gcc8 版本，不支持新标准，所以需要升级版本。

- 编辑器中的 clangd 环境需要相应配置。
  
  

### 具体操作及问题解决

1. 首先尝试 yum 源安装，在 centos7 上升级高版本是安装 devtoolset-x，但是在 centos8 上发现并没有。查询得知在 Centos8 上更改了名字，改为了 gcc-toolset-x。

```bash
sudo yum install gcc-toolset-11
source /opt/rh/gcc-toolset-11/enable
gcc --version
```

2. 在 cpp 测试文件中，引入 `<bit>` 头文件，并进行编译运行。

```bash
g++ test.cpp -std=c++20 && ./a.out
```

3. 在 neovim 中进行编辑时，报错 `<bit>` 头文件找不到 和 GLIBCXX20_CONSTEXPR 未定义的问题，所以需要配置编辑器中 clangd 的环境

```lua
return {
  cmd = {
    "/path/to/clangd",
    "--header-insertion=never",
  },
  init_options = {
    fallbackFlags = {
      "-std=c++20",
      -- <bit> 头文件在这个下面
      "-I/opt/rh/gcc-toolset-11/root/usr/include/c++/11",
      -- GLIBCXX20_CONSTEXPR 在这个文件夹下 bits/c++config.h 中定义
      "-I/opt/rh/gcc-toolset-11/root/usr/include/c++/11/x86_64-redhat-linux",
    },
  },
}
```

4. 遇到了 `no member named 'fenv_t' in the global namespace`的问题，在 GUN 官网上查询到问题，定义为 BUG。个人认为是 GUN 和 CLANG 两个厂家的产品有些地方不兼容，因为 GCC 可以编译，但是 clangd 报错。修改方式也在该页面 `https://gcc.gnu.org/bugzilla/show_bug.cgi?id=100017` 的 comment 12，以下是粘取的原文。

```git
Naive patch based on https://gcc.gnu.org/bugzilla/show_bug.cgi?id=100017#c7 gets my canadian crosses building. 

diff --git a/libstdc++-v3/include/c_compatibility/fenv.h b/libstdc++-v3/include/c_compatibility/fenv.h
index 0413e3b7c25..56cabaa3635 100644
--- a/libstdc++-v3/include/c_compatibility/fenv.h
+++ b/libstdc++-v3/include/c_compatibility/fenv.h
@@ -26,6 +26,10 @@
  *  This is a Standard C++ Library header.
  */
 
+#if !defined __cplusplus || defined _GLIBCXX_INCLUDE_NEXT_C_HEADERS
+# include_next <fenv.h>
+#else
+
 #ifndef _GLIBCXX_FENV_H
 #define _GLIBCXX_FENV_H 1
 
diff --git a/libstdc++-v3/include/c_global/cfenv b/libstdc++-v3/include/c_global/cfenv
index 0b0ec35a837..d24cb1a3c81 100644
--- a/libstdc++-v3/include/c_global/cfenv
+++ b/libstdc++-v3/include/c_global/cfenv
@@ -37,9 +37,11 @@
 
 #include <bits/c++config.h>
 
-#if _GLIBCXX_HAVE_FENV_H
-# include <fenv.h>
-#endif
+// Need to ensure this finds the C library's <fenv.h> not a libstdc++
+// wrapper that might already be installed later in the include search path.
+#define _GLIBCXX_INCLUDE_NEXT_C_HEADERS
+#include_next <fenv.h>
+#undef _GLIBCXX_INCLUDE_NEXT_C_HEADERS
 
 #ifdef _GLIBCXX_USE_C99_FENV_TR1
```



### 问题总结

经上述步骤，目前可以在 Centos8 上使用 C++20 等新标准库了，而且 neovim 编辑器的环境也重新配置好了，目前基本上没有其它问题。
