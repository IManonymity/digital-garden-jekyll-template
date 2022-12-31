---
title: scanner
date: 2022-12-31, 17:33:33
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

$$s_1+s_2 = s_3$$






