# UART_Forwarding

quectel-uart-ddp -help


## Send/Receive AT Commands Over Main UART

quectel-uart-ddp –uart /dev/ttyHS0 -smd /dev/smd8


## Send/Receive AT Commands Over Debug UART

quectel-uart-ddp –uart /dev/ttyHSL0 -smd /dev/smd8


## Output NMEA Data Over Main UART

quectel-uart-ddp –uart /dev/ttyHS0 -smd /dev/smd7

Then after sending AT+QGPS=1 to enable the GNSS function, you can output NMEA data through the 
main UART.



