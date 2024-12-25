# VHDL Signal Assignment Race Condition
This repository demonstrates a common coding error in VHDL: a race condition caused by improper signal assignment within a process.  The example showcases a scenario where the output signal isn't reliably updated due to the timing of signal updates inside the process.

## Bug Description
The provided VHDL code attempts to simply register an input signal.  However, the assignment of `internal_reg` and `data_out` within the same `rising_edge` could lead to unpredictable behavior in hardware.  The synthesis tool might optimize these assignments in a way that the output `data_out` does not reflect the latest value of the input `data_in` in every clock cycle.

## Solution
The solution introduces an additional signal to decouple the assignments of `data_in` to `internal_reg`, and `internal_reg` to `data_out`. This ensures that `data_out` always receives the previous clock cycle's value of `data_in`.