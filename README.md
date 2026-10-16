<!-- GitHub profile README: create a public repo named exactly <your-username> and drop this in as README.md -->

# Hi, I'm Aaryan!

**Electronics Engineering @ Texas A&M** · Digital design, AI hardware, and power/instrumentation

I work where silicon meets software: profiling ML workloads to find the real bottleneck, then designing the hardware that removes it. Currently building RTL for transformer inference accelerators and a low-latency FPGA trading pipeline with **REV Silicon** (AI Architecture / RTL Design Team).

---

## 🔬 Featured Projects

### LLM Inference Profiling → Systolic Accelerator `in progress`
Measured where TinyLlama-1.1B actually spends time, then sized hardware to the data.
- Profiled TinyLlama-1.1B (4-bit, `bitsandbytes`) on a T4 with `torch.profiler`
- Roofline analysis: batch-1 decode is **memory-bound in both attention and FFN** (≈4 FLOPs/byte vs. T4 ridge point ≈203). The usual "FFN is compute-bound" assumption breaks at batch 1 because matrix dimensions cancel out of the intensity ratio
- Designed an **8×8 weight-stationary systolic PE tile** sized to the measured `gate_proj` shape (2048×5632); ~230 ns first-principles latency estimate
- Phase 3: SystemVerilog RTL — single PE verified in Icarus; full array → Verilator next

`Python` `PyTorch` `SystemVerilog` `Icarus Verilog` `Verilator`

### Transformer Inference ASIC — TinyTapeout / SKY130 `REV Silicon`
Team tapeout of a quantized transformer accelerator under TinyTapeout's area, pin, and no-SRAM constraints.
- 4×4 weight-stationary INT8 PE array, 7-state control FSM (Idle → Load W → Load A → Compute → Drain → Postproc → Done)
- DFF-based storage (no SRAM macro in the OpenLane flow), DDR input sampling to double pin bandwidth
- Wrote the bit-accurate **C golden model** (incl. int32→int8 saturating requantization) and a layered **host driver** (register map → HAL w/ mock backend → API → unit tests)
- Second, unconstrained accelerator variant in active design

`SystemVerilog` `C` `OpenLane` `Yosys` `Verilator` `cocotb` `SKY130`

### FPGA Tick-to-Trade Pipeline — ETF Arbitrage `REV Silicon` `in design`
Nasdaq TotalView-ITCH ingest to OUCH order egress for QQQ vs. Nasdaq-100 arbitrage.
- Ingress → decompose (MoldUDP64/ITCH 5.0) → core compute → deterministic pre-trade risk gate → OUCH compose
- Tiered "fast/slow" architecture keeps ML off the nanosecond critical path (LUT/quantized micro-inference only)
- Python golden models with `pytest` for ITCH parsing, incremental NAV, and checksum generation
- Target: AMD Kria KR260, 10GBASE-R

`SystemVerilog` `Python` `pytest` `Vivado` `cocotb`

### Digital Logic on FPGA
Coursework designs implemented and verified on a DE10-Lite: 7-segment HEX decoder (SOP/POS), 3-bit two's-complement negator in NAND-only logic, structural Verilog + testbenches.

`Verilog` `Quartus` `ModelSim`

---

## 🏭 Experience

**Electrical & Instrumentation Engineering Intern** — ExxonMobil, Golden Pass LNG (Summer 2026)
Authored a standardized Electrical DMCC walkdown checklist grounded in NEC, NFPA 70E, NETA ATS, and IEEE standards.

**Undergraduate Researcher** — AI × Cybersecurity
Building and modifying test benches in Rust.

**Undergraduate Researcher** — AI in Education (w/ Prof. Ross Greer)

---

## 🛠️ Toolbox

| Area | Tools |
| --- | --- |
| HDL & Verification | SystemVerilog, Verilog, Verilator, Icarus, cocotb, ModelSim |
| ASIC / FPGA | OpenLane, OpenROAD, Yosys, SKY130, Quartus, Vivado |
| Languages | C, Python, Rust, C++ (learning) |
| ML / Profiling | PyTorch, `torch.profiler`, bitsandbytes, roofline analysis |
| Standards | NEC, NFPA 70E, NETA ATS, IEEE |

## 📈 Currently Learning
C++ · ROS 2 · FPGA timing closure · power electronics (closed-loop buck converter planned)

## 🏃 Off the bench
Love all kinds of sports, robotics, and traveling!
---

📫 [LinkedIn](https://www.linkedin.com/in/aaryan-gujarathi/) · [Email](aaryang2007@tamu.edu)
