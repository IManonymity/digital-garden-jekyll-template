---
title: overview of compiler
date: 2022-12-31, 17:33:33
tags: compiler
book: Engineering a compiler
---

[page-27](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=26&x=337&y=232&id=12&uuid=a6b7dc0d58d5aa8dd1c84bacfe2a7234)

编译器按照处理顺序分为三部分：前端、中端和后端：
- 前端的作用是处理源程序，并生成IR表示
- 中端对IR表示进行优化
- 后端将IR转换到具体机器所能识别的语言

[page-33](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=32&x=330&y=262&id=19&uuid=69dd411a8a350d53827268cfe07a16b0)

编译器的一般图示结构为：
- ![assets/images/编译器结构.png](/assets/images/编译器一般结构.png)


[page-34](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=33&x=207&y=160&id=20&uuid=cb866ff7791f95c110c519401d2af752)

编译器各部分的图示结构：
- ![assets/images/编译器结构.png](/assets/images/编译器具体结构.png)

