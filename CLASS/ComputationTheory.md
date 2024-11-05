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
    * 状态的合并union和拆分

### 
- NFA without accepting state: Add an accepting state without transitions
- 交叉闭包：$L(M)=L(M_1) \union L(M_2) \qquad (q_0,q_1)$


### 06-regular grammars正则文法
$S->\lameda$产生空字符串
$S->SS$指任意的S连接S仍然是S
`S->aB|A`是两个产生规则
- 线性文法和非线性文法：`->`右边有两个变量；Right-Linear Grammars右线性文法：如果有，变量一定在最右边
- 左线性文法或右线性文法生成的语言一定是正则语言
* 证明：正则文法->正则语言
    * `S->bB|a`显然有`S-(b)->B`&`S-(a)->(())`
    * 状态转化显然可以表示为右线性正则文法
    * 左线性文法应该先转化为右线性文法：$L(G)=L(G')^R$，由于正则语言在翻转上封闭，故而左线性也是正则语言

### Non-regular Language
- Pumping lemma泵引理是正则语言的必要条件
- 由鸽巢原理得状态组合的重复性(walk指点和边都重复)