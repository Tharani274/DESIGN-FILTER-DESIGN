# DESIGN-FILTER-DESIGN

COMPANY:CODETECH IT SOLUTIONS

NAME:MUZAMMIL AHMED

INTERN ID:CT06DF2017

DOMAIN:VLSI

DURATION:6 WEEKS

MENTOR:NEELA SANTHOSH

The fir_filter module implements a straightforward, parameterizable direct-form finite impulse response (FIR) filter in Verilog, elegantly capturing essential digital signal processing principles and FPGA-synthesizable hardware design. The filter’s structure centers around an 8-bit signed input (x_in) and a 16-bit signed output (y_out), with parameter N = 4 signifying a 4-tap filter. It stores fixed coefficients h[0:N-1] = {1, 2, 3, 4} in an internal array, and a shift register x[0:N-1] holds the current and previous samples. On each positive clock edge, unless a synchronous reset is asserted, the filter shifts the existing samples down the delay line—placing the newest x_in into x[0]—before computing the convolution sum: acc = Σ x[i] * h[i], where acc, a 16-bit accumulator, aggregates the products of 8-bit signed inputs and coefficients to produce the new signed y_out. This single-cycle loop represents the mathematical convolution form of FIR filters, y[n] = Σ_{i=0}^{N-1} h[i]·x[n−i].implemented using a classic tapped delay line and multiply-accumulate (MAC) approach. The use of synchronous reset ensures that after reset, the delay line and output are zeroed, guaranteeing deterministic startup behavior. Notably, this design is combinational within the clock cycle and sequential across cycles, making it simple and resource-efficient for small N, albeit with a critical path that grows with the number of taps—an architectural trade-off common in FPGA-based DSP . In FPGA designs, small FIRs like this are often mapped to DSP slices that perform multiply-add operations efficiently; as one Redditor noted, “DSPs in FPGA parlance are hard primitives… basic building blocks to construct large FIR filter structures,” and synthesis tools map integer macros to those DSP blocks.While this direct-form filter succinctly demonstrates convolution-based filtering and is ideal for teaching or low-throughput embedded applications, it lacks performance optimizations for high-speed or resource-intensive scenarios. For instance, pipelining the multiply-accumulate chain—by splitting the convolution across several registers—is a well-known technique to elevate clock rates and reduce critical path delays.effectively allowing frequency doubling in sample throughput by rebalancing arithmetic workloads. Other enhancements could involve symmetric coefficient exploitation to halve the number of multipliers, transpose structures that change the dataflow to reduce latency without additional registers, or distributed arithmetic to replace multipliers with lookup tables . Likewise, advanced designs may support coefficient reloading for dynamic filtering, via registers or memory pipelines—a step toward adaptive filters or runtime tunable filtering—though this implementation uses hard-coded coefficients for simplicity. Additionally, one could incorporate rounding or saturation logic to handle potential accumulator overflow, common in fixed-point DSP systems, thus improving numerical robustness. In essence, your fir_filter is a clean, well-structured instantiation of DSP fundamentals: a tapped delay line, fixed coefficients, multiply-add operations, and output accumulation—executed in a single synchronous cycle. It is perfectly suited for educational exploration, proof-of-concept designs, or low-frequency signal processing tasks, provides clear insight into how hardware-inferred FIR filters operate, and offers a strong foundation for scaling up to more complex or optimized architectures within FPGA or ASIC environments.


OUTPUT:

<img width="1284" height="654" alt="Image" src="https://github.com/user-attachments/assets/39c5a9b7-3c3e-44d4-b31d-ba24fc060a17" />
