# pico_9bitsUART_int
to change it to 8 bits or 9 bits just change line 54 from uart_rx.pio

set x, 8    [10]    ; Preload 9 bit counter, then delay until halfway through

set x, 7    [10]    ; Preload 8 bit counter, then delay until halfway through

set x, 9    [10]    ; Preload 10 bit counter, then delay until halfway through

you can also to set a timeout to reset RXpointer. This way we can remove some noisy and false packets
you just need to set a uint timeroutRX = 2; //2 mili seconds if any new byte arrives the pointer will be reseted
use:
    TOUT(timeroutRX,funcResetPIORXPointer());           //function will be find it at main.c
    
at timer-pnal.c in void alarm_irq(void)

then create funcResetPIORXPointer() at main.c or any other place. 

void funcResetPIORXPointer(void)
{
  pbuffer = buffer;
}
