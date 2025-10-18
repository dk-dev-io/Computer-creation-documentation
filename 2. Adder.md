# Adder

To begin, we need to define two very important concepts:

1. **Binary system** — the foundation of all modern computing. In everyday life, we use the decimal system, which has 10 digits (0–9) and positional values, where each subsequent position is 10 times greater than the previous one. In the binary system, we have only 0 and 1, and each next position is 2 times greater. For example, 5 in binary is written as `101`.

2. **Bitness** — we often hear terms like *8-bit*, *16-bit*, *32-bit*, and so on. This refers to the size of the number that a device can process. Later, it will be explained how this limitation arises.

Thus, any modern computing device has a defined bitness and operates on the binary system.  
It is also important to know that no computer can subtract, divide, or multiply in the usual sense — all our computing hardware is fundamentally based on **addition**, and we have simply learned how to represent all other operations as additions.

---

## Half Adder

A **half adder** is a component that adds two bits.  
Its output is a **two-bit** value, and it has **two inputs** and **two outputs**.  
Let’s denote the inputs as **A** and **B**, and the outputs of the half adder as **h** (high bit) and **l** (low bit).

The simplest and most efficient way to build a half adder is to use an **xor** module and connect an **inverter** to its **guard**.  
Then, the **xor** output gives **l**, and the **inverter** output gives **h**.

---

## Full Adder

A **full adder** is a component that adds **three bits**: **a**, **b**, and **c**,  
where **a** and **b** are inputs, and **c** is the carry from the previous addition.  
The ability to add the third bit makes it “full,” since it can now account for the carry of the higher bit.

The simplest way to create a full adder is to use **two half adders** and **one or gate**.  
In the first half adder, we connect inputs **a** and **b**.  
The **l** output of this half adder is connected to the input of the second half adder, together with the input **c**.  
Then, we use an **or** gate to check for signals on the **h** outputs of both half adders and connect it to the output.  

Thus:
- The first half adder adds **a** and **b**.  
- If only one of them is active, its **l** output goes to the next half adder and is added with **c**.  
- If all inputs are active, **a** and **b** produce **h** on the first adder and don’t send the signal further, while **c** produces a signal on the **l** output.

However, this circuit is **not optimal** — it requires **15 nand** gates, which in turn require **30 transistors**.  
A full adder can be built using only **9 nand** gates, almost half as many.

To do this, we need **two xor** gates and **one nand** gate.  
If we recall from earlier, an **xor** gate checks whether both inputs are active.  
We can "peek" at its output to detect overflow.  

By connecting **two xor gates in sequence**, where the first one takes inputs **a** and **b**, and the second takes **c** and the output of the first **xor**,  
we connect the output of the second **xor** to **l**,  
and the output of the **nand** gate (which is connected to the guards of both **xor** gates) to **h**.  

Thus, we sequentially add **a**, **b**, and **c**,  
and the extra **nand** gate checks that no overflow occurs.

---

## Multi-bit Adder

To create an adder of any bitness, we need to connect the required number of full adders in sequence.  
Suppose we want to build a **4-bit adder** — it will be able to add two 4-bit numbers  
(range `0–1111` in binary or `0–15` in decimal).  
The result will be a **5-bit** number (for example, adding `1111` and `1111` gives `11110 = 30`).  

Let’s define our outputs as **s0–s4** (a 5-bit output).  
Inputs will be **a0–a3** and **b0–b3**.  

As mentioned, we’ll need **4 full adders**, labeled **c0–c3**.

- In **c0**, connect inputs **a0** and **b0**.  
  - Connect **l** output to **s0**, and **h** output to **c1**.  
- In **c1**, connect the **h** output of **c0**, and inputs **a1**, **b1**.  
  - Connect **l** to **s1**, and **h** to **c2**.  
- Continue this pattern until the last adder — in our case, **c3**.  
  - In **c3**, connect **a3**, **b3**.  
  - Connect **l** to **s4**, and **h** to **s5** (since this is the last adder and there’s nowhere else to carry the bit).

Thus, we have created a **multi-bit adder**,  
which can be scaled to **any bitness** as needed.
