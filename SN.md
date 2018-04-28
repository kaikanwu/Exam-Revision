# System and Network

<!-- TOC -->

- [System and Network](#system-and-network)
    - [一、Introduction](#一introduction)
        - [Levels of Abstraction](#levels-of-abstraction)
        - [Computers](#computers)
        - [Data](#data)
        - [Representations](#representations)
        - [Programs](#programs)
        - [Binary Codes](#binary-codes)
        - [Computer Storage](#computer-storage)
        - [Bytes](#bytes)
        - [Words](#words)
        - [Questions](#questions)
    - [二、Binary Codes](#二binary-codes)
        - [Basic Components](#basic-components)
        - [Unsigned Number Representation](#unsigned-number-representation)
        - [Unsigned binary addition加法](#unsigned-binary-addition加法)
        - [Hexadecimal](#hexadecimal)
        - [Signed numbers](#signed-numbers)
        - [Characters](#characters)
        - [Question](#question)

<!-- /TOC -->

## 一、Introduction

Build computer systems from very many simple components- e.g. transistors(晶体管) & wires(金属丝).

### Levels of Abstraction

![Screen Shot 2018-04-27 at 12.44.12.png](https://i.loli.net/2018/04/27/5ae30d5202a2c.png)

### Computers

A computer is a machine that executes sequences on **instructions(programs)** which direct it to operate on **(process)data.**

Can be: Personal computer, sever, embedded computer, high performance computer

Strength: generality

### Data

Numbers used in two ways:

* counting/labelling (**Whole Numbers**)整数
* measurement(**Real Numbers**)实数

 In other words, real numbers contain all rational and irrational numbers and only them.

Whole numbers sometimes are same as Natural numbers and sometimes include 0. Ex: 34

Results of labeling and measurements are **data sets**. sequences are data.

A set of data iems under discussion at a given time forms a data set.

### Representations

Data representation(数据表示法)involves finding suitable physical quantities to represent numbers.(need presentations that can be stored(**memory**) in physical devices and communicatd between devices.)

In current technology electrical **voltages**(电压) are most commonly used. 用电压的不同来表示数据。

* Easily stored and transmitted over wires
* Other technologies are possible(e.g. optical(光学的))

**Machine work with representations not with data.**

Two distinct approaches:

* **Analogue representations(模拟表示法)** use continuous phenomena/ continuous physical quantities连续的物理量(measured to arbitrary accuracy任意精度)

  * In reality measurement has limited accuracy, and this limites the acuracy of the representation.
  * Noise in the environment also introduces errors which are hard to control.
  * Once polular, have largely fllen out of use.
  * Simple example: slide rule uses length as measureable quantity

* **Digital representations(数字表示)** use discrete phenomena离散现象(finite number of allowed measurable values)
  * Current technolgy favours **binary representationsb**(二进制表示法) with two values of **voltage**, usually called **low** and **high**.
  * In general the values are labelled **0** and **1** and are called **bits**(binary digits)
  * Only need to be able to tell 2 values aprat, so superior resistance to noise and errors(因此可以有效的抵抗噪音和错误).
  * can represent as many data items as required using sequences(strings) of bits called **code words**

### Programs

A **program** is a set of instructions detailing how input data should be processed to achieve a desired result(oupput data).

Programs may themselves be treated as data by other programs(e.g. a **compiler**)

### Binary Codes

A mapping from **a data set** to **binary code words** is called a **binary code**
![Screen Shot 2018-04-28 at 10.26.20.png](https://i.loli.net/2018/04/28/5ae43e5967a54.png)

* If all the code words have same number of bits, code is **fixed legth**.

### Computer Storage

Basic digital circuit基本数字电路:

* take a data bit and store it
* remember the value indefinitely
* read out the sotred value

A **bit storage circuit** as a box that: contains one bit, can read out its contents and can store a new bit value.

The computer's memory consists of a large number of these basic circuits.

### Bytes

A byte is a string of 8 bits, e.g. 01101001

A byte is represented in the computer by 8 copies of the baisc bit storage circuit.

There are exactly 256(2的8次方) different values that can be represented in a byte.

### Words

A word is a larger amount of inofrmation.

|Column1  |Column2  |Column3  |
|---------|---------|---------|
|Short word    | 16 bits        |  2 bytes       |
|Word     |  32 bits       |    4 bytes     |
|Long word     |  64 bits       |  8 bytes       |

A word contain K bits is called a k-bit word. 可以表示2的K次方的不同的值。

![Screen Shot 2018-04-28 at 10.46.12.png](https://i.loli.net/2018/04/28/5ae442fd55050.png)

Early machines used 8-bits; today the norm is 64-bits.

### Questions

1. What data sets are involved in the following Java data types: boolean, byte, short, char?

2. Design an 8-bit code for unsigned numbers. Now design one for signed numbers.

3. Explain why digital representations have more resistance to noise than analogue.

4. An 8-bit adder is a device that takes in two 8-bit code words representing numbers and generates the 8-bit code word representation of the sum of the numbers. Such a device will sometimes fail to give the right answer. Explain why.

## 二、Binary Codes

To manipulate binary representations in real devices need to connect components by **wires**.

- Each wire can represent one bit at one time(as high or low voltage bewteen wire & ground).
- **Line driver(output)**
- **line receiver(input)**
- To carry n-bits, can use one wire(**serial transmission**串行传输)taking n bit times, or n wires running in parallel(**parallel transmission**并行传输)taking 1 bit time. This arrangement is called an n-bit bus.

### Basic Components

A 1-bit memory(build into n-bit **registers** to store binary code words)

Devices to perform useful operations on bits and on code words.
Examples:

- **Inverter反相器**(or NOT gate非门): onew wire in, one wire out, flips input bit(H->L, L->H).
- **n-bit adder**:

### Unsigned Number Representation

Decimal postitional code. And binary positional code. E.g.
![Screen Shot 2018-04-28 at 23.21.25.png](https://i.loli.net/2018/04/29/5ae4f400aa1c1.png)

### Unsigned binary addition加法

x = 1010 and y = 1111, the result should be 11001.

If we add two n-bit unsigned numbers and the sum is too big to be an n-bit number, the sum cannot be represented in the n-bit code. This is called an **(unsigned) overflow(这里指算数溢出)**

### Hexadecimal

hexa:六 decimal:十进制的 hexadecimal:十六进制的

Binary codewords can be very long and difficult for humans to work with. A common way to shorten binary strings is to convrt them to a base 16 number representation: hexadecimal.

Hexadecimal has 16 digits: **0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f.**

Convert hexadecimal to binary: 3a6e-> 0011 1010 0110 1110

### Signed numbers

Here numbers can be **negative** or **positive**.

Negative 1 in 8-bit sign and magnitude code is 1000 0001
Positive 1 in 8-bit sign and magnitude code is 0000 0001

complement code: 补码

**原码表示法**是机器数的一种简单的表示法。其符号位用0表示正号，用1表示负号，数值一般用二进制形式表示。

机器数的**反码**可由原码得到。如果机器数是正数，则该机器数的反码与原码一样；如果机器数是负数，则该机器数的反码是对它的原码（符号位除外）各位取反而得到的。

机器数的**补码**可由原码得到。如果机器数是正数，则该机器数的补码与原码一样；如果机器数是负数，则该机器数的补码是对它的原码（除符号位外）各位取反，并在未位加1而得到的。

### Characters

A character code is a table giving the bit value that represents each character.

ASCII(American Standard Code for Information Interchange) is an older standard code(1960), still in common use: uses 7-bits or 8-bit code words.

**Unicode**(two-byte code, 16 bits) is the current standard and includes many additional characters. can be extended to 32-bits.

C, C++: ASCII
Java: A string in Java is a sequence of Unicode characters.

### Question

1. Bit times are just as important on buses as on single wires. Why?
2. A register will need some inputs and outputs other than for the data.
stored or read. Why?
3. Convert 224 to binary.
4. Convert 111101012 to hexadecimal.
5. Convert FE16 to decimal.
6. The 8-bit 2’s complement code can represent all numbers between - 128 and +127. An 8-bit unsigned adder will add numbers in this range correctly unless the code overflows. Find two examples to show that 2’s complement code overflows do not occur when unsigned code overflows do (one example) and vice versa (another example)
7. Challenge. Can you find a condition for two’s complement overflow in an 8-bit code (Hint it involves the carries into and out of the MSB)