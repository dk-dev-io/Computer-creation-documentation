# Transistors and Logic Gates

Regardless of which technology you choose—transistors, vacuum tubes, or relays—they all operate on the same principle. There is a cathode, an anode, and a gate between them that allows changing their state.

It is important to understand that transistors themselves do not compute anything. A computer consists not only of a logic module but of a large number of interconnected mechanisms. However, we will start with computation.

First, we need to learn how to work with input signals. For this, we use logic gates. There are five of them: **nand** (no and), **not** (inverter), **and**, **or**, **xor** (exclusive or).

**Nand** can be safely called the most important, because all other modules can be built from it. This is exactly where we will start:

## Nand

For easier understanding, we will design it based on relays. They come in two types: normally closed and normally open relays. In the first case, the contact is initially closed, and when current is applied to the coil, it opens the circuit. In the second case, the contact is initially open, but when current is applied to the coil, it attracts the relay and closes the circuit.  

With one relay of each type, we can build a **not and** component.  

Like any computer, we will need a constant power source to keep the system operational. In addition, we need two inputs to monitor.  

Suppose we have inputs A, B, C, where C is the constant power source.  

The **not and** gate consists of two relays connected in series. We need a normally closed relay—its input is connected to the constant power source, and its coil is connected to another relay, normally open, to which inputs A and B are connected. Now, when both inputs are applied, one will pass current through the relay, and the other will send current to the coil, which will close the circuit and pass the current further to the coil of the first relay, opening it.  

Thus, only if both inputs A and B are active, the output will be 0.

## Not

This is probably the simplest gate. It requires only one **nand** component. To invert input A, we connect it to both inputs of the **nand** component. This will result in an initial 1, but when voltage is applied to input A, the **nand** will trigger, and the output will be 0.

## And

The **and** component checks for simultaneous activation of both inputs. Suppose we have inputs A and B. We need to connect them to a **nand** gate and invert its output. Thus, only if both inputs are active, the **nand** will output 0, and the following inverter will change the value to 1.

## Or

For the **or** module, suppose we have inputs A and B. First, we need to connect them to inverters, and then connect their inverted values to a **nand** module. The **nand** module will be active when the inputs are off, outputting 0. But as soon as any of the inputs is active, or both (if both A and B are active), it will receive 0, and the output will be 1.

## Xor

Exclusive or means that only one of the inputs should be active to output 1. In other words, we get 0 when both inputs are off or both inputs are on. Suppose we have inputs A and B.  

The most optimal solution is to connect both inputs to a **nand** component, which will check that both inputs are not activated; for clarity, we will call this module the **guardian**. Then, each input needs to be connected to another **nand** module, and the second input of each is connected to the guardian.  

As long as both inputs are not active, the guardian will output 1, so activating one input triggers the corresponding **nand** module to output 0. When both inputs are activated, the guardian outputs 0, and both subsequent **nand** modules output 1. Finally, we combine these two **nand** modules with another **nand** module, and the exclusive or is ready.

---

These are all five logic modules that we use for computation.
