---
title: 2.2 Regular expression
date: 2022-12-31
tags: compiler
book: Engineering a compiler
---


[page-59](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=58&x=329&y=107&id=7&uuid=eaf051f6a0fb30a21fe89eac6f5eb339)

>The set of words accepted by a finite automaton,$F$, forms a language,denoted $L(F)$. The transition diagram of the FA specifies, in precise detail, that language. It is not, however, a specification that humans find intuitive. daily reading. For any FA, we can also describe its language using a notation called a regular expression (re).

有限自动机$F$可以描述一个语言集合，该集合也可以被转移图(transition diagram)描述，但是这些描述都不利于代码实现。因此，本节介绍正则表达式，用来描述该语言集合。

[page-60](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=59&x=211&y=310&id=37&uuid=12b2dcd9f9cdde959015bc3c6f83b485)

>An re describes a set of strings over the characters containedin some alphabet, $\Sigma$, augmented with a character $\epsilon$ that represents the empty string. We call the set of strings a language. For a given re, $r$, we denote the language that it specifies as $L(r)$.

RE的严格描述为：RE描述一个字符串集合，该集合的字符串是由字符集$\Sigma$和$\epsilon$组成。字符串集合也可以被叫做语言集合，对一个给定的正则表达式$r$，它描述的语言集合可以表示为$L(r)$。

> An re is built up from three basic operations:
> - Alternation The alternation, or union, of two sets of strings, $R$ and $S$, denoted $R \| S$, is              $\{x \| x \in R \text{ or } x \in S \}$.
> - Concatenation The concatenation oftwo sets $R$ and $S$, denoted $RS$, contains all strings formed by prepending an element of $R$ onto one from $S$, or ${xy \| x \in R \text{ and } y \in S}$.
> - Closure The Kleene closure of a set $R$, denoted $R^∗$, is $\cup_{i=0}^{\infty}R^i$. This is just the union of the concatenations of $R$ with itself, zero or more times.
>   The notation  $R^i$ denotes from one to $i$ occurrences of $R$. A finite closure can be always be replaced with an enumeration of the possibilities; for example, $R^3$ is just $(R \| RR \| RRR)$. The positive closure, denoted $R^+$, is just $RR^∗$ 
 
RE的三种基本操作是 ：
- 或，使用$\|$
- 且，直接拼接就可以
- 闭包，使用\*，表示0次到无数多次中任意一种
从这三种基本操作中可以衍生出：
- +，表示一次到无数多次中任意一种
- i，表示一次到i次中任意一种

> Using the three basic operations, alternation, concatenation, and Kleene closure, we can define the set of res over an alphabet $\Sigma$ as follows:
> - If $a \in \Sigma$, then $a$ is also an re denoting the set containing only $a$.
> - If $r$ and $s$ are res, denoting sets $L(r)$ and $L(s)$, respectively, then $r \| s$ is an re denoting the union, or alternation, of $L(r)$ and $L(s)$, $rs$ is an re denoting the concatenation of $L(r)$ and $L(s)$, respectively, and $r^*$is an re denoting the Kleene closure of $L(r)$.
> - $\epsilon$ is an re denoting the set containing only the empty string.
> 
> To eliminate any ambiguity, parentheses have highest precedence, followedby closure, concatenation, and alternation, in that order.

与三种基本操作对应，其描述的语言集合也会发生相应的改变。另外，符号操作之间存在优先级，括号优先级最高，然后是闭包，联结，或运算。

[page-65](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=64&x=329&y=502&id=162&uuid=651b2f45a2386b219ccc1c9a13ce5fd3)

>Regular expressions are closed under many operations—that is, if we applythe operation to an re or a collection of res, the result is an re. Obvious examples are concatenation, union, and closure.

正则表达式在基本运算下封闭，这意味着，我们可以先构建简单的Re，然后通过运算，将简单的Re变成复杂的Re.

[page-66](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=65&x=211&y=354&id=46&uuid=11fbe49906feb2fa86e82c29de94d0f8)

> The next section shows a sequence of constructions that build an fa to rec-ognize the language specified by an re. Section 2.6 shows an algorithm that goes the other way, from an fa to an re. Together, these constructionsestablish the equivalence of res and fas.
> 
> This result suggests that res are closedunder complement. Indeed, many systems that use res include a complementoperator, such as the ˆ operator inlex

在下一节，我们将从Re构建FA，然后在下下节，我们从FA构建Re，这就建立了Re和FA的等价性。这种等价性也说明了，Re在补运算下封闭。













