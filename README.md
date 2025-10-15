# UVM Sequence Library Usage Pattern

This repository provides a focused, self-contained implementation of the **`uvm_sequence_library`** feature in UVM. This project illustrates an advanced UVM technique for creating scalable and maintainable test suites by managing a collection of sequences as a single, configurable entity.

---

### Project Overview

In complex verification environments, managing dozens or even hundreds of individual sequences can be challenging. The `uvm_sequence_library` is a powerful base class that simplifies this task by acting as a container for other sequences. It allows a test to run a collection of sequences in various modes (e.g., random, random-cyclic, in-order) without needing to start each one manually.

This implementation shows how to:
1.  Define a sequence library class that inherits from `uvm_sequence_library`.
2.  Programmatically add individual sequences (`seq1`, `seq2`) to the library using `add_typewide_sequence()`.
3.  Configure the library's execution mode (`selection_mode = UVM_SEQ_LIB_RANDC`).
4.  Configure the number of sequences to run (`min/max_random_count`).
5.  Start the entire library as a single sequence from a UVM test.

---

### File Structure

-   `sequence_library_test.sv`: A single SystemVerilog file containing the complete UVM code, including the transaction, individual sequences, the sequence library, a minimal UVM environment, and the top-level test.

---

### Key Concepts Illustrated

-   **`uvm_sequence_library`**: The core component, which inherits from `uvm_sequence` and can execute other sequences.
-   **`add_typewide_sequence()`**: The function used to programmatically register sequences with the library, offering a flexible alternative to macros.
-   **`selection_mode`**: A property of the sequence library that controls the order of execution. This example uses `UVM_SEQ_LIB_RANDC` (Random-Cyclic), which runs all registered sequences one time in a random order before repeating.
-   **Test-Level Configuration**: Shows how a UVM test can create, configure, and launch the sequence library, demonstrating a clean separation of test intent from the underlying sequences.

---

### How to Run

1.  Compile `sequence_library_test.sv` using a simulator that supports SystemVerilog and UVM.
2.  Set `top` as the top-level module for simulation.
3.  Execute the simulation. The log will show the sequence library being configured and then starting a random number of sequences (between 5 and 10) in a random-cyclic order.
