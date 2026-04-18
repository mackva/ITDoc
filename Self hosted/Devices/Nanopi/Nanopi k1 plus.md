![[NanoPi-K1-Plus-001.png]]

- CPU: Allwinner H5, Quad-core 64-bit high-performance Cortex™-A53
- GPU: Hexa-core Mali450
- DDR3 RAM: 2GB
- Ethernet: 10/100/1000M Ethernet using RTL8211E IC
- Wireless: 802.11 b/g/n and onboard PCB antenna
- Infrared: Onboard infrared receiver
- Audio: 3.5mm audio jack/Via HDMI
- Mic: onboard microphone
- eMMC: onboard eMMC interface
- I2S: onboard I2S interface(7Pin, 2.54mm pin-header)
- MicroSD Slot: MicroSD card slot
- USB Host: 3 x USB 2.0 Host, type A port
- DVP Camera interface: 24-Pin, 0.5mm pitch FPC seat
- MicroUSB: 1 x USB 2.0, OTG, for power input and data transmission
- HDMI: HDMI Type-A port. It supports 4K@30fps dsplay
- Video Output: HDMI 1.4. It supports 4K@30fps display, CVBS
- GPIO Pin-header: 40 Pin,2.54mm pitch pin-header containing I2C, GPIO, UART, PWM, SPDIF, SPI and etc
- Serial Debug Port: 4Pin, 2.5mm pitch pin-header
- Button: 1 x GPIO button(user configurable)
- LED: 1 x power LED and 1 x status LED
- Power Interface: MicroUSB
- PCB Size:56 x 85mm, 6-layer, ENIG
- Power: DC 5V/2A

#### **GPIO Pin Spec**

| Pin# | Name                                     | Linux gpio | Pin# | Name                                       | Linux gpio |
| ---- | ---------------------------------------- | ---------- | ---- | ------------------------------------------ | ---------- |
| 1    | SYS_3.3V                                 |            | 2    | VDD_5V                                     |            |
| 3    | I2C0_SDA / GPIOA12                       |            | 4    | VDD_5V                                     |            |
| 5    | I2C0_SCL / GPIOA11                       |            | 6    | GND                                        |            |
| 7    | GPIOG11                                  | 203        | 8    | UART1_TX / GPIOG6                          | 198        |
| 9    | GND                                      |            | 10   | UART1_RX / GPIOG7                          | 199        |
| 11   | UART2_TX / GPIOA0                        | 0          | 12   | GPIOA6                                     | 6          |
| 13   | UART2_RTS / GPIOA2                       | 2          | 14   | GND                                        |            |
| 15   | UART2_CTS / GPIOA3                       | 3          | 16   | UART1_RTS / GPIOG8                         | 200        |
| 17   | SYS_3.3V                                 |            | 18   | UART1_CTS / GPIOG9                         | 201        |
| 19   | SPI0_MOSI / GPIOC0                       | 64         | 20   | GND                                        |            |
| 21   | SPI0_MISO / GPIOC1                       | 65         | 22   | UART2_RX / GPIOA1                          | 1          |
| 23   | SPI0_CLK / GPIOC2                        | 66         | 24   | SPI0_CS / GPIOC3                           | 67         |
| 25   | GND                                      |            | 26   | SPDIF-OUT / GPIOA17                        | 17         |
| 27   | I2C1_SDA / GPIOA19 / PCM0_CLK / I2S0_BCK | 19         | 28   | I2C1_SCL / GPIOA18 / PCM0_SYNC / I2S0_LRCK | 18         |
| 29   | GPIOA20 / PCM0_DOUT / I2S0_SDOUT         | 20         | 30   | GND                                        |            |
| 31   | GPIOA21 / PCM0_DIN/ I2S0_SDIN            | 21         | 32   | GPIOA7                                     | 7          |
| 33   | GPIOA8                                   | 8          | 34   | GND                                        |            |
| 35   | UART3_CTS / SPI1_MISO / GPIOA16          | 16         | 36   | UART3_TX / SPI1_CS / GPIOA13               | 13         |
| 37   | GPIOA9                                   | 9          | 38   | UART3_RTS / SPI1_MOSI / GPIOA15            | 15         |
| 39   | GND                                      |            | 40   | UART3_RX / SPI1_CLK / GPIOA14              | 14         |

#### **eMMC Connector Pin Spec**

| Pin# | Name     | Pin# | Name     |
| ---- | -------- | ---- | -------- |
| 1    | eMMC_D0  | 2    | eMMC_D1  |
| 3    | eMMC_D2  | 4    | eMMC_D3  |
| 5    | eMMC_D4  | 6    | eMMC_D5  |
| 7    | eMMC_D6  | 8    | eMMC_D7  |
| 9    | eMMC_DS  | 10   | GND      |
| 11   | eMMC_CMD | 12   | eMMC_CLK |
| 13   | NC       | 14   | GND      |
| 15   | NC       | 16   | 1.8V OUT |
| 17   | eMMC_RST | 18   | 3.3V OUT |
| 19   | GPIOY_5  | 20   | GND      |

#### **Debug Port（UART0）**

| Pin# | Name    |
| ---- | ------- |
| 1    | GND     |
| 2    | VDD_5V  |
| 3    | UART_TX |
| 4    | UART_RX |

#### **7Pin I2S Pin Spec**

|   |   |
|---|---|
|Pin#|Name|
|1|GND|
|2|SYS_3.3V|
|3|I2S0_BCK|
|4|I2S0_LRCK|
|5|I2S0_SDOUT|
|6|I2S0_SDIN|
|7|I2S_MCLK|
#### **Notes**
1. SYS_3.3V: 3.3V power output
2. VDD_5V: 5V power input/output. Input power range: 4.7～5.5V
3. All signal pins are 3.3V

#### Ссылки: 
1) [NanoPi K1 Plus](https://wiki.friendlyelec.com/wiki/index.php/NanoPi_K1_Plus)
2) [Use NetworkManager to configure network settings](https://wiki.friendlyelec.com/wiki/index.php/Use_NetworkManager_to_configure_network_settings)