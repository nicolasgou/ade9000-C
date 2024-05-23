
<h1 align="center">
  *** WORKING ON ***
</h1>
<h3 align="center">ADE9000 - High Performance, Multiphase Energy, and Power Quality Measurement IC</h3>
<h4 align="center">Analog Device ade9000 IC platform independent driver based on Standard C language</h4>

![analogDevice_C_ade9000](https://github.com/nicolasgou/ade9000-C/assets/45576249/b94bdc01-6026-456f-ad56-552b0f142273)



# 1 - Introduction

Analog Device ade9000 IC platform independent driver written in C programming language. This repository contains the sensor driver files (.h and .c) to be included, or linked directly as a git submodule, in your project. The driver is MISRA compliant and the documentation can be generated using the [Doxygen](http://www.doxygen.org/) tool.

In order to `clone` the complete content of the repository folder, use the command:

```
git clone https://github.com/nicolasgou/ade9000-C/
```

Some examples of driver usage can be found [reference examples](https://github.com/nicolasgou/ade9000-C/examples).

------



# 2 - Integration details

The driver is platform-independent, you only need to define two functions for read and write transactions from the sensor hardware bus  (ie. SPI or I²C). **A few devices integrate an extra bit in the communication protocol in order to enable multi read/write access, this  bit must be managed in the read and write functions defined by the user.** Please refer to the read and write implementation in the [reference examples](https://github.com/nicolasgou/ade9000-C/examples).



### 2.a Source code integration

- Include in your project the driver files of the sensor (.h and .c) 
- Define in your code the read and write functions that use the I²C or SPI platform driver like the following:

```
/** Please note that is MANDATORY: return 0 -> no Error.**/
int32_t platform_write(void *handle, uint8_t Reg,const uint8_t *Bufp, uint16_t len)
int32_t platform_read(void *handle, uint8_t Reg, uint8_t *Bufp, uint16_t len)
```

- Declare and initialize the structure of the device interface:

```
xxxxxxx_ctx_t dev_ctx; /** xxxxxxx is the used part number **/
dev_ctx.write_reg = platform_write;
dev_ctx.read_reg = platform_read;
```

- If needed by the platform read and write functions, initialize the handle parameter:

```
dev_ctx.handle = &platform_handle;
```

Some integration examples can be found [here](https://github.com/STMicroelectronics/STMems_Standard_C_drivers/tree/master/iis3dwb_STdC/examples).

### 2.b Required properties

> - A standard C language compiler for the target MCU
> - A C library for the target MCU and the desired interface (ie. SPI, I²C)

------

**More Information: [http://www.analog.com](https://www.analog.com/en/products/ade9000.html)**

