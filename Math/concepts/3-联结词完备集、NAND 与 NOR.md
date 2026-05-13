下面这块其实是离散数学/数电里很重要的基础：**联结词完备集**说的是“我手里只有某几个逻辑联结词，但能不能表达出所有命题逻辑公式”。

---

# 1. 什么是联结词？

命题逻辑里的常见联结词有：

| 符号    | 名称 | 含义       |
| ----- | -- | -------- |
| $\neg P$    | 非  | 不是 P     |
| $P \wedge Q$ | 合取 | P 且 Q    |
| $P \vee Q$ | 析取 | P 或 Q    |
| $P \to Q$ | 蕴含 | 如果 P，则 Q |
| $P \leftrightarrow Q$ | 等价 | P 当且仅当 Q |

这些符号就像编程语言里的运算符，比如 `!`、`&&`、`||`。

---

# 2. 什么叫“联结词完备集”？

一句话：

> 如果只用某一组联结词，就能表示出所有命题逻辑公式，那么这组联结词叫做**联结词完备集**。

比如：

> `{¬, ∧, ∨}` 是一个完备集。

因为命题逻辑里几乎所有复杂公式都可以通过 **非、且、或** 表示出来。

例如：

## 蕴含可以表示成

$$
P \to Q \equiv \neg P \vee Q
$$

也就是说，`→` 不是必须的，它可以被 `¬` 和 `∨` 表示。

## 等价可以表示成

$$
P \leftrightarrow Q \equiv (P \to Q) \wedge (Q \to P)
$$

进一步展开：

$$
P \leftrightarrow Q \equiv (\neg P \vee Q) \wedge (\neg Q \vee P)
$$

所以 `↔` 也不是必须的。

---

# 3. 为什么 $\{\neg, \wedge, \vee\}$ 是完备的？

因为任意一个真值表，都可以写成**析取范式**，也就是：

> 若干个“且”的结果，再用“或”连接起来。

例如，某个公式 F 的真值表如下：

| $P$ | $Q$ | F |
| - | - | - |
| T | T | T |
| T | F | F |
| F | T | T |
| F | F | F |

F 为真的情况有两行：

第一行：P 真，Q 真，对应：

$$
P \wedge Q
$$

第三行：P 假，Q 真，对应：

$$
\neg P \wedge Q
$$

所以：

$$
F \equiv (P \wedge Q) \vee (\neg P \wedge Q)
$$

这就说明，只要有：

$$
\neg,\ \wedge,\ \vee
$$

我们就能根据真值表构造任何命题公式。

所以：

$$
\{\neg, \wedge, \vee\}
$$

是联结词完备集。

---

# 4. 更小的完备集

其实 `{¬, ∧, ∨}` 还不是最小的。

因为：

## 或可以用非和且表示

根据德摩根律：

$$
P \vee Q \equiv \neg(\neg P \wedge \neg Q)
$$

所以 `{¬, ∧}` 就够了。

---

## 且可以用非和或表示

$$
P \wedge Q \equiv \neg(\neg P \vee \neg Q)
$$

所以 `{¬, ∨}` 也够了。

---

因此：

$$
\{\neg, \wedge\}
$$

是完备集。

$$
\{\neg, \vee\}
$$

也是完备集。

---

# 5. NAND 是什么？

NAND 叫做：

> 与非

意思是：

> 先做“与”，再取“非”。

符号常写作：

$$
P \uparrow Q
$$

或者：

$$
P \mid Q
$$

定义是：

$$
P \uparrow Q \equiv \neg(P \wedge Q)
$$

读作：

> P 与非 Q

---

# 6. NAND 的真值表

| $P$ | $Q$ | $P \wedge Q$ | P NAND Q |
| - | - | ----- | -------- |
| T | T | T     | F        |
| T | F | F     | T        |
| F | T | F     | T        |
| F | F | F     | T        |

也就是说：

> NAND 只有在 P 和 Q 都为真时才为假，其余情况都为真。

记忆方式：

```text
AND：两个都真才真
NAND：两个都真才假
```

---

# 7. 为什么 NAND 是完备的？

关键结论：

> 只用 NAND 一个联结词，就能表示 $\neg$、$\wedge$、$\vee$。

只要能表示出：

$$
\neg,\ \wedge,\ \vee
$$

就说明 NAND 是完备的。

---

## 7.1 用 NAND 表示非

$$
\neg P \equiv P \uparrow P
$$

为什么？

因为：

$$
P \uparrow P \equiv \neg(P \wedge P)
$$

而：

$$
P \wedge P \equiv P
$$

所以：

$$
P \uparrow P \equiv \neg P
$$

也就是：

```text
P NAND P = not P
```

---

## 7.2 用 NAND 表示与

因为：

$$
P \uparrow Q \equiv \neg(P \wedge Q)
$$

这已经是“与”的否定了。

如果再否定一次，就回到“与”。

所以：

$$
P \wedge Q \equiv (P \uparrow Q) \uparrow (P \uparrow Q)
$$

理解：

```text
P NAND Q              = ¬(P ∧ Q)
(P NAND Q) NAND itself = ¬¬(P ∧ Q)
                       = P ∧ Q
```

---

## 7.3 用 NAND 表示或

根据德摩根律：

$$
P \vee Q \equiv \neg(\neg P \wedge \neg Q)
$$

而：

$$
\neg P \equiv P \uparrow P
$$

$$
\neg Q \equiv Q \uparrow Q
$$

所以：

$$
P \vee Q \equiv (P \uparrow P) \uparrow (Q \uparrow Q)
$$

因为 NAND 本身就是：

$$
A \uparrow B \equiv \neg(A \wedge B)
$$

代入 $A = \neg P$，$B = \neg Q$，就得到：

$$
\neg(\neg P \wedge \neg Q)
$$

也就是：

$$
P \vee Q
$$

---

# 8. NAND 小结

只用 NAND 可以表示：

| 原运算   | NAND 表示           |
| ----- | ----------------- |
| $\neg P$    | $P \uparrow P$             |
| $P \wedge Q$ | $(P \uparrow Q) \uparrow (P \uparrow Q)$ |
| $P \vee Q$ | $(P \uparrow P) \uparrow (Q \uparrow Q)$ |
| $P \to Q$ | $P \uparrow (Q \uparrow Q)$       |

所以：

$$
\{NAND\}
$$

或者：

$$
\{\uparrow\}
$$

本身就是一个联结词完备集。

这非常重要，因为它说明：

> 一个联结词就可以表达所有命题逻辑运算。

---

# 9. NOR 是什么？

NOR 叫做：

> 或非

意思是：

> 先做“或”，再取“非”。

符号常写作：

$$
P \downarrow Q
$$

定义是：

$$
P \downarrow Q \equiv \neg(P \vee Q)
$$

读作：

> P 或非 Q

---

# 10. NOR 的真值表

| $P$ | $Q$ | $P \vee Q$ | P NOR Q |
| - | - | ----- | ------- |
| T | T | T     | F       |
| T | F | T     | F       |
| F | T | T     | F       |
| F | F | F     | T       |

也就是说：

> NOR 只有在 P 和 Q 都为假时才为真，其余情况都为假。

记忆方式：

```text
OR：只要有一个真就真
NOR：只要有一个真就假
```

---

# 11. 为什么 NOR 也是完备的？

同样，只要我们能用 NOR 表示：

$$
\neg,\ \wedge,\ \vee
$$

就能证明 NOR 是完备的。

---

## 11.1 用 NOR 表示非

$$
\neg P \equiv P \downarrow P
$$

因为：

$$
P \downarrow P \equiv \neg(P \vee P)
$$

而：

$$
P \vee P \equiv P
$$

所以：

$$
P \downarrow P \equiv \neg P
$$

也就是：

```text
P NOR P = not P
```

---

## 11.2 用 NOR 表示或

因为：

$$
P \downarrow Q \equiv \neg(P \vee Q)
$$

如果再否定一次，就得到：

$$
P \vee Q
$$

所以：

$$
P \vee Q \equiv (P \downarrow Q) \downarrow (P \downarrow Q)
$$

理解：

```text
P NOR Q              = ¬(P ∨ Q)
(P NOR Q) NOR itself = ¬¬(P ∨ Q)
                     = P ∨ Q
```

---

## 11.3 用 NOR 表示与

根据德摩根律：

$$
P \wedge Q \equiv \neg(\neg P \vee \neg Q)
$$

而：

$$
\neg P \equiv P \downarrow P
$$

$$
\neg Q \equiv Q \downarrow Q
$$

所以：

$$
P \wedge Q \equiv (P \downarrow P) \downarrow (Q \downarrow Q)
$$

因为 NOR 本身就是：

$$
A \downarrow B \equiv \neg(A \vee B)
$$

代入 $A = \neg P$，$B = \neg Q$，就得到：

$$
\neg(\neg P \vee \neg Q)
$$

也就是：

$$
P \wedge Q
$$

---

# 12. NOR 小结

只用 NOR 可以表示：

| 原运算   | NOR 表示                        |
| ----- | ----------------------------- |
| $\neg P$    | $P \downarrow P$                         |
| $P \vee Q$ | $(P \downarrow Q) \downarrow (P \downarrow Q)$             |
| $P \wedge Q$ | $(P \downarrow P) \downarrow (Q \downarrow Q)$             |
| $P \to Q$ | $((P \downarrow P) \downarrow Q) \downarrow ((P \downarrow P) \downarrow Q)$ |

所以：

$$
\{NOR\}
$$

或者：

$$
\{\downarrow\}
$$

也是联结词完备集。

---

# 13. NAND 和 NOR 的核心区别

| 项目             | NAND      | NOR       |
| -------------- | --------- | --------- |
| 中文名            | 与非        | 或非        |
| 定义             | $\neg (P \wedge Q)$  | $\neg (P \vee Q)$  |
| 什么时候为真         | 不是两个都真    | 两个都假      |
| 真值特点           | 只有 TT 时为假 | 只有 FF 时为真 |
| 是否完备           | 是         | 是         |
| 单独一个符号能否表达所有逻辑 | 能         | 能         |

---

# 14. 为什么 NAND / NOR 在数字电路里很重要？

因为它们是“通用门”。

意思是：

> 只用 NAND 门，理论上可以搭建任何逻辑电路。
> 只用 NOR 门，理论上也可以搭建任何逻辑电路。

比如 CPU、存储器、控制电路，本质上都可以用逻辑门组合出来。

所以 NAND 和 NOR 不只是离散数学里的符号，它们在数字电路里也非常核心。

---

# 15. 常见完备集与非完备集

## 常见完备集

| 联结词集合     | 是否完备 |
| --------- | ---- |
| $\{\neg , \wedge, \vee\}$ | 完备   |
| $\{\neg , \wedge\}$    | 完备   |
| $\{\neg , \vee\}$    | 完备   |
| $\{\neg , \to\}$    | 完备   |
| $\{NAND\}$    | 完备   |
| $\{NOR\}$     | 完备   |

---

## 常见非完备集

| 联结词集合  | 为什么不完备     |
| ------ | ---------- |
| $\{\wedge, \vee\}$ | 没有办法表达否定   |
| $\{\neg \}$    | 不能连接两个命题   |
| $\{\to\}$    | 单独不能表达所有运算 |
| $\{\leftrightarrow\}$    | 表达能力太弱     |
| $\{\wedge\}$    | 只能表示“且”类关系 |
| $\{\vee\}$    | 只能表示“或”类关系 |

例如 `{∧, ∨}` 为什么不完备？

因为它们都不会“翻转真假”。

如果只有：

$$
P \wedge Q
$$

$$
P \vee Q
$$

你永远无法得到：

$$
\neg P
$$

所以它不完备。

---

# 16. 做题套路

遇到题目问：

> 证明某个联结词集合是完备集。

最常用方法是：

## 方法一：证明它能表达 $\neg$、$\wedge$、$\vee$

因为 `{¬, ∧, ∨}` 已经是完备集。

所以只要你能用目标符号表达出：

$$
\neg P
$$

$$
P \wedge Q
$$

$$
P \vee Q
$$

就证明完备。

---

## 例如证明 NAND 完备

写出：

$$
\neg P \equiv P \uparrow P
$$

$$
P \wedge Q \equiv (P \uparrow Q) \uparrow (P \uparrow Q)
$$

$$
P \vee Q \equiv (P \uparrow P) \uparrow (Q \uparrow Q)
$$

所以 NAND 完备。

---

## 例如证明 NOR 完备

写出：

$$
\neg P \equiv P \downarrow P
$$

$$
P \vee Q \equiv (P \downarrow Q) \downarrow (P \downarrow Q)
$$

$$
P \wedge Q \equiv (P \downarrow P) \downarrow (Q \downarrow Q)
$$

所以 NOR 完备。

---

# 17. 最容易混淆的点

## NAND 不是 AND

NAND 是：

$$
\neg(P \wedge Q)
$$

不是：

$$
P \wedge Q
$$

所以它是“与之后再取反”。

---

## NOR 不是 OR

NOR 是：

$$
\neg(P \vee Q)
$$

不是：

$$
P \vee Q
$$

所以它是“或之后再取反”。

---

## NAND 和 NOR 都可以表示非

这是它们能成为完备集的关键。

因为：

$$
P \uparrow P = \neg P
$$

$$
P \downarrow P = \neg P
$$

也就是说，把同一个命题输入两次，就能得到它的否定。

---

# 18. 一句话总结

> 联结词完备集，就是一组足够强的逻辑符号。只用它们，就能表达所有命题逻辑公式。

最经典的完备集是：

$$
\{\neg, \wedge, \vee\}
$$

更强的是：

$$
\{NAND\}
$$

和：

$$
\{NOR\}
$$

因为 NAND 和 NOR 单独一个符号就能表示非、且、或，所以它们各自都是完备集。

最核心要背住这六个公式：

$$
\neg P = P \uparrow P
$$

$$
P \wedge Q = (P \uparrow Q) \uparrow (P \uparrow Q)
$$

$$
P \vee Q = (P \uparrow P) \uparrow (Q \uparrow Q)
$$

以及：

$$
\neg P = P \downarrow P
$$

$$
P \vee Q = (P \downarrow Q) \downarrow (P \downarrow Q)
$$

$$
P \wedge Q = (P \downarrow P) \downarrow (Q \downarrow Q)
$$
