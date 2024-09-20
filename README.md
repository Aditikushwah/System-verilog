#Sequential Circuit Verification for a Simple Up and Down Counter

**Overview**
This project implements a verification environment for a simple up and down counter, which is a sequential circuit.
The verification environment is written in SystemVerilog and follows a modular approach inspired by the Universal Verification Methodology (UVM) concepts, without relying on the full UVM library. 
The counter's behavior is governed by a clock signal, and its output depends on the current inputs as well as the internal state of the counter.

The primary goal of this verification environment is to ensure that the counter correctly performs its counting operations (both incrementing and decrementing) while responding appropriately to control signals such as reset, load, and up/down count selection.

**Counter Functionality**
The up and down counter being verified is a sequential circuit that:

Counts up when the up signal is asserted.
Counts down when the up signal is deasserted.
Loads a specific value into the counter when the load signal is active.
Resets to an initial state when the rst signal is asserted.
The counter’s output changes on every clock cycle, depending on its internal state and the input signals applied in previous cycles.

**Components of the Verification Environment**
**Transaction**
The transaction class defines the input and output data for the counter. It includes:

loadin: The value to be loaded into the counter when the load signal is active.
dout: The expected or observed output of the counter.
This transaction data structure is used to communicate between the various components of the testbench.

**Generator**
The generator is responsible for creating randomized input sequences for the counter. It generates transactions with random values for loadin and control signals (up, load, rst) to thoroughly test the counter's ability to handle different counting scenarios.

**Driver**
The driver applies the generated transactions to the counter by setting the appropriate signals (loadin, up, load, rst) on the counter's interface. The driver operates in a continuous loop, sending the values to the DUT (Device Under Test) according to the clock signal, ensuring correct sequencing of inputs.

**Monitor**
The monitor observes the behavior of the counter by capturing the values of the counter’s output (dout) and input signals (loadin, up, rst, load). It checks the outputs over multiple clock cycles, taking into account the internal state transitions expected in a sequential circuit. The monitor forwards the observed values to the scoreboard for further validation.

**Scoreboard**
The scoreboard compares the actual output of the counter (dout) with the expected output based on the counter’s functionality. It ensures that the counter increments and decrements correctly when up is toggled, loads the correct value when load is active, and resets appropriately when rst is asserted.

**Environment**
The environment serves as the top-level module that instantiates and connects the generator, driver, monitor, and scoreboard. It manages the communication between these components using mailboxes and events, ensuring that data flows properly and in sync with the clock signal.

**Sequential Circuit Considerations**
Since the up and down counter is a sequential circuit, its behavior depends on both the current input signals and its internal state, which evolves over time. As a result, verifying this type of circuit requires:

Ensuring correct state transitions based on the control signals (up, load, rst).
Checking the output on every clock cycle to confirm the counter's correct operation over time.
Verifying the handling of asynchronous events like reset and synchronous operations like counting up or down.

**Conclusion**
This project provides a structured and modular approach to the verification of a sequential up and down counter. By using a combination of random stimulus generation, output monitoring, and scoreboard-based checking, this environment ensures that the counter performs as expected in a variety of scenarios. The environment is also flexible and can be easily extended to support more complex verification tasks.
