---
title: BWT压缩算法
date: '2013-09-11'
description: 利用BWT算法进行文本压缩
categories: algorithm
tags: [算法, BWT, 压缩 ]
---

##Burrows-Wheeler transform##

算法是非常巧妙的。首先把输入的数据则重排列，使得相同的字符，尽量地排在一起，这样方便压缩。如果只是想把相同的字符放在一起，
可以简单地对各个字符统计一下出现次数，然后放在一起。然而巧妙的地方是，它还可以根据重新排列后的字符串，算出
原始的字符串，从而解压缩。

重排列的过程如下：

把输入串的所有rotation（所谓rotation是指轮换，比如abcd有四个轮换，abcd,bcda,cdab,dabc）排序，然后依次把这些rotation
的最后一个字符串接起来成为新的串。这里要注意两个地方，一是各个字符出现的次数是否跟源串相同，二是相同的字符是否更多
地放在一起。

第一点是很容易证明，取这些rotation的任意一位串连起来，各个字符出现的次数跟源串都是相同的。

第二点很难证明，现在粗略分析一下。假设源串含有the,排序的结果应该是"he"打头的ratation排在一起
，这样最后一个字符是"t"的字符也应该排在一起。为什么不用这些rotation的第一位串联起来呢？用第一位的话，解释起来更直观，
但是用第一位串联起来的话，无法反映射回去。

现在来讨论一下怎么反映射。反映射的算法非常巧妙，从OI到ACM都考过这道题。有O（N）的算法的，实现起来也不难，只是比较难
想到。

用banana举例，它的六个rotation排序为：

abanan

anaban

ananab

banana

nabana

nanaba

则转换后的结果为nnbaaa，因为是有序的，我们可以反推出第一列应该为aaabnn，从而可以知道有下列六对相邻关系
na,na,ba,ab,an,an。
这些相邻关系里最小的一对应该是ab，把这六组相邻关系排序一下，为ab,an,an,ba,na,na。

从而知道六个rotation的第二列分别为b,n,n,a,a,a。

如果不是这样的话，则它们不应该这样排列，这其实是反证法。

从而可以得出另一组相邻关系，nab,nan,ban,aba,ana,ana，继续上面的过程，可以得出长度为四的相邻关系，一步步递推，
最终得出原始的所有的rotation。但是怎么知道哪个rotation是源串呢？只要在源串的结束处加一个特殊字符，然后再求rotation，
最终结束符放在最后的rotation就是源串了。
上面的实现是很低效的，是O（n^2)的，不过上面的过程已经说明这个算法可以用了。而且一般来说
，都是分块压缩的，n不会很大，平方的算法也够了。

下面描述效率为O（n)的实现方法：

从以上排序结果中，除了可以得到L[i]是F[i]的前缀外，还可以得到一个重要的性质：L中相同字母出现的顺序和F中相同字母
出现顺序相同。在已知原字符串最后一个字符是L[I]的情况下，要还原原字符串，关键是寻找字符L[I]的前一个字符在数组L中的
位置。

构造辅助数组，K[c]表示字符c在F中出现的次数，M[c]表示字符c在F中的首要位置，C[i]表示L[i]字符在i位置之前出现过车次数。由此
L[i]前一个字符在数组L中的位置可由C[i] + M[L[i]]推出。本实例中I=4，则依次推出L[4,1,5,2,6,3]="ANANAB"，正好是原字符串的反序。
逆变换的时间复杂度和空间复杂度均为O(n)。
