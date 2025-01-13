# SDRAM-controller

SDRAM (Synchronous Dynamic Random Access Memory) refers to a type of memory. Synchronous means that the memory operates in synchronization with a clock signal, and the sending of commands and data transmission are based on this clock. Dynamic indicates that the storage array needs to be continuously refreshed to prevent data loss. This is because data in SDRAM is stored using capacitors, and as we know, capacitors naturally discharge over time. If the charge is completely discharged, the data in SDRAM will be lost. Therefore, SDRAM requires refreshing before the capacitors are fully discharged. Random means that the data is not stored sequentially in a linear order but is accessed by freely specifying an address for data read and write operations.

![image](https://github.com/user-attachments/assets/e71f5ee0-ff46-4d2a-9e8b-57a340ea2700)


SDRAM Capacity (bits)=Data Width×Total Number of Storage Units(Row Address Count×Column Address Count×Number of Banks)

this design is based on hynix 128Mb Synchronous DRAM (2M x 4Bank x 16 bits I/O)
![image](https://github.com/user-attachments/assets/e3723eab-7730-4e91-950e-6e4f435f8dd4)













## Table of Contents

- [Initialization](#Initialization)
- [Arbitration](#Arbitration)
- [API](#API)
- [Contributing](#Contributing)
- [License](#License)



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








## License
