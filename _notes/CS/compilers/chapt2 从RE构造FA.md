---
title: 2.3 construct FA from RE
date: 2022-12-31
tags: compiler
book: Engineering a compiler
---

[page-69](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=68&x=104&y=249&id=51&uuid=f389ad51123f7625ede56859aff5e8a0)

> - Nondeterministic FA : an FA that allows transitions on the empty string, $\epsilon$, and states that have multiple transitions on the same character
> - Deterministic FA: a DFA is an FA where the transition function issingle-valued. DFAs do not allow $\epsilon$-transitions.

FA分为两种：
- NFA：有$\epsilon$转换，接受同一个字符，有多个转换行为
- DFA：没有$\epsilon$转换，接受同一个字符，只有一个转换行为

[page-70](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=69&x=211&y=261&id=54&uuid=5181f0261298971fb10be47bccecb59d)

>Under the second model of NFA behavior, the NFA has some finite set of operating clones. The number of these configurations can be bounded; for each state, the configuration either includes one or more clones in that state or it does not. Thus, an NFA with n states produces at most $\|\Sigma\|^n$ configurations.
>the DFA that simulates the NFA still runs in time proportional to the length of the input string. The simulation of an NFA on a DFA has a potential space problem, but not a time problem.

可以通过使用DFA来模拟NFA，由于字符串的长度不变，DFA处理的时间也不会变，改变的是空间的使用，使用DFA模拟NFA需要更多空间。


[page-70](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=69&x=211&y=588&id=164&uuid=6cbf91056ff59985ff9294b63f938076)

>It has a template for building the NFA that correspondsto a single-letter re, and a transformation on nfas that models the effect ofeach basic re operator: concatenation, alternation, and closure.
>![](/assets/images/构建NFA.png)

从RE构建NFA的模板是：首先对每个简单的re进行构建NFA，然后使用NFA的转换将re的操作联系起来。


[page-71](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=70&x=329&y=517&id=165&uuid=dd4d6b5f2fc495ec565892d7ba031063)

>Each nfa has one start state and oneaccepting state. No transition, other than the initial transition, enters thestart state. No transition leaves the accepting state. An $\epsilon$-transition always connects two states that were, earlier in the process, the start state and theaccepting state of nfas for some component res. Finally, each state has atmost two entering and two exiting $\epsilon$-moves, and at most one entering and one exiting move on a symbol in the alphabet. Together, these propertiessimplify the representation and manipulation of the nfas.

上述步骤构建NFA的性质

[page-73](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=72&x=329&y=414&id=166&uuid=863401a5ec6e325aa0aa2f9318756576)

> The algorithm that constructs a DFA from an NFA is called the subset construction.
> 
> The NFA and the DFA use the same alphabet, $\Sigma$.The DFA's start state, $d_0$, and its accepting states, $D_A$, will emerge from the construction. The complex part of the construction is the derivation of theset of DFA states D from the NFA states N, and the derivation of the DFA transition function $\delta_D$.
> 
> ![](/assets/images/构建DFA算法流程.png)

从NFA构建DFA的方法叫子集选择，其算法如上图所示，思想就是将所有能通过$\epsilon$转换到达的状态作为一个集合，该集合作为一个新的状态去构建DFA。

[page-78](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=77&x=211&y=503&id=168&uuid=7815a6b11c15e896af62e4946b938f87)

>To minimize the number of states in a DFA, $(D,\Sigma,\delta,d_0, D_A)$, we need a technique to detect when two states are equivalent—that is, when they produce the same behavior on any input string.
>
>![](/assets/images/精简DFA.png)

我们可以精简DFA的状态个数，将那些有相同行为的状态放在一起，从而可以节约空间，减少时间消耗。精简算法如上图所示。


[page-83](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=82&x=329&y=123&id=169&uuid=42f3ffc57974afb150ac60ef3234c7dc)

> Since most real programs contain more than one word, we need to transform either the language or the recognizer.
> 
> At the language level, we can insist that each word end with some easily recognizable delimiter, like a blank or a tab.
> 
> At the recognizer level, we can change the implementation of the dfa and itsnotion of acceptance.

因为不只是识别一个单词，而是很多个单词，我们需要做一些改变，如使用分隔符将输入流分开，或者 在识别的时候下一点功夫。


[page-83](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=82&x=329&y=235&id=173&uuid=6857ca1113e269f861aa507dc31e2c95)

> To find the longest word that matches one of the res,the dfa should run until it reaches the point where the current state, s, has no outgoing transition on the next character. 
> 
> Two cases arise; the first is simple. Ifs is an accepting state, then the dfa has found a word in the language andshould report the word and its syntactic category.
> 
 >Two cases occur. If the dfa passed through one or more accepting states on its way to s, the recognizer should back up to the most recent such state. This strategy matchesthe longest valid prefix in the input string. If it never reached an acceptingstate, then no prefix of the input string is a valid word and the recognizershould report an error.

为了识别更长的单词，我们在遇到接受状态并不停止，而是不断向前，直到无法向前，此时再判断状态，如果是接受状态，则返回，否则倒退到第一个接受状态并返回，如果没有接受状态，则返回错误。

[page-83](bookxnotepro://opennote/?nb={b7f4e0c6-1a2e-4ef0-9121-1eeb029d1870}&book=21548d9f83b3ce5d353a8baccff171a2&page=82&x=329&y=404&id=176&uuid=0f02a937b38654b389c3acfa14fb7b59)

> As a final complication, an accepting state in the dfa may represent severalaccepting states in the original nfa.
> 
> For example, if the lexical specifi-cation includes res for keywords as well as an re for identifiers, then akeyword such asnewmight match two res. The recognizer must decidewhich syntactic category to return: identifier or the singleton category forthe keyword new.
> 
> Most scanner-generator tools allow the compiler writer to specify a priorityamong patterns.

同一个单词可能有两个类别，我们需要给类别设置优先级。



























