# Debugging

## Debugging cause of a stack overflow

Stack memory is an area of RAM which is defined in the linker descriptor file. During a function execution stack memory is used for storing temporary data such as
- Local variables
- function arguments
- return addresses

Stack overflow occurs when a function writes to a memory address that is out of bounds of stack memory.

Some of the causes of stack overflow are
- recursion
- large local buffer
> temp_buffer[1024]
- multi level nested function calls
- printfs

Debugging of a stack overflow
- Adding a break point on the reset/assert handler and checking for the call stack
- Checking map file for large buffers allocated near stack limit.
- For FreeRTOS use of StackHighWaterMark()


## Debugging cause of a watchdog timer reset

Watchdog timer is used to find if any function/task is stuck and can reset the system. The watchdog timer must be periodically pet so that it does not reset the system.

If the microcontroller has a reset register, it can be confirmed if the source of the reset was a watchdog timer.

Debugging watchdog timer reset
- Add logging message to see which tasks pet and which didn't pet the watchdog. 
- Adding a interrupt handler for watchdog which can capture the PC and LR. And this information can be saved in a noinit RAM section which can be read at reboot.

