---
title: "Install LLDB-mi in ubuntu 20.04"
summary: Install LLDB-mi in ubuntu 20.04
date: 2022-09-26
series: ["LLDB"]
weight: 1
aliases: ["/install_lldb_mi"]
tags: ["rust", "lldb"]
author: "baysao"
---

## Install the following packages via apt
```
sudo apt install clang-10 llvm-10-dev liblldb-10-dev
Create soft links for executable files so things can work as expected
sudo ln -s /usr/bin/clang-10 /usr/bin/clang
sudo ln -s /usr/bin/clang++-10 /usr/bin/clang++
sudo ln -s /usr/bin/lldb-10 /usr/bin/lldb
```
This one is a bit strange but VSCode only looks for the name `lldb-server-10.0.0` but not `lldb-server-10`
```
sudo ln -s /usr/bin/lldb-server-10 /usr/bin/lldb-server-10.0.0
Build the lldb-mi executable from source
git clone https://github.com/lldb-tools/lldb-mi.git
cd lldb-mi
cmake .
cmake --build .
sudo cp src/lldb-mi /usr/bin/
```

