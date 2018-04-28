# System and Network

## Introduction

Build computer systems from very many simple components- e.g. transistors(晶体管) & wires(金属丝).

### Levels of Abstraction

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