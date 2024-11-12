# The Theory of Computation计算理论

### Introduction
讨论Computability & Complexity 可计算性和复杂性
- 什么是NP问题？什么是NP完全问题？
NP-complete problems: believed to take exponential time to be solved

### Language
计算机处理的本质是计算机语言，什么是语言？
- 语言的运算
    1. 连接；reverse反转；
    2. （profix & fix前缀后缀n+1个）
    3. Exponent Operation幂运算
    4. kleene The \* Operation 全集$\sum_{}^{*} = \{ \epsilon,a,b,aa,ab,ba,bb,...\}$
    5. The \+ Operation 除开空字符串；
* 对（语言）集合
    1. 补$L^{-} = \sum_{}^{*} - L$
    2. 翻转$L^{R}=\{ w^{R}\}$
    3. Concatenation连接$L_1 L_2 = \{\}\{\} = \{\}$ 特殊的有幂运算$L^{n}=LL...L;L^0=\{\epsilon\}$ 
	    - 注意：$L = \{a^nb^n:n>0\}$ => $L^2 = \{a^nb^na^mb^m:m,n>0\}$ 
    4. star-closure(kleene)$L^{*} = L^0 \cup L^{+}$ 

### FSM&FSA
FSM有限状态机 & FSA有限自动状态机
- FSM：没有输出，但有一些状态被指定为接受状态，是专门为识别语言而设计的
- FSA：可以用状态表或状态图来表示，其中最终状态用双圈表示

### DFA(Deterministic Finite Automaton)
- 确定性有限自动机：Output: "Accept"or"Reject"
    - (initial state)->...->((accepting state))
    - **For every state, there is a transition for every symbol in the alphabet**
- DFA五元组
* 定义regular language为DFA接收的语言

### NFA(Non-Deterministic Finite Automata)
- 非确定性有限自动机：其与DFA的区别在于对同一个输入，可能有多个状态；
    - 典型的有Epsilon Transitions($\epsilon$)
* proof: DFA<==>NFA
    * 状态的合并union和拆分；最终生成的 DFA/NFA 能够模拟 NFA/DFA 的所有转换，并无歧义性

### 
- NFA without accepting state: Add an accepting state without transitions
- 交叉闭包：$L(M)=L(M_1) \union L(M_2) \qquad (q_0,q_1)$


### regular Language 正则语言
`(0+1)*`和`(0*+ 1*)*`是等价的


#### regular grammars 正则文法
什么是文法？G=(V,T,S,P) 四元组：变量，起始变量，常量，生成规则
$S->\epsilon$ 产生空字符串
$S->SS$ 指任意的S连接S仍然是S
`S->aB|A`是两个产生规则（式子）

- 线性文法和非线性文法：`->`右边有两个变量；Right-Linear Grammars右线性文法：如果有，变量一定在最右边
- 左线性文法和右线性文法合为**正则文法**
* 证明：正则文法->正则语言
    * `S->bB|a`显然有`S-(b)->B`&`S-(a)->(())`
    * 状态转化显然可以表示为右线性正则文法
    * 左线性文法应该先转化为右线性文法：$L(G)=L(G')^R$，由于正则语言在翻转上封闭，故而左线性也是正则语言

#### Pumping--Non-regular Language
- Pumping lemma泵引理是正则语言的必要条件
- 由鸽巢原理得状态组合的重复性(walk指点和边都重复)：必然有 $w=xy^{i}z ,\, i \geq 0$
    - 我们不关心z的长度，但是可以明确的是 $\left| xy \right| \leq p && \left| y \right| \leq 1$(p=minLength)
    - 也就是说，对 $w=xyz$ 证明 $w'=xy^{i}z \notin L$


### Context-Free Language
#### Context-Free Grammars 上下文无关文法
上下文无关文法：Variable -> String of variables and terminals
而上下文无关文法定义的语言就是上下文无关语言
- Examples
    - $S->aSa|bSb|\epsilon$ L(G)= {$ww^{R}: w\in \{ a,b \}^*$}
    - $S->aSb|SS|\epsilon$ L(G)={$w:n_{a}(w)=n_b(w)$, and $n_{a}(v) \geq n_{b}(v)$ in any prefix v}

- 我们可以通过`Derivation Tree派生树(parse tree解析树)`来构建字符串（S->节点直到生成全部叶子节点无变量）
- **Ambiguity**二义性成为难以解决的问题（**需要注意的是，这里的+是“连接”的意思，而非正则语言的“或”意义**）
    - 在没有运算优先级的情况下，即使是`a+a*a`的派生树也会出现问题(E->E+E|E*E|a)
    - Sometimes it is possible to find a non-ambiguous grammar for a language. But, in general it is difficult to achieve this. (E->E+T|T; T->T*F|F; F->(E)|a)
    - L={$\{a^n b^n c^m\} \union \{ a^n b^m c^m \} $} ($n,m \geq 0$)对于$a^n b^n c^n$显然就有不同的派生树

```
正则语言和上下文无关语言的交集是上下文无关语言
- 通过定义我们知道：
    - 正则语言的文法是左线性文法和右线性文法的集合，也即`S->aS|a`||`S->Sa|a`。a是包含空字符串的任何常量
    - 而上下文无关文法是
```
#### Simplifications of Context-Free Grammars
移除某个变量；remove Useless Productions（没有结果或不能抵达）
- Chomsky Normal Form
    - `A->BC|a(两个变量或一个常量)`，转化方法是增加变量（常量增为变量）
    - an equivalent grammar in Chomsky Normal Form
- Greinbach Normal Form
    - $A->aV_1V_2...V_k,\,(k\geq 0)$

### Pushdown Automaton -- PDA 下推自动机
- PDA: `$`为stack head, `z`为stack top
    - `(q)----(a(Input symbol), b(pop sysbol)->c(push symbol))---->(q)`
* 注意：`b(pop sysbol)->c(push symbol)`均是从top向下逐个写的
- PDAs are non-deterministic($\epsilon - transition$)
    - 也容易产生match found $\epsilon , \$->\$ || \epsilon, \epsilon->\epsilon$
- All the input is consumed  AND  The last state is an accepting state
    - we do not care about the stack contents at the end of the accepting computation
    - 我们**只需要一条路径来证明正确性**，而不正确的路径我们不关心：$\epsilon, \epsilon->\epsilon$ 尽管这样的可能带来多余的路径
- Transition function: $\delta(q_1,a,w_1)= \{(q_2,w_2), (q_3,w_3)\}$
    - PDA 的基本组成部分：(...省略) 栈符号集：栈中允许的符号集合。初始栈符号：栈开始时的符号。
    - 瞬时描述(Instantaneous Description):`(q(CurrentState), u(RemainingInput), s(CurrentStackContents))`是执行该步后的状态
        - 用`>`指示瞬时描述的前进，$>^{*}(上方)$表示快进
L(M)={$w: (q_0,w,z) >^{*} (q_f,\epsilon,s)$}

* PDA和CFG的转化
    * CFG转化为PDA：将CFG规则全作为$\epsilon$入栈规则，而将常量作为常量出栈规则
        * ($q_0$)---$\epsilon, \$->S\$$-->($q_1$)--规则-->($q_1$)--($\epsilon, \$->\$$)-->((q))
    * PDA转化为CFG
        * 首先对PDA进行预处理