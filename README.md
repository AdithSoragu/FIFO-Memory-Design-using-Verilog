# 🚀 FIFO Memory Design using Verilog HDL

<p align="center">
  <img src="https://img.shields.io/badge/Language-Verilog-blue">
  <img src="https://img.shields.io/badge/Simulation-ModelSim-green">
  <img src="https://img.shields.io/badge/Status-Completed-success">
</p>

---

# 📌 Introduction

FIFO (First In First Out) is a temporary memory buffer widely used in digital systems for storing and transferring data between hardware modules operating at different speeds.

In FIFO memory:
- The **first data written** into memory
- becomes the **first data read** from memory

FIFO acts exactly like a queue in real life.

This project implements a **Synchronous FIFO Memory** using **Verilog HDL** with configurable:
- FIFO depth
- Data width
- Read and write operations
- Full and empty status detection

The project also includes a complete Verilog testbench for simulation and waveform verification.

---

# 🎯 Project Objectives

The main objectives of this project are:

- Design a synchronous FIFO memory
- Implement FIFO using Verilog HDL
- Perform read and write operations
- Generate FIFO full and empty flags
- Verify FIFO functionality using simulation
- Analyze waveform outputs

---

# 🧠 FIFO Concept

FIFO stands for:

> **First In First Out**

The data that enters first will leave first.

---

## 📖 Example

| Operation | Data |
|-----------|------|
| Write | 10 |
| Write | 20 |
| Write | 30 |

### Read Order

```text
10 → 20 → 30
```

The order of data remains unchanged.

---

# 🏗️ FIFO Architecture

The FIFO design consists of:

- Memory Array
- Write Pointer
- Read Pointer
- Full Detection Logic
- Empty Detection Logic
- Control Signals

---

# 📂 Project Directory Structure

```text
FIFO_Design/
│
├── fifo.v           # FIFO Design Module
├── tb_fifo.v        # Testbench File
├── dump.vcd         # Waveform Dump File
└── README.md        # Documentation
```

---

# ⚙️ FIFO Specifications

| Parameter | Value |
|-----------|-------|
| FIFO Type | Synchronous FIFO |
| FIFO Depth | 8 |
| Data Width | 16-bit |
| Clock | Single Clock |
| Reset | Active Low |
| HDL Used | Verilog HDL |

---

# 🛠️ Software and Tools Used

| Tool | Purpose |
|------|----------|
| Verilog HDL | Hardware Design |
| ModelSim | Simulation |
| QuestaSim | Verification |
| GTKWave | Waveform Viewing |

---

# 📌 FIFO Input Signals

| Signal | Type | Description |
|--------|------|-------------|
| clk | Input | System Clock |
| rst_n | Input | Active Low Reset |
| cs | Input | Chip Select |
| wr | Input | Write Enable |
| rd | Input | Read Enable |
| data_in | Input | Input Data |

---

# 📌 FIFO Output Signals

| Signal | Type | Description |
|--------|------|-------------|
| data_out | Output | Output Data |
| fifo_empty | Output | FIFO Empty Flag |
| fifo_full | Output | FIFO Full Flag |

---

# 🔄 FIFO Working Operation

## ✏️ Write Operation

Data is written into FIFO when:

```text
cs = 1
wr = 1
fifo_full = 0
```

### Steps:
1. Input data is stored in memory
2. Write pointer increments
3. FIFO status updates

---

## 📖 Read Operation

Data is read from FIFO when:

```text
cs = 1
rd = 1
fifo_empty = 0
```

### Steps:
1. Data is fetched from memory
2. Read pointer increments
3. FIFO status updates

---

# 🧩 Verilog Design Explanation

## 📌 Memory Declaration

```verilog
reg [DATA_WIDTH-1:0] mem [0:FIFO_DEPTH-1];
```

Creates FIFO memory storage.

- Depth = 8
- Width = 16-bit

---

## 📌 Write Pointer

```verilog
reg [FIFO_DEPTH_LOG:0] wr_ptr;
```

Tracks the write location.

---

## 📌 Read Pointer

```verilog
reg [FIFO_DEPTH_LOG:0] rd_ptr;
```

Tracks the read location.

---

# 📝 Write Logic

```verilog
always @(posedge clk or negedge rst_n)
```

The write operation occurs at every positive edge of the clock.

---

## Write Condition

```verilog
if (cs && wr && !fifo_full)
```

Data is written only when FIFO is not full.

---

## Memory Write

```verilog
mem[wr_ptr[FIFO_DEPTH_LOG-1:0]] <= data_in;
```

Stores incoming data into FIFO memory.

---

## Pointer Increment

```verilog
wr_ptr <= wr_ptr + 1'b1;
```

Moves the write pointer to the next location.

---

# 📖 Read Logic

```verilog
always @(posedge clk or negedge rst_n)
```

The read operation also occurs at positive clock edge.

---

## Read Condition

```verilog
if (cs && rd && !fifo_empty)
```

Data is read only when FIFO contains data.

---

## Memory Read

```verilog
data_out <= mem[rd_ptr[FIFO_DEPTH_LOG-1:0]];
```

Reads stored data from FIFO.

---

## Pointer Increment

```verilog
rd_ptr <= rd_ptr + 1'b1;
```

Moves the read pointer forward.

---

# 📌 FIFO Empty Logic

```verilog
assign fifo_empty = (rd_ptr == wr_ptr);
```

FIFO becomes empty when:
- Read pointer equals write pointer

---

# 📌 FIFO Full Logic

```verilog
assign fifo_full =
(rd_ptr == {~wr_ptr[FIFO_DEPTH_LOG],
wr_ptr[FIFO_DEPTH_LOG-1:0]});
```

FIFO becomes full when:
- Write pointer wraps around
- Write pointer catches the read pointer

---

# 🧪 Testbench Description

The testbench verifies FIFO functionality using multiple scenarios.

---

## ✅ Scenario 1

### Operations:
- Write 1
- Write 10
- Write 100
- Read all values

### Expected Output

```text
1 → 10 → 100
```

---

## ✅ Scenario 2

### Operations:
- Simultaneous read and write
- Continuous FIFO operation

Purpose:
- Verify real-time FIFO functionality

---

## ✅ Scenario 3

### Operations:
- Fill FIFO completely
- Verify FIFO full condition
- Read entire FIFO contents
- Verify FIFO empty condition

---

---


# 🚀 Applications of FIFO

FIFO memories are widely used in:

- UART Communication
- DMA Controllers
- Audio Streaming
- Video Processing
- Packet Buffering
- Embedded Systems
- Processor Communication
- Networking Devices

---

# ✅ Advantages of FIFO

- Simple architecture
- Fast data buffering
- Reliable data transfer
- Prevents data loss
- Efficient memory utilization

---

# 👨‍💻 Author

## Adith Soragu

Electronics and Communication Engineering


