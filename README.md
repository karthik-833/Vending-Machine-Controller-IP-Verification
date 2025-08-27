# Vending-Machine-Controller-IP-Verification
## Overview  
This repository contains the *SystemVerilog UVM-based verification environment* for the *Vending Machine Controller (VMC) IP*, designed as per the official specification document.  

The DUT (Design Under Test) implements a *configurable vending machine controller* with support for multiple items, currency denominations, and operational modes. The verification environment ensures *functional correctness, interface compliance, and robustness* under different operating conditions.  


## Verification Objectives  
- Validate *reset, configuration, and operational states*  
- Verify *APB-based register interface* functionality  
- Ensure correctness of *item dispense* and *currency change* logic  
- Check *error scenarios* including invalid item selection, underpayment, and out-of-stock conditions  
- Confirm *timing requirements* (≤10 cycles latency per dispense, one output per transaction)  
- Achieve *functional and code coverage* for verification sign-off  


##  DUT Specification Highlights  
- *System Clock:* 100 MHz  
- *Config Interface:* APB @ 50 MHz  
- *Max Items Supported:* 1024 (parameterized)  
- *Supported Currency Values:* {5, 10, 15, 20, 50, 100 INR}  
- *Latency Requirement:* ≤10 system clock cycles per dispense  
- *Operating Modes:* Reset, Configure, Operation  


## Verification Environment (UVM)  
- *Methodology:* UVM (Universal Verification Methodology)  
- *Language:* SystemVerilog  
- *Key Components:*  
  - cfg_agent → APB configuration transactions  
  - currency_agent → Currency input stimulus  
  - item_agent → Item selection stimulus  
  - dispense_agent → Passive monitor for DUT outputs  
  - *Scoreboard & Reference Model* → Functional correctness  
  - *Assertions (SVA)* → FSM and protocol compliance  


## Test Plan Categories  
1. *Reset Tests* – Verify reset clears registers and FSM states  
2. *Configuration Tests* – APB read/write operations, invalid accesses, edge cases  
3. *Operation Tests*  
   - Exact payment  
   - Overpayment with change return  
   - Underpayment rejection  
   - Multi-part currency insertion  
   - Zero-stock handling  
   - Invalid item selection  
4. *Randomized & Stress Tests* – Mixed operations to uncover corner cases  
5. *Timing Tests* – Latency ≤10 cycles, enforce single-output-per-transaction  
6. *Integration Tests* – Complete system validation (config → operation → monitoring)  


##  Bugs Identified in DUT  
- *Unused APB signal:* pready declared but not functionally used  
- *Clock domain issue:* No synchronization for asynchronous slow currency clock (10 kHz–50 MHz)  
- *FSM bug:* Incorrect handling when currency is inserted during cfg_mode  
- *Dispense issue:* Multiple dispense pulses generated in random stress conditions

## 🔗 Reference
Full code and testbench are available here on *EDA Playground*:  
 [Run on EDA Playground](https://edaplayground.com/x/w234)
