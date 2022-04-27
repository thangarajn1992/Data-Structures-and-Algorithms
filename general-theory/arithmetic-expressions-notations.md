---
description: Infix, Prefix, Postfix notations
---

# Arithmetic Expressions ( Notations )

In real word, we express an arithmetic expression with operator in between two operands. This notation is called **infix notation**. But, there are other ways in which an arithmetic expression can be written without changing the essence or output of an expression. These notations are

1. Infix Notation
2. Prefix Notation ( Polish )
3. Postfix Notation ( Reverse-Polish )

These notations are named as how they use operator in expression.

### Infix Notation

As mentioned earlier, this is general mathematical way we express an arithmetic expression. Operators are used **in-**between operands e.g. a-b+c. It is easy for us humans to read, write and speak in infix but the same does not go well with computing devices. An algorithm to process infix notation could be difficult and costly in terms of time and space consumption.

### Prefix Notation

Operator is **prefix**ed to operands, i.e. operator is written ahead of operands. e.g. +ab. It is also known **Polish Notation**

### **Postfix Notation**

Operator is **postfix**ed to operands, i.e. operator is written after the operands e.g. ab+. It is also known as **Reverse Polish Notation.**

| Sr.No. | Infix Notation    | Prefix Notation | Postfix Notation |
| ------ | ----------------- | --------------- | ---------------- |
| 1      | a + b             | + a b           | a b +            |
| 2      | (a + b) ∗ c       | ∗ + a b c       | a b + c ∗        |
| 3      | a ∗ (b + c)       | ∗ a + b c       | a b c + ∗        |
| 4      | a / b + c / d     | + / a b / c d   | a b / c d / +    |
| 5      | (a + b) ∗ (c + d) | ∗ + a b + c d   | a b + c d + ∗    |
| 6      | ((a + b) ∗ c) - d | - ∗ + a b c d   | a b + c ∗ d -    |

## **Parsing Expressions**

It is not a very efficient way to design an algorithm to parse infix notations. Instead, these infix notations are first converted to either prefix or postfix notations and then computed.

To parse any arithmetic expression, we need to take care of operator precedence and associativity also.

### Operator Precedence

When an operand is in between two operators, which operator will take the operand first, is decided by the precedence of an operator over others.

For eg:  a + b \* c   =>    a + ( b \* c)

Multiplication operation has precedence over addition.

### Operator Associativity

Associativity describes the rule where operators with same precedence appear in an expression. For eg, in expression a + b - c, both + and - have same precedence, then which part of the expression is evaluated first, is determined by associativity of those operators.

| **Sr.No.** | **Operator**                          | **Precedence** | **Associativity** |
| ---------- | ------------------------------------- | -------------- | ----------------- |
| 1          | Exponentiation ^                      | Highest        | Right Associative |
| 2          | Multiplication ( ∗ ) & Division ( / ) | Second Highest | Left Associative  |
| 3          | Addition ( + ) & Subtraction ( − )    | Lowest         | Left Associative  |

At any point of time in expression evaluation, the order can be altered by using **parenthesis.**

### **Postfix Evaluation Algorithm**

****[**Stacks**](../data-structures/stacks/) **** are used to evaluate postfix expression.

1. Scan the expression from Left to Right
2. If operand, push it to stack
3. If operator, pull operand from stack and perform operation
4. Store the result of the operation back into stack
5. Scan the expression until all operands are consumed
6. Pop the stack and perform operation.

