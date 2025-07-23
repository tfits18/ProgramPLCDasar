# Programmable Logic Controllers (PLC): Programming & Applications

This document aims to provide a basic understanding of PLC systems, instructions, and their applications, with a focus on the OMRON CPM2A PLC.

---

## 📖 Chapter 1: PLC Programming

PLCs can be programmed using several standard languages (IEC 1131-3) which are divided into two categories: **Textual** and **Graphical**.

### PLC Programming Languages

1.  **Ladder Diagram (LD)**
    * The most commonly used graphical language, resembling a relay control circuit diagram. It consists of two vertical lines (`power rails`) and horizontal lines (`rungs`) that contain the control logic.
    * **Key Features**:
    * Power flows from left to right.

      <img width="380" height="149" alt="image" src="https://github.com/user-attachments/assets/cde603e1-20bc-4f27-b683-ef5c9e3ed33f" />

    * Each rung must have at least one input and one output.
  
      <img width="477" height="137" alt="image" src="https://github.com/user-attachments/assets/4fb5156e-60e9-467a-b170-c1ef36b7b290" />

    * Outputs cannot be connected in series but must be in parallel.
  
      <img width="508" height="354" alt="image" src="https://github.com/user-attachments/assets/09787e0c-d378-4ce7-b238-33bc73bf51a2" />

    * An output address can only be used once, but input addresses can be used multiple times.
  
      <img width="493" height="398" alt="image" src="https://github.com/user-attachments/assets/e531695a-58e8-4569-bc08-2afce7e9456c" />
      <img width="499" height="275" alt="image" src="https://github.com/user-attachments/assets/a8bc8e8d-835f-4e32-bce0-9e33b94dac01" />

1.  **Instruction List (IL) / Mnemonic Code**
    * A text-based language that uses a list of statements to program the PLC. It is a textual representation of a Ladder Diagram. It consists of three columns: **Address**, **Instruction**, and **Operand/Data**.

      <img width="411" height="225" alt="image" src="https://github.com/user-attachments/assets/a3e3cb22-8b92-4334-8db1-7b8215529392" />
      <img width="449" height="207" alt="image" src="https://github.com/user-attachments/assets/44914fdf-a9b6-4bf1-b8c5-c0244ed5100d" />

2.  **Structured Text (ST)**
    * A high-level textual language similar to PASCAL, C, or BASIC, developed for industrial control. It is ideal for complex mathematical, algorithmic, or decision-making tasks. It uses statements like `IF...THEN...ELSEIF...END_IF;`.
      <img width="396" height="170" alt="image" src="https://github.com/user-attachments/assets/1a5e7081-44a3-41ab-933e-579e2dacf372" />
      <img width="428" height="144" alt="image" src="https://github.com/user-attachments/assets/e718c62f-275f-47a9-8923-2f7c4614f0ea" />

3.  **Function Block Diagram (FBD)**
    * A graphical language that uses blocks to describe the flow of signals and data. It is most useful for applications with high data flow between control components. It uses standard logic blocks like `AND`, `OR`, timers, and counters.
      <img width="465" height="286" alt="image" src="https://github.com/user-attachments/assets/eef051d3-577c-4d6f-8df5-3640ce67633c" />
      <img width="415" height="181" alt="image" src="https://github.com/user-attachments/assets/1b3f75a9-1485-4e42-8eba-554e49b1fe3c" />
      <img width="373" height="143" alt="image" src="https://github.com/user-attachments/assets/ee6fbb4d-5732-4a6d-b05b-73b664094253" />

4.  **Sequential Function Chart (SFC)**
    * A graphical language ideal for sequential processes. It consists of three main components: **Steps** (system functions), **Transitions** (conditions to move between steps), and **Actions** (outputs).
      <img width="299" height="226" alt="image" src="https://github.com/user-attachments/assets/3093942c-d99b-4053-b1d7-5d871dc4c9ac" />
      <img width="259" height="333" alt="image" src="https://github.com/user-attachments/assets/ecfdf37a-0fbf-4304-98fb-a76ff0b091aa" />
---

## 🛠️ Chapter 2: Basic Logic Instructions

These are the fundamental instructions used in PLC programming.

| Instruction | Description |
| :--- | :--- |
| **LD / LD NOT** | Starts a rung with a Normally Open (NO) or Normally Closed (NC) contact. |
| **AND / AND NOT** | Connects an NO or NC contact in series. |
| **OR / OR NOT** | Connects an NO or NC contact in parallel. |
| **OUT / OUT NOT** | Controls an NO or NC output coil at the end of a rung. |
| **AND LD** | Joins two parallel instruction blocks that are connected in series. |
| **OR LD** | Joins two series instruction blocks that are connected in parallel. |
| **END** | Marks the end of the program. It is required in every program. |

---

## ⏱️ Chapter 3: Timer & Counter Instructions

### Timer (TIM)

* Used to provide a time delay for input or output signals. It has a **Timer Number (N)** and a **Set Value (SV)**.
* **On-Delay Timer**: The timer is activated when the input is ON, and the output becomes active after the time delay has been reached.
* **Off-Delay Timer**: The output is active when the input is ON. When the input turns OFF, the timer starts counting to turn the output OFF after a delay.

### Counter (CNT)

* Used to count pulses or events.
* It has a **Clock Pulse (CP)** input for counting and a **Reset (R)** input to return the value to its SV.
* Each time CP transitions from OFF to ON, the set value decreases by one. When it reaches zero, the counter's output is activated.

---

## ✨ Chapter 4: Special Instructions

These instructions are used for more complex control functions.

* **Internal Relay (IR)**: An internal memory bit, not connected to a physical output, used to store an ON/OFF status within the program.
* **Holding Circuit (Latch)**: A circuit used to "latch" or maintain an output's status even after the trigger input is no longer active. It can be created using an auxiliary contact from the output itself or an IR.
* **SET / RESET**: Instructions to turn a bit ON (SET) or OFF (RESET). The bit remains in its state until the corresponding instruction is executed.
* **KEEP**: Functions similarly to a `Holding Circuit` or `SET/RESET` but is a single instruction block with Set (S) and Reset (R) inputs.
* **DIFU (Differentiate Up) / DIFD (Differentiate Down)**: Turns a bit ON for only one scan cycle when the input transitions from OFF to ON (DIFU) or from ON to OFF (DIFD).
* **IL (Interlock) / ILC (Interlock Clear)**: Used to disable (skip) all program logic between IL and ILC if the IL input is in the OFF condition. When the IL input is OFF, all outputs within the interlocked section are reset.
* **JMP (Jump) / JME (Jump End)**: Similar to Interlock, but when it skips a section of the program, the last status of the outputs within that section is **maintained** (not reset).

---

## 💡 Chapter 5: PLC Programming Applications

This chapter presents real-world examples, including:
* **Three-Phase Motor Direct Control**: Using a PLC to start and stop a motor via a contactor.
* **Three-Phase Motor Forward-Reverse Control**: Controlling the rotational direction of a motor with two contactors and interlock logic to prevent short circuits.
* **Pedestrian Crossing Traffic Light System**: Managing the cycle of red, yellow, and green lights for both cars and pedestrians using timers and sequential logic.
* **A Conveyor Dispatching System**: Controlling conveyor movement to transport boxes based on inputs from sensors and buttons.
* **Part Sorting for Assembled Material**: Using different types of sensors (capacitive, inductive) to detect and sort assembled parts from unassembled ones.
