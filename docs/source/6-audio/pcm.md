# PCM interface

There are two PCM interface. 

But the primary PCM is set to SPI mode by default.

Primary PCM

| PinName | PIN Num | default Function | Function1 | Function2 | Function3 | Function4 |
| ------  | ------  | -------          | ------    | ------    |    ------  | ------   |
| SPI_CS_N|    37   | SPI_CS_N_BLSP6   | PCM_IN    |  I2S_IN   | GPIO22    | UART_RTS_BLSP6 |
| SPI_CS_N|    38   | SPI_MOSI_BLSP6   | PCM_OUT   |  I2S_OUT  | GPIO20    | UART_TXD_BLSP6 |
| SPI_CS_N|    39   | SPI_MISO_BLSP6   | PCM_SYNC  |  I2S_WS   | GPIO21    | UART_RXD_BLSP6 |
| SPI_CS_N|    40   | SPI_CLK_BLSP6    | PCM_CLK   |  I2S_CLK  | GPIO23    | UART_CTS_BLSP6 |

Secondary PCM

| PinName | PIN Num | defaultFunction | Function1 | Function2 | 
| ------  | ------  | -------         | ------    | ------    |
| PCM_IN  |    24   |       PCM_IN    |  I2S_IN   | GPIO76    |
| PCM_OUT |    25   |       PCM_OUT   |  I2S_OUT  | GPIO77    | 
| PCM_SYNC|    26   |       PCM_SYNC  |  I2S_WS   | GPIO79    | 
| PCM_CLK |    27   |       PCM_CLK   |  I2S_CLK  | GPIO78    | 


## PCM reference design

![](pcm_reference_design.png)

## 



