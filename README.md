# IP5356
Some data about the IP5356 component provided by the manufacturer [Yingjixin Technology](https://www.injoinic.com/)
- (This IC has I2C communication, and can be found in Power Bank with display)

![img](https://raw.githubusercontent.com/rtek1000/IP5356/refs/heads/main/Doc/IP5356_Power_Bank_board.jpg)

The manufacturer's website only shows the Datasheets without the I2C communication registers:
- (The manufacturer's website is written only in Chinese, but most of the text can be automatically translated using Google)
![img](https://raw.githubusercontent.com/rtek1000/IP5356/refs/heads/main/Doc/Datasheets.png)

Fortunately the manufacturer sent me the I2C register file for the IP5356 IC:
- (The email I sent had a Chinese translation followed by the English text, asking where to find the I2C part information)

![img](https://raw.githubusercontent.com/rtek1000/IP5356/refs/heads/main/Doc/Contact.png)

#### Note:

- ##### If you want to modify a register of IP5356, you need to read out the value of the corresponding register first, perform the and or operation on the bit to be modified, and then write the calculated value into this register, ensure that only the bit to be modified and the value of other open bits cannot be changed at will. The default value of the register is based on the read value. The IC default values may vary from batch to batch.

- Notes found in the PDF file about I2C:
1) The IP5356_LED_CL standard supports I2C by default.

2) The maximum frequency of IP5356 I2C supports 300K. Considering the MCU clock deviation, it is recommended to use about 200K clock for MCU communication when applying I2C.

3) When the IP5356 switches from hibernation state to working state (key, load access, 5V charging access), the IP5356 first detects whether L1 and L2 pins are pulled up to 3.3V (VCC). If L1 and L2 are pulled up to 3.3V at the same time, the IP5356 enters the I2C mode, and L3 outputs a high level of 3.1V. If L1 and L2 are not detected at the same time, it will enter the LED light display mode, and will detect each time it enters the working state from sleep.

4) Since I2C detection will be carried out when IP5356 enters the working state from hibernation, the MCU needs to configure SDA and SCK as input or high-resistance states during hibernation, and cannot read and write I2C data until the INT is detected to be high for more than 100ms. Otherwise, the IC cannot enter the I2C state because L1 or L2 is not pulled up when it enters the working state from sleep.

5) Since the IP5356 will perform I2C detection when it enters the working state from hibernation and the digital level inside IP5356 is 3.3V, the MCU must have VCC power supply. If the MCU uses an external LDO power supply, when the BAT is out of power or less than 2V, the VIN will connect 5V to supply power to the IP5356. The VCC system will perform I2C detection when the power is on, but the MCU has no power, and the status of SDA and SCK is uncertain, which may lead to the failure of L1
and L2 to enter I2C mode without detecting pull-up.

6) If you want to modify a register of IP5356, you need to read out the value of the corresponding register first, perform the and or operation on the bit to be modified, and then write the calculated value into this register, ensure that only the bit to be modified and the value of other open bits cannot be changed at will. The default value of the register is based on the read value. The IC default values may vary from batch to batch.

7) MCU operation process: INT continuous high 100ms can read and write the I2C register, you can initialize the register (need to modify the special function to modify the register, if you do not need to modify the register can not write the register) and then read the IC internal information (power, charge and discharge state, key state) characteristic requirements (such as special indicator, charge and discharge management, fast charge request management) operation.

8) IP5356 has two groups of I2C addresses, namely 0xEA and 0xE8. When reading and writing registers, you need to check whether the I2C address corresponding to the current register address is 0xE8 or 0XEA.

9) The default value of the IP5356 register is only for customers to refer to the configuration of the current function. If you need to operate the register, you need to read it out and calculate it before writing it back to the register.
