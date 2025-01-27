# SDRAM-controller



![image](https://github.com/user-attachments/assets/e1752530-87ba-4840-bf9d-c33c70ab882d)





SDRAM (Synchronous Dynamic Random Access Memory) refers to a type of memory. Synchronous means that the memory operates in synchronization with a clock signal, and the sending of commands and data transmission are based on this clock. Dynamic indicates that the storage array needs to be continuously refreshed to prevent data loss. This is because data in SDRAM is stored using capacitors, and as we know, capacitors naturally discharge over time. If the charge is completely discharged, the data in SDRAM will be lost. Therefore, SDRAM requires refreshing before the capacitors are fully discharged. Random means that the data is not stored sequentially in a linear order but is accessed by freely specifying an address for data read and write operations.

![image](https://github.com/user-attachments/assets/e71f5ee0-ff46-4d2a-9e8b-57a340ea2700)


SDRAM Capacity (bits)=Data Width×Total Number of Storage Units(Row Address Count×Column Address Count×Number of Banks)

this design is based on hynix 128Mb Synchronous DRAM (2M x 4Bank x 16 bits I/O)
![image](https://github.com/user-attachments/assets/e3723eab-7730-4e91-950e-6e4f435f8dd4)

clk = 50Mhz











## Table of Contents

- [Initialization](#Initialization)
- [Arbitration](#Arbitration)
- [Write](#Write)
- [Cmd_decode](#Cmd_decode)
- [FIFO](#FIFO)
- [FPGA](#FPGA)

![image](https://github.com/user-attachments/assets/9dfaba72-a7b7-4b86-b4e6-61632cd28d9e)










## Initialization

![image](https://github.com/user-attachments/assets/b6c00525-c111-483d-aade-bd9f990dc09e)

For the initialization process, a delay of 200 µs is first required. Once the delay is satisfied, a Precharge command is issued, followed by two Auto-refresh commands, and finally, the mode register configuration is performed.




## 1.command

![image](https://github.com/user-attachments/assets/9647e808-89e0-4ff9-82ff-398a944cd7f8)


##  2.Mode register Configuration

![image](https://github.com/user-attachments/assets/cb96247f-3e97-4a03-b31b-36fbe5c03957)


CMD:                          CS           RAS            CAS            WE           

Precharge:                    0             0              1             0

A-Refresh:                    0             0              0             1

NOP:                          0             1              1             1 

Mode-Set:                     0             0              0             0

addr  :  12'b0000_0011_0010                              


## 3.Initial Timing Diagram

![image](https://github.com/user-attachments/assets/c356371c-4f7b-4520-828f-78433a1382c6)






## 4.Simulation
![image](https://github.com/user-attachments/assets/279ba957-5981-4920-8290-bcb2b105b955)




## Arbitration
hynix 4096 Refresh cycles / 64ms (AO-A11 address: 2^12)





![image](https://github.com/user-attachments/assets/65daf9e8-92e1-4fcf-a675-f72fd00e3a9a)



## 1.Arbitration module state machine

![image](https://github.com/user-attachments/assets/836bc428-201f-4561-b858-817e3ecdec10)



## 2.auto refresh cycle
![image](https://github.com/user-attachments/assets/37f061e3-aada-41c8-a79f-924d9512833f)




## 3.auto refresh simulation
![image](https://github.com/user-attachments/assets/fca9e827-f051-4bb3-867d-4ec88556731a)





![image](https://github.com/user-attachments/assets/7249c36f-1e50-4b4b-9d5c-b6b548cb6d73)








## Write


## 1.Sequence Diagram
![image](https://github.com/user-attachments/assets/f9751c02-ea54-49e7-8f7c-adf3cf9341b4)


Assume we need to write two rows of data into the SDRAM. Under what conditions can the arbitration state machine exit the write state:

1.The data has been fully written;
2.The SDRAM needs to perform a refresh operation;
3.The data is not fully written, and the next row needs to be activated for writing.


## 2.Sequence Diagram

![image](https://github.com/user-attachments/assets/e0cfd45c-d1b3-464a-993c-fc0d89e89d3f)








## 3.Write module Timing design
![image](https://github.com/user-attachments/assets/445c3314-7f19-46ed-8c3c-1dcf27bece70)



## 4.Write command Timing design
![image](https://github.com/user-attachments/assets/381dbb8c-05ea-4a14-87af-86f798961805)






## Cmd_decode
## 1.Sequence Diagram

![image](https://github.com/user-attachments/assets/583837e8-c357-4ae6-a3e4-bbe8de501215)






## 2.cmd_decode simulation



![image](https://github.com/user-attachments/assets/d1538cfa-86bf-4647-8b38-20b4a0070231)









## FIFO

1.Writing to DRAM :sending 4 bytes of data via the serial port takes too long, while writing data to SDRAM is extremely fast. Therefore, FIFO buffering needs to be used to write the data.
2.Reading from SDRAM: Data read from SDRAM needs to be sent to the host computer. Since the SDRAM read speed is much faster than the serial port's data transmission rate, a FIFO buffer is required to store the data read from SDRAM.


## 1.write SDRAM timing design


![image](https://github.com/user-attachments/assets/b1e9fa4c-e034-4408-9402-50a6280ad523)



## 2.reaad SDRAM timing design


![image](https://github.com/user-attachments/assets/dfcbd6c9-6736-4a57-a2bc-ab21047bc80e)




## 3.FIFO design


![image](https://github.com/user-attachments/assets/722b264b-7a77-450a-86d0-2b1e5024aa3b)


clk = 50Mhz (same clk)





## FPGA

## Synthesis

![image](https://github.com/user-attachments/assets/856394dd-7951-423a-8b34-b8c6a69ab77b)

![image](https://github.com/user-attachments/assets/aefea7b2-4b0b-48f8-a9a5-aeefbc5e870a)


## modify (if-else)
![image](https://github.com/user-attachments/assets/318138ab-76bf-4fdb-9143-93cb4bc5a942)




## 2.Fitter(Place & Route)
![image](https://github.com/user-attachments/assets/49d26450-d5f0-4717-90cd-ceb403d42cdd)







