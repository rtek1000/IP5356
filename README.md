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
