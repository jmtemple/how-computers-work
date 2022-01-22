# Logic gates, digital circuits, data path, memory, and machine language

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

This lab covers a variety of topics related to how computers "work." This lab is designed to help you gain an understanding of how the basic logical and mathematical operations underlying computation are performed mechanically. We will also use a simulation of CPU architecture to learn more about how an instruction is processed along the CPU data path cycle and how values from memory are incorporated into CPU instructions. We are doing this to gain more experience with understanding a computer’s mechanical operations at a higher level of abstraction. Finally, this lab covers reading and writing basic machine language, to help us see the 0s and 1s underneath higher level programming and apply them to basic algorithms.

## Acknowledgements

### Logic gates and digital circuits
This section of the lab incorporates elements of the "Log gates & digital circuits" lab:
- Written: Marge Coahran, April 2008
- Revised: Jerod Weinman, 17 March 2009
- Revised: Marge Coahran, 14 April 2010
- Revised: Jerod Weinman, 22 March 2011 & 15 April 2011
- Revised: Jerod Weinman, 3 April 2014
- Revised: Jerod Weinman, 1 April 2015
- Portions adapted from Coahran and Weinman

### Data path and memory
This section of the lab is based on the "Data path & memory" lab:
- Created: Jerod Weinman, 16 March 2009
- Modified: Jerod Weinman, 20 April 2011
- Modified: Jerod Weinman, 4 April 2014
- Portions adapted from Dave Reed, “A Balanced Introduction to Computer Science,” Exercises 14.1-14.6.

### Machine language
This section of the lab is based on the "Machine language" lab:
- Created: Jerod Weinman, March 16, 2009
- Revised: Janet Davis, April 27, 2012
- Revised: Janet Davis, March 12, 2013
- Revised: Jerod Weinman, 4 April 2014
- Adapted from Dave Reed, “A Balanced Introduction to Computer Science,” Exercises 14.9, 14.10, and 14.13. 

# Table of Contents

- [Logic gates and digital circuits](#logic-gates-and-digital-circuits)
  * [Academo Logic Gate Simulator](#using-academo-logic-gate-simulator)
- [Data path and memory](#data-path-and-memory)
  * [CPU Data Path](#cpu-data-path)
  * [ALU Operation](#alu-operation)
  * [CPU and memory](#cpu-and-memory)
- [Machine Language](#machine-language)
  * [Assembly to Machine Language](#assembly-to-machine-language)
  * [Machine to Assembly Language](#machine-to-assembly-language)
    * [Executing a Program](#executing-a-program)
    * [The `HALT` Instruction](#the-halt-instruction)
- [Lab Notebook Questions](#lab-notebook-questions)

# Logic gates and digital circuits

## Using Academo Logic Gate Simulator

The tool we will use for this lab is [Academo Logic Gate Simulator](https://academo.org/demos/logic-gate-simulator/), "a free online resource for digital logic circuit design and simulation.”

Open Academo.

Attempt the following tasks:
  * connect your input switch to the output pin
  * use the input switch to turn the output on and off
  * add another input switch 
  * add an `AND-Gate` to your circuit
  * connect two input switches to the `AND-Gate`'s input points
  * connect an output pin to the `AND-GATE`'s output point.
  * test all possible input combinations
  * replace the `AND-Gate` with an `OR-Gate` 
  * test all possible inputs for these new gates
  * replace the current gate with an `XOR-Gate`
  * test all possible inputs for these new gates
  * create a system involving 2 levels of gates (first level, any combination of `AND-Gate`'s and/or `OR-Gate`'s, and the second level, an `XOR-Gate` or `NOR-Gate`

<blockquote>Q1: Describe your experience attempting each of tasks. What went well? What was challenging? What lingering questions do you have about how circuits and logic gates work? Include an image of your final logic gate system involving 2 levels of gates with the output state being 'ON' and explain what is happening at each level to make turn the output state 'ON'.</blockquote>

# Data path and memory

## CPU Data Path

Open the [Knob & Switch Datapath 1 Simulator](http://www.dave-reed.com/book/Chapter14/datapath/datapath.html) in a new browser window. 

This simple CPU contains four registers, but no control unit. You will be the control unit that directs which registers are operated on and which operations are done.

Take a look at the top box that says `Register Bank.` At the right are two command knobs, `A Bus Address` and `B Bus Address.` These knobs specify which registers should be read as inputs to the ALU. 

<blockquote>CPU stands for central processing unit. ALU stands for arithmetic logic unit.</blockquote>

Click on each knob to turn it.

Set the `A bus` address to `R2` and the `B bus` address to `R1`. 

When a cycle is executed, the CPU will send the values from `R2` and `R1` along the bus.

The register values are the textboxes with a green background. Currently, all the register default values are zero. 

Set the value of `R1` to 42. Set the value of `R2` to 31.

Check that `Animation Speed` is set on `Medium` and `Number Base` is set to `+-10.`

<blockquote>Q2: Based on the settings of the bus addresses, what values do you expect to show along the A and B bus?</blockquote>

<blockquote>Q3: What happens when you click Execute? Are the <code>A bus</code> and <code>B bus</code> values what you expected? Why or why not?</blockquote>
  
## ALU Operation

The previous set of steps sent data to the ALU. Next we will tell the ALU what to do with the data. 

In the bottom right of the simulator is yet another knob entitled `ALU Operation.` This knob instructs the ALU what operation to perform on the data it has received. 

Click the knob so that it points to the instruction `A-B.`

The box to the left of the ALU knob is a diagnostic. It reports information based on the input provided to the ALU.

Right now, `zero` has a check next to it because the default result is zero. You should see this reflected in the `C` textbox.

<blockquote>Q4: What do you think will happen to the boxes when the result is less than zero?</blockquote>

Check that the simulator's current settings to make sure it is set to run `A-B`, where `A` is `R2` and `B` is `R1`.

<blockquote>Q5: With the values of <code>R1=42</code> and <code>R2=31</code> that you input earlier, what do you expect the result <code>C</code> to be?</blockquote>

Run the simulator to start a cycle with these settings. Halt the simulator when the result flashes in `C.` 

<blockquote>Q6: Is the result what you expected? Why or why not? What happened to the diagnostic boxes?</blockquote>

Now we want the ALU to do something with the calculated result.

The calculated result gets sent along the `C bus` back into the `register bank`.

The `C Bus Address` knob in the top-left of the simulator tells the CPU which register it should use to store the calculated result. 

Click the knob to store the result in `R3`.

Run a simulation of a full cycle to subtract `R1` from `R2` and store the result in `R3`.

<blockquote>Q7: Describe what happened and the output in the previous step.</blockquote>

<blockquote>Q8: What settings (e.g., knob positions) would cause the value stored in <code>R3</code> to be doubled?</blockquote>

<blockquote>Q9: Set <code>R3</code> to 12 and test your answer to Q8? Did your hypothesis hold true? Why or why not?</blockquote>

## CPU and memory

So far, we have only been using data from a limited number of CPU registers. Actual computers have much more storage in their main memory. Data gets from memory into the registers through additional communication channels.

Open the [Knob & Switch Datapath and Memory Simulator](http://www.dave-reed.com/book/Chapter14/dpandmem.html) in a new browser window. 

Two notable components here are the memory and bus switches. The memory values on the left of the simulator represent `RAM`. The button next to each memory location indicates which location will be read (`R`) from or written to (`W`) in one cycle of the machine.

The bus connections from the ALU to the register bank now have switches on them. 

Click these connections to toggle (open and close) the switches. Note that an open switch looks like an open door. No signal will flow across an open switch. A closed switch allows the signal to flow across it. 

Open the circuit from the ALU into the `C bus`, so that there is no longer a connection.

We also have two new connections along the `C bus`. The `C bus` is the pathway into the register bank. 

The connection pointing up from the `Main Memory Bus` into `C bus` allows us put memory values into registers, rather than ALU results. 

Click to close the connection from the `Main Memory bus` to the `C bus`. The connection from the `C bus` to the memory bus should be open.

Put the value 42 into memory location 0, and select it as the `RW` location.

Set the connection switch along the `C Bus` into the register bank so that it is closed. Select the `C Bus address` to be `R0`.

<blockquote>Q10: Based on these settings, what do you think will happen when you click Execute?</blockquote>
  
Verify your prediction using the simulator.

<blockquote>Q11: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?</blockquote>

Set `R0=23` and `R3=16` and verify your prediction using the simulator.

# Machine Language

Open the [Knob & Switch Machine Language Instruction Set](http://www.dave-reed.com/book/Chapter14/instructions.html) in a new browser window. 

Open the [Knob & Switch Machine Simulator](http://www.dave-reed.com/book/Chapter14/machine.html) in a second new browser window. 

Keep both Knob & Switch windows open in this section of the lab.

## Assembly to Machine Language

In memory location `0`, type the instruction `ADD R2 R1 R0`.

<blockquote>Q12: Using the Instruction Set from step 40, how would you start translating the `ADD R2 R1 R0` instruction from assembly or machine language to binary language?</blockquote>

Use the `View As:` drop-down menu on the left-hand side of the window to check your result. Change the menu value to `2` to reveal the binary executable instruction. 

<blockquote>Q13: How does your answer to Q12 compare to the simulator output from step 44? What discrepancies (if any) can you identify?</blockquote>

## Machine to Assembly Language

Refresh the window to reset the simulator to default settings.

On the drop-down menu next to memory location `1`, change the value from `Auto` to `2`.

<blockquote>Q14: Using the Instruction Set from step 40, how would you start to translate the binary instruction (or machine code) <code>1000001001001010</code> into assembly language or instructional language?</blockquote>

Copy this bit string into memory location `1`.

On the drop-down menu next to memory location `1`, change the value from `2` to `Instr` to show the binary executable instruction. 

<blockquote>Q15: How does your answer to Q14 compare to the simulator output from step 48? What discrepancies (if any) can you identify?</blockquote>

### Executing a Program
 
Enter the `HALT` instruction in memory location `2`.

Change the contents of `R0`, `R1`, `R2`, and `R3` to 1, 3, 5, and 7, respectively.

Click `Reset` above the `PC` (Program Counter) to initialize it to zero.

<blockquote>Q16: What do you expect to be the result when you click Execute? Run the simulation and verify your prediction.</blockquote>
  
### The `HALT` Instruction

<blockquote>Q17: What would happen if you had forgotten the <code>HALT</code> instruction? How would the control unit react?</blockquote>

Test your prediction by changing `HALT` in memory address `2` to something other than the default value.
  * You may need to change the `View as` drop-down to something other than `Instr`.

Reset the PC to value zero and execute the program to test your prediction.

# Lab Notebook Questions
  
Q1: Describe your experience attempting each of tasks. What went well? What was challenging? What lingering questions do you have about how circuits and logic gates work? Include an image of your final logic gate system involving 2 levels of gates with the output state being 'ON' and explain what is happening at each level to make turn the output state 'ON'.

Q2: Based on the settings of the bus addresses, what values do you expect to show along the A and B bus?

Q3: What happens when you click Execute? Are the `A bus` and `B bus` values what you expected? Why or why not?

Q4: What do you think will happen to the boxes when the result is less than zero?

Q5: With the values of `R1=42` and `R2=31` that you input earlier, what do you expect the result `C` to be?

Q6: Is the result what you expected? Why or why not? What happened to the diagnostic boxes?

Q7: Describe what happened and the output in the previous step.

Q8: What settings (e.g., knob positions) would cause the value stored in `R3` to be doubled?

Q9: Set `R3` to 12 and test your answer to Q8? Did your hypothesis hold true? Why or why not?

Q10: Based on these settings, what do you think will happen when you click Execute?

Q11: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?

Q12: Using the Instruction Set from step 40, how would you start translating the `ADD R2 R1 R0` instruction from assembly or machine language to binary language?

Q13: How does your answer to Q12 compare to the simulator output from step 44? What discrepancies (if any) can you identify?

Q14: Using the Instruction Set from step 40, how would you start to translate the binary instruction (or machine code) 1000001001001010 into assembly language or instructional language?

Q15: How does your answer to Q14 compare to the simulator output from step 48? What discrepancies (if any) can you identify?

Q16: What do you expect to be the result when you click Execute? Run the simulation and verify your prediction.

Q17: What would happen if you had forgotten the `HALT` instruction? How would the control unit react?
