---
title: 2.1 FA
date: 2022-12-31
tags: compiler
book: Engineering a compiler
---

[page-51](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=50&x=329&y=323&id=157&uuid=2a05edefdd833e61bbd1ab555a17a214)daily reading

>While most textbooks and courses advocate the use of generated scanners, most commercial compilers and open-source compilers use hand-crafted scanners. A hand-crafted scanner can be faster than a generatedscanner because the implementation can optimize away a portion of the over-head that cannot be avoided in a generated scanner. Because scanners aresimple and they change infrequently, many compiler writers deem that the performance gain from a hand-crafted scanner outweighs the convenienceof automated scanner generation.

可以使用已有的扫描器，也可以手写，但更偏向于手写，因为手写的扫描器可以做更多优化，从而获得更好的性能。

> A compiler’s scanner reads an input stream that consists of charactersand produces an output stream that contains words, each labelled with its syntactic category—equivalent to a word’s part of speech in English. To accomplish this aggregation and classification, the scanner applies a set of rules that describe the lexical structure of the input programming language,sometimes called its microsyntax.

扫描器读取字符输出流，然后输出分类后的单词。如何识别单词呢？词法结构描述了每一类单词的规则，通过应用词法结构，扫描器就可以识别每类单词，并输出tokendaily reading，即一个元祖(单词,类别)。

[page-52](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=51&x=211&y=335&id=159&uuid=7a99fb4302134621d9996dcf66ee7b6f)

>The compiler writer starts from a specification of the lan-guage’s microsyntax. She either encodes the microsyntax into a notationaccepted by a scanner generator, which then constructs an executable scan-ner, or she uses that specification to build a hand-crafted scanner. Bothgenerated and hand-crafted scanners can be implemented to require justO(1) time per character, so they run in time proportional to the number of characters in the input stream.

通过使用某些符号(如，正则表达式)去描述词法结构，并将这些符号输入给一个开源的扫描器，就大功告成了，开源的扫描器就能正常工作了。或者我们根据这些词法结构，去手动实现一个扫描器。这两种方法所用的时间都与输入的字符数成正比。

[page-54](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=53&x=436&y=522&id=30&uuid=b80627c3b3bfbb71b5c41973b9e4fcea)

>Finite automatona formalism for recognizers that has a finite set of states, an alphabet, a transition function, a startstate, and one or more accepting states. 
>
>Formally, a finite automaton (FA) is a five-tuple ($S$, $\Sigma$, $\delta$, $s_0$, $S_A$), where
>- $S$ is the finite set of states in the recognizer, along with an error state $s_e$.
>- $\Sigma$ is the finite alphabet used by the recognizer. Typically, $\Sigma$ is the union of the edge labels in the transition diagram.
>- $\delta(s,c)$ is the recognizer’s transition function. It maps each state $s\in S$ and each character $c\in \Sigma$ into some next state. In state siwith input character $c$, the FA takes the transition $s_i \stackrel{c}{\rightarrow} \delta(s_i,c)$.
>- $s_0\in S$ is the designated start state.
>- $S_A$ is the set of accepting states, $S_A\subseteq S$. Each state in $S_A$ appears as a double circle in the transition diagram.
>  
>  a  FA example 
>  ![images](/assets/images/有限自动机.png)

我们可以使用有限自动机对识别单词的过程进行描述。有限自动机是一个五元组($S$, $\Sigma$, $\delta$, $s_0$, $S_A$)，每个部分已在上文解释。


[page-55](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=54&x=329&y=384&id=31&uuid=1706c823ec4230eec66abf0793e9023c)

>An FA accepts a string $x$ if and only if, starting in $s_0$, the sequence of characters in the string takes the FA through a series of transitions that leave sit in an accepting state when the entire string has been consumed.
>
>More formally, if the string $x$ is composed of characters $x_1x_2x_3\ldots x_n$, then the FA($S$, $\Sigma$, $\delta$, $s_0$, $S_A$) accepts $x$ if and only if
>
$$ 
\delta(\delta(\ldots\delta(\delta(s_0, x_1),x_2)\ldots,x_{n-1}),x_n)\in S_A
$$

成功处理：当且仅当消耗完所有字符，且最后的状态是接受状态$S_A$时，字符串$x$才会被识别为一个单词。


[page-56](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=55&x=211&y=129&id=32&uuid=56b2453417db3d112f378b9b76a5677e)

>Two other cases are possible. The FA might encounter an error while processing the string—that is, some character $x_j$ might take it into the error state $s_e$.This condition indicates a lexical error; the string $x_1x_2x_3\ldots x_j$ is not a valid prefix for any word in the language accepted by the FA. The FA can also discover an error by exhausting its input and terminating in a nonaccepting state other than $s_e$.

失败处理有两种情况：
- $x_1x_2x_3\ldots x_j$不是有效前缀，会导致错误状态$s_e$
- 处理完所有字符串，最后不是接受状态$S_A$，也不是错误处理状态$s_e$


[page-58](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=57&x=211&y=304&id=161&uuid=fb967d8cbcbecae1ec63193bcd0f954d)

> FAS can be viewed as specifications for a recognizer. However, they are notparticularly concise specifications. To simplify scanner implementation, we need a concise notation for specifying the lexical structure of words, anda way of turning those specifications into an FA and into code that implements the FA. The remaining sections of this chapter develop precisely those ideas.

有限自动机可以对单词的识别过程进行描述，但是不利于我们去写代码实现，接下来我们将介绍正则表达式用来等价地描述有限自动机。









