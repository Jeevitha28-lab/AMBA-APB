# AMBA APB Protocol Implementation (Verilog)

## 📖 Overview

This project implements the **AMBA Advanced Peripheral Bus (APB)** protocol in **Verilog HDL**. It demonstrates communication between a **single APB Master** and **three APB Slaves** through an **Address Decoder**, along with a complete **Testbench** for simulation.

The design performs automatic **write** and **read** transactions to each slave using a Finite State Machine (FSM), making it suitable for learning APB protocol fundamentals and FPGA/ASIC digital design.

---

## 🚀 Features

- Single APB Master
- Three APB Slave modules
- APB Address Decoder
- APB Top Module
- Complete Testbench
- FSM-based Master Controller
- Automatic Write & Read Operations
- Memory-based Slave Storage
- Ready (PREADY) Handshake Support
- Simulation Waveform Generation (VCD)

---

## 🏗️ Project Architecture

```
                 +----------------+
                 |   APB Master   |
                 +--------+-------+
                          |
                          |
                    Address/Data Bus
                          |
                +---------+---------+
                |   APB Decoder     |
                +----+-----+-----+--+
                     |     |     |
                     |     |     |
                 Slave1 Slave2 Slave3
```

---

## 📂 Project Structure

```
AMBA-APB/
│
├── apb3_master.v
├── apb3_slave.v
├── apb3_decoder.v
├── apb_fpga_top.v
├── apb3_tb.v
└── README.md
```

---

## ⚙️ Modules

### 1. APB Master
- FSM-based controller
- Performs write and read transactions
- Generates APB control signals
- Communicates with all three slaves

### 2. APB Slave
- 256 × 8-bit memory
- Supports write operation
- Supports read operation
- Generates PREADY signal

### 3. Address Decoder
Selects slave based on upper address bits.

| Address Range | Selected Slave |
|---------------|----------------|
| 0x00 – 0x0F | Slave 1 |
| 0x10 – 0x1F | Slave 2 |
| 0x20 – 0x2F | Slave 3 |

---

## 🔄 APB Transaction Flow

### Write Transaction

```
IDLE
   ↓
SETUP WRITE
   ↓
ENABLE WRITE
```

### Read Transaction

```
SETUP READ
     ↓
ENABLE READ
     ↓
DONE
```

---

## 📝 Sample Transactions

| Slave | Address | Write Data |
|--------|---------|------------|
| Slave 1 | 0x05 | 0x11 |
| Slave 2 | 0x15 | 0x22 |
| Slave 3 | 0x25 | 0x33 |

The master writes data to each slave and immediately performs a read to verify the stored value.

---

## 🛠️ Simulation

The supplied testbench performs:

- Clock Generation
- Reset Generation
- Automatic APB Transactions
- Read/Write Verification
- Waveform Dump Generation

Output waveform:

```
apb_wave.vcd
```

---

## ▶️ Run Simulation

Using Icarus Verilog:

```bash
iverilog -o apb_sim apb3_master.v apb3_slave.v apb3_decoder.v apb_fpga_top.v apb3_tb.v
vvp apb_sim
gtkwave apb_wave.vcd
```

---

## 📚 APB Signals

| Signal | Description |
|---------|-------------|
| PCLK | APB Clock |
| PRESETn | Active Low Reset |
| PSEL | Slave Select |
| PENABLE | Transfer Enable |
| PWRITE | Read/Write Control |
| PADDR | Address Bus |
| PWDATA | Write Data |
| PRDATA | Read Data |
| PREADY | Slave Ready |

---

## 🎯 Applications

- FPGA Design
- ASIC Design
- Digital System Design
- AMBA Bus Learning
- Embedded Systems
- SoC Design

---

## 🧪 Tools Used

- Verilog HDL
- Icarus Verilog
- GTKWave
- FPGA Simulation Environment

---

## 📌 Future Improvements

- APB4 Protocol Support
- Wait State Handling
- Error Response (PSLVERR)
- Multiple APB Masters
- Interrupt Support
- FPGA Hardware Implementation

---

## 👨‍💻 Author

**Jeevitha C R**

GitHub: https://github.com/Jeevitha28-git

---

## 📄 License

This project is developed for educational and learning purposes.
