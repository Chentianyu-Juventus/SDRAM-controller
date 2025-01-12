# SDRAM-controller

SDRAM (Synchronous Dynamic Random Access Memory) refers to a type of memory. Synchronous means that the memory operates in synchronization with a clock signal, and the sending of commands and data transmission are based on this clock. Dynamic indicates that the storage array needs to be continuously refreshed to prevent data loss. This is because data in SDRAM is stored using capacitors, and as we know, capacitors naturally discharge over time. If the charge is completely discharged, the data in SDRAM will be lost. Therefore, SDRAM requires refreshing before the capacitors are fully discharged. Random means that the data is not stored sequentially in a linear order but is accessed by freely specifying an address for data read and write operations.

![image](https://github.com/user-attachments/assets/e71f5ee0-ff46-4d2a-9e8b-57a340ea2700)


SDRAM Capacity (bits)=Data Width×Total Number of Storage Units(Row Address Count×Column Address Count×Number of Banks)

this design is based on hynix 128Mb Synchronous DRAM (2M x 4Bank x 16 bits I/O)
![image](https://github.com/user-attachments/assets/e3723eab-7730-4e91-950e-6e4f435f8dd4)













## Table of Contents

- [Initialization](#Initialization)
- [Configuration](#Configuration)（可选）
- [Usage](#Usage)
- [API](#API)
- [Contributing](#Contributing)
- [License](#License)



## Initialization

![image](https://github.com/user-attachments/assets/b6c00525-c111-483d-aade-bd9f990dc09e)

For the initialization process, a delay of 200 µs is first required. Once the delay is satisfied, a Precharge command is issued, followed by two Auto-refresh commands, and finally, the mode register configuration is performed.




command
![image](https://github.com/user-attachments/assets/9647e808-89e0-4ff9-82ff-398a944cd7f8)

CMD:                          CS           RAS            CAS            WE           

Precharge:                    0             0              1             0

A-Refresh:                    0             0              0             1

NOP:                          0             1              1             1 

Mode-Set:                     0             0              0             0

## Configuration





## API



## Contributing



## License
