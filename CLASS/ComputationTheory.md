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
- 交叉闭包：$L(M)=L(M_1) \cup L(M_2) \qquad (q_0,q_1)$


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
    - pumping lemma：如果一个语言A是正则语言，那么存在一个数p，使得A中任意长度至少为p的字符串s，可以被分割为三部分xyz，其满足条件
        -  $\left| xy \right| \leq p 且 \left| y \right| \geq 1$  下面这个式子对非负整数i都成立：$w'=xy^{i}z \in L$
    - 也就是说，如果要证明不是正则语言：对 $w=xyz$ 证明 $w'=xy^{i}z \notin L$





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
    - $L=\{\{a^n b^n c^m\} \cap \{ a^n b^m c^m \} \}$ ($n,m \geq 0$)对于$a^n b^n c^n$显然就有不同的派生树

```
正则语言和上下文无关语言的交集是上下文无关语言
- 通过定义我们知道：
    - 正则语言的文法是左线性文法和右线性文法的集合，也即`S->aS|a`||`S->Sa|a`。a是包含空字符串的任何常量
    - 而上下文无关文法是
```
##### Simplifications of Context-Free Grammars
移除某个变量；remove Useless Productions（没有结果或不能抵达）
- Chomsky Normal Form
    - `A->BC|a(两个变量或一个常量)`，转化方法是增加变量（常量增为变量）
    - an equivalent grammar in Chomsky Normal Form
- Greinbach Normal Form
    - $A->aV_1V_2...V_k,\,(k\geq 0)$

#### Pushdown Automaton -- PDA 下推自动机
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
        - 用 $\succ$ 指示瞬时描述的前进，$\succ^{*}(上方)$表示快进
L(M)={$w: (q_0,w,z) \succ^{*} (q_f,\epsilon,s)$}

* PDA和CFG的转化
    * CFG转化为PDA：将CFG规则全作为$\epsilon$入栈规则，而将常量作为常量出栈规则
        * ($q_0$)---($\epsilon, \epsilon->S$)-->($q_1$)--规则-->($q_1$)--($\epsilon, \$->\$$)-->((q))
        * （思路是将CFG认为是由左到右拆解，已经拆解的就是步骤，未拆解的入栈）Grammar Leftmost Derivation
    * PDA转化为CFG
        * 首先对PDA进行预处理
            * PDA只有一个接受状态；使用新的初始堆栈符号且验收时堆栈只包含堆栈符号（此符号不用于任何过渡）；每个过渡要么推一个符号，要么弹出一个符号，但不能同时推和弹出
            * 方法有：增加接收状态；增加新开始和结束符号（并在接收状态的结束符号出删栈）；将一个过渡拆解为push和pop（$\epsilon$也需要拆解）
        * 对于每个状态$q_n$，对 $A_{q_a q_b}$ 等价于 $q_a -> q_b$ （显然 $A_{q_a q_a}=\epsilon$）
        * （不太理解12的47后证了啥。。。）
##### DPDA (Deterministic)
- 意为每个转化都是确定的（唯一的）；相对的，有deterministic context-free
- 显然 $vv^{R}$ 就是典型的Non-DPDA
- PDAs **Have More Power than** DPDAs


#### Properties of Context-Free languages
- Properties of Context-Free languages
    - union $\cup$ `|` ; Concatenation连接; Star Operation星操作 $S_{1} \to SS_{1}|\lambda$
- Negative Properties:(不封闭) intersection交集; complement取反

* $L = L(M_{1}) \cap L(M_{2})$ is context-free
    * RL是CFL的子集，故而也是CFL。RL作为CFL（得到的语言）的子集，在L(M)上则可以认为是增加了规则
    * 根据上下文无关文法的文法条件可以得到L是上下文无关语言
    * 根据这个推论可以得到一些复杂的上下文无关语言的证明和证伪
    * **证伪**：反证法：假定L是上下文无关语言，那么$L'=L{\cap}L_{CFL}$也该是上下文无关语言（这样就通过了L的某个子集不是CFL证明了L不是CFL）

#### Pumping Lemma for Context-free Languages
- 对于一个足够长的CLG的生成字符串G，应该会出现重复的变量，或者说，出现 $B\to aBc$
- 设r为变量的个数，设t为任意文法生成式右侧最大个数；对于任意 $w \in L(G)$，若有 $\left|w\right| > t^{r}$生成过程必然有变量重复
    - 这是由文法生成树的结构的结构决定的
    - 也就是说，可以拆解 $w=uvxyz$, 且有 $w'=uv^{i}xy^{i}z \in L(G)$ （$\left|vy\right| \geq 1$）
- The Pumping Lemma: 存在p，对length>P的任意一个字符串..都应该找到uvxyz...

### Turing Machine 图灵机
- No boundaries -- infinite length
- `Read-Write head` at each transition: Read, Write, Move Left/Right; $(q_1)--a \to b, R-->(q_2)$
    - 我们用 $\lozenge$ 表示存储的空字符(?也有用B表示 $--(a, b, R)-->$ )
- Turing Machines are **deterministic**. No $\lambda$-transitions allowed.
- Halting: The machine halts in a state if there is no transition to follow.
- *Accepting states* have no outgoing transitions. The machine halts and accepts. 不允许出接收状态
    - Reject Input: halts in a non-accept state OR **enters an infinite loop**

- 图灵机对 $a^{n}b^{n}$ 的解法：指针在ab直接轮转，每次将最左边的a和b换成x和y，直到不存在a时也不存在b
- 1的补码（1's complement）就是常说的反码；2的补码（2's complement）就是常说的补码
    - 具体来说，补码的实现可以简化为：`在第一次遇到1之前不用修改，1之后全部取反即可`；不过，需要注意的是应该将最终的指针放在字符串开头处
...
- Turing Machine的构成：基本与PDA类似；Instantaneous description: `q_1(指针，指向后一个字符)caba`
    - 瞬时描述：转化 $\succ$ 多级转化 $\succ^{*}$

##### Turing_Variations
- 除了标准图灵机外，还有Different Turing Machine Classes；但我们可以证明，其与标准图灵机的运算能力相当
- 以下证明所有的With功能都可以与Standard Turing互相模拟simulate
    - Stay-Option(保持不动功能): standard增加一个中间状态；举例...；
    - Semi-Infinite Tape(半无限长带，移到最左侧时，左移无效)
        - 显然主要证单向变双向：我们可以将一个双向折叠成单向使用，只需要把状态添加一个L/R的标识符就可以了（可以在border增加一个LR的转化）
        - A useful trick: Multiple Track Tape(多轨)
    - Multi-tape Turing Machine(多带)：独立控制，更灵活
        - 显然主要证单带变多带：我们可以使用对每个tape建立两个Track，记录tape和head position；借用一个Reference point作为border壁找到current position
        - 需要注意的是`Same power doesn’t imply same speed`；多带很适合处理 复杂/多数据段切换算法
    - Multidimensional Turing Machines (多维图灵机)
        - 显然主要证单维变多维：Store symbols in track 1；Store coordinates in track 2 （a;#1,-1#; b;#0,0#）
        - 某种意义上，这是因为二维整数坐标上的点能和自然数对应
    - Nondeterministic Turing Machines(不确定图灵机)
        - 显然主要证确定变不确定：为了让 DTM 模拟 NTM，我们使用广度优先搜索或深度优先搜索（容易陷入无限路径的困境），遍历所有可能的计算路径（使用多带储存所有的备份情况）


####  Turing Recognizable/Acceptable / Recursively Enumerable

##### decidable
- 如果说一个语言可以被Turing machine接收，那么认为ta是可判定的/可解的solvable

```
是先得到p，然后寻找字符串
‘
显然 VV是S->SS的子集，
但实际上，VV失去了S->SS的一部分包含性，故而不再是上下文无关语言
=>显然对于m 存在a^m b^m a^m b^m 不是
```














## class
### 作业3
##### 第一题
###### 第一问
- $S\to S_1S_D | S_AS_2$
- $S_1 \to aS_1c | S_B | ac \qquad S_2 \to bS_2d | S_C |bd$
- $S_A \to aS_A | a \quad S_B \to bS_B | b \quad S_C \to S_Cc | \epsilon \quad S_D \to S_Dd | \epsilon$ 
将以上式子简单化简：
- $S\to S_1S_D | S_AS_2$
- $S_1 \to aS_1c | ac | bS_1 | b \qquad S_2 \to bS_2d | bd | S_2c | \epsilon$
- $S_A \to aS_A | a   \quad S_D \to S_Dd | \epsilon$ 
###### 第二问
aabccddd接收
abcccdd拒绝


##### 第二题
- $S\to aaSbbb | aabbb$
- aabbb接收；aaabbbb拒绝
##### 第三题
- $S \to aSa | bSb | \#$
- 不可以，因为缺少了明显的界限，DPDA不知道应该执行前半部分的指令还是后半部分的指令

