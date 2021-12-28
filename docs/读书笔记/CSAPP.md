# 深入理解计算机系统

## Chapter 2

#### 2.1.3 Addressing and Byte Ordering

Litle endian: machines choose to store the object in memory ordered from least
significant byte to most.

Except Sun is big-endian machine, other is litile endian.

#### 2.2.6 Expanding the Bit Representation of a Number

Expansion of an unsigned number by zero extension, a two's-complement number by sign
extension.

C standards require, first expand size, then change sign. For:

```
short a;
unsigned a == (unsigned)(int)a
```

#### 2.4.2 IEEE Floating-Point Representation

$$
V = (-1)^s \times M \times 2^E
$$

```
// s-exp-frac 
//Single precision k = 8, n = 23, Bias = 127
//Double precision k = 11, n = 52, Bias = 1023
```

- Normalized Values

$$
e \neq 0, \neq 2^k - 1
M = 1 + f, E = e - Bias
$$

- Denormalized Values

$$
e = 0\\
M = f, E = 1 - Bias
$$

- Special Values

$$
NaN: e = 1, f \neq 0\\
\infty: e =1, f = 1
$$

## Chapter 3

### 3.4 Accessing Information

Integer registers:

| Argument number | Registers |
| --- | --- |
| 1 | %rdi, %edi, %di, %dil |
| 2 | %rsi, %esi, %si, %sil |
| 3 | %rdx, %edx, %dx, %dl |
| 4 | %rcx, %ecx, %cx, %cl |
| 5 | %r8, %r8d, %r8w, %r8b |
| 6 | %r9, %r9d, %r9w, %r9b |

%rax, %eax, %ax, %al -> Return value
%rbp, %rbx, %r12-%r15 -> Callee saved
%r10, %r11 -> Caller saved

#### 3.4.2 Data Movement Instructions

| Description | Instruction |
| --- | --- |
| Move | movb, movw, movl, movq, movabsq |
| Move with zero extension | movzbw, movzbl, movzbq, movzwl, movzwq |
| Move with sign extension | movsbw, movsbl, movsbq, movswl, movswq, movslq, cltq |

#### 3.4.4 Pushing and Popping Stack Data

| Description | Instruction |
| --- | --- |
| Push quad word | pushq |
| Pop quad word | popq |

### 3.5 Arithmetic and Logical Operations

The operations are divided into four
groups: load effective address, unary, binary, and shifts.

| Description | Instruction |
| --- | --- |
| Load effective address | leq S, D|
| Increment | INC D |
| Decrement | DEC D |
| Negate | NEG D |
| Complement | NOT D |
| Add | ADD S, D |
| Subtract | SUB S, D |
| Multiply | IMUL S, D |
| Exclusive-or | XOR S, D |
| Or | OR S, D |
| And | AND S, D|
| Left shift | SAL k, D |
| Left shift | SHL k, D |
| Arithmetic right shift | SAR k, D |
| Logical right shift | SHR k, D |

#### 3.5.5 Special Arithmetic Operations

| Description | Effect | Instruction |
| --- | --- | --- |
| imulq S | R[%rdx]:R[%rax] ← S × R[%rax] | Signed full multiply |
| mulq S | R[%rdx]:R[%rax] ← S × R[%rax] | Unsigned full multiply |
| cqto | R[%rdx]:R[%rax] ← (R[%rax])| Convert to oct word SignExtend |
| idivq S | R[%rdx] ← R[%rdx]:R[%rax] mod S; R[%rax] ← R[%rdx]:R[%rax] ÷ S| Signed divide |
| dicq S | R[%rdx] ← R[%rdx]:R[%rax] mod S; R[%rax] ← R[%rdx]:R[%rax] ÷ S | Unsigned divide |

#### 3.6.1 Condition Codes

CF: Carry flag. The most recent operation generated a carry out of the most significant bit. Used to detect overflow for unsigned operations.

ZF: Zero flag. The most recent operation yielded zero.

SF: Sign flag. The most recent operation yielded a negative value.

OF: Overflow flag. The most recent operation caused a two's-complement overflow—either negative or positive.

| Description | Instruction |
| --- | --- |
| Compare | CMP |
| Test | TEST |

#### 3.6.2 Accessing the Condition Codes

| Description | Instruction |
| --- | --- |
| Equal / zero | sete, setz |
| Not equal / not zero | setne, setnz |
| Negative | sets |
| Nonnegative | setns |
| Greater (signed >) | setg, setnle |
| Greater or equal (signed >=) | setge, setnl |
| Less (signed <) | setl, setnge |
| Less or equal (signed <=)| setle, setng |
| Above (unsigned >) | seta, setnbe |
| Above or equal (unsigned >=)| setae, setnb |
| Below (unsigned <) | setb, setnae |
| Below or equal (unsigned <=)| setbe, setna |

#### 3.6.3 Jump Instructions

| Description | Instruction |
| --- | --- |
| Direct jump | jmp Label |
| Indirect jump | jmp *Operand |
| Equal, ..., Below or equal | j(same as set) Label |

#### 3.6.5 Implementing Conditional Branches with Conditional Control

```
if (test-expr)
    then-statement
else
    else-statement
```

```
    t = test-expr;
    if (!t)
        goto false;
    then-statement
    goto done;
false:
    else-statement
done:
```

#### 3.6.6 Implementing Conditional Branches with Conditional Control

| Description | Instruction |
| --- | --- |
| Equal, ..., Below or equal | cmov(same as set) Label |

```
v = then-expr;
ve = else-expr;
t = test-expr;
if (!t) v = ve;
```

#### 3.6.7 Loops

1. Do-While Loops

```
do
    body-statement
    while (test-expr);
```

```
loop:
    body-statement
    t = test-expr;
    if (t)
        goto loop;
```

2. While Loops

```
while (test-expr)
    body-statement
```

Jump to middle

```
    goto test;
loop:
    body-statement
test:
    t = test-expr;
    if (t)
        goto loop;
```

Guarded do

```
t = test-expr;
if (!t)
    goto done;
do
    body-statement
    while (test-expr);
done:
```

```
t = test-expr;
if (!t)
    goto done;
loop:
    body-statement
    t = test-expr;
    if (t)
    goto loop;
done:
```

#### 3.7.1 The Run-Time Stack

```c
| 		Stack "botton" 		|
| ------------------------- |
| 	   Earlier frames       |
| 		    ...             |
| 		Arugment n          |
| 			...             |
| 		Arugment 7          |
| 	  Return address        |
| 	  Saved registers       |
| 	  Local variables       |
| 	Argument build areas    |
| 	   **Stack "top"**      |
```

#### 3.7.2 Control Transfer

| Description | Instruction |
| --- | --- |
| Procedure call | call Label |
| Procedure call | call *Operand |
| Return from call | ret |

### 3.11 Floating-Point Code

%ymm0, %xmm0 1st FP arg / Return value
%ymm(1-7), %xmm(1-7) (2-8)th FP argument
%ymm(8-15), %xmm(8-15) Caller saved

#### 3.11.1 Floating-Point Movement and Conversion Operations

| Description | Instruction |
| --- | --- |
| Move single precision | vmovss |
| Move double precision | vmovsd |
| Move aligned, packed single precision | vmovaps |
| Move aligned, packed double precision | vmovapd |
| Convert with truncation single precision to integer| vcvttss2si |
| Convert with truncation double precision to integer| vcvttsd2si |
| Convert with truncation single precision to quad word integer| vcvttss2siq |
| Convert with truncation double precision to quad word integer | vcvttsd2siq |
| Convert integer to single precision | vcvtsi2ss |
| Convert integer to double precision | vcvtsi2sd |
| Convert quad word integer to single precision | vcvtsi2ssq |
| Convert quad word integer to double precision | vcvtsi2sdq |

```x86asm
;Conversion from single to double precision
vunpcklps %xmm0, %xmm0, %xmm0 ;Replicate first vector element
vcvtps2pd %xmm0, %xmm0 ;Convert two vector elements to double
```

```x86asm
;Conversion from double to single precision
vmovddup %xmm0, %xmm0 ;Replicate first vector element
vcvtpd2psx %xmm0, %xmm0 ;Convert two vector elements to single
```

#### 3.11.3 Floating-Point Arithmetic Operations

| Description | Instruction |
| --- | --- |
| Floating-point add | vaddss, vaddsd |
| Floating-point subtract | vsubss, vsubsd |
| Floating-point multiply | vmulss, vmulsd |
| Floating-point divide | vdivss, vdivsd |
| Floating-point maximum | vmaxss, vmaxsd |
| Floating-point minimum | vminss, vminsd |
| Floating-point square root | sqrtss, sqrtsd |

#### 3.11.5 Using Bitwise Operations in Floating-Point Code

| Description | Instruction |
| --- | --- |
| Bitwise EXCLUSIVE-OR | vxorps, vxorpd |
| Bitwise AND | vandps, vandpd |

#### 3.11.6 Floating-Point Comparison Operations

| Description | Instruction |
| --- | --- |
| Compare single precision | vucomiss |
| Compare double precision | vucomisd |

The floating-point comparison instructions set three condition codes: the zero flag ZF, the carry flag CF, and the parity flag PF.