# AVR programming
## Make: AVR Programming by Elliot Williams (MAKE). Copyright 2014 Elliot Williams, 978-1-4493-5578-4.
- Why using `C` language?
    - your code will be much faster (cycles and size)
    - make the code flexible
    - `C` is available for every CPU
    - `C` will work on every AVR
- Micro controller is a whole computer on a chip, but it is very little computer
    - CPU
    - Dynamic memory
    - Non-volatile memory
- Tool chain
    - life cycle of AVR programming : `write code in C` then `compile the code to machine language` then `transfer the code to the chip` using FTDI protocol, so we need a hardware between the AVR board and the PC
- What we need to begin
    - cross compiler : GNU `avr-gcc` >> for linux users `sudo apt-get install avrdude binutils-avr avr-libc gcc-avr`
    - hardware programmer
    - AVRDUDE : knows how to run many hardware programmers
    - a makefile to compile and flash in one step
    - usb-serial converter
- Hardware
    - AVR uses the SPI interface for In-system programming (ISP)
    - Wires need to hoock up
        - Power
        - Ground
        - SCK (serial clock)
        - MISO (Maser in Slave out)
        - MOSI (Master out slave in)
        - RESET (tell the AVR to enter programming mode)
        - ![isp](isp.png)
- Software
    - Arduino ISP example, flash it to arduino
    - `avrdude -p atmega168 -c avrisp -b 19200 -p /dev/ttyACM0 -nv`
    - if it runs it will give info about board, if not recheck connections
    - ![arduino](arduino.png)
    - make file
        - to setup the make file i have to define
            - target MCU
            - programmer
            - serial port and speed
        - make sure to open the make file in the same directory of the project
    - open up terminal
    - run `make flash` or `make program`
    - type `make` to make the hex file
    - you can use `avrdude -p atmega168 -c usbtiny -U blinkLED.hex` 0R `avrdude -p atmega168 -c avrisp -b 19200 -P /dev/ttyACM0 -U blinkLED.hex` depending on the programmer
        - `-p` chip type
        - `-c` programmer type
        - `-U` hexfile file to upload
    - it is better to personalize these values in your makefile and you can use it every time without type it again

    ```
    // where your include information from other files
    #include <avr/io.h>
    #include <util/delay.h>
    // here we can also use define function.
    // or define globale variables
    int main(void) // the C code must have one main, here                  //where the AVR starts executing your code
    {
        DDRB = 0b00000010;  // DDR, Data direction register sets pin one in PORTB (PB1) into output mode
                            // can be DDRB |= (1<<PB1); 
        while(1)            // called main loop
        {
            PORTB = 0b00000010;
            _delay_ms(1000);
            PORTB = 0b00000000;
            _delay_ms(1000);
        }
        return (0);
    }
    ```
- there is another method to do that
    ```
    #include<avr/io.h>
    #include<util/delay.h>

    #define led PB0
    #define led_port PORTB
    #define led-ddr DDRB
    #define bv(x) (1<<x)
    #define setbit(p,b) p|=bv(b)
    #define clearbit(p,b) p&=bv(b)
    #define togglebit(p,b) p^=bv(b)
    ...
    in the main function
    setbit(led-ddr,led)
    ...
    togglebit(led-port,led)
    ```
- <avr/io.h> is the file that defines all the PORTs and DDRs.
- <util/delay.h> provides us with the _delay_ms() function that we use to delay between blinks.
- #define statements 
    - improve code readability and portability by defining  constants or code fragments.
    - For instance, in a setup with only one LED, I’ll usually define LED as a synonym for a particular pin on the AVR (PB0) partly to remind myself how to hook up the circuit, but also partly to make it easy to change later.
    - For instance, if you were reproducing the blinkLED code, but you’d like to physically wire the LED to pin PB5, you could go through the code and change every occurrence of PB0 to PB5. 
    If instead, as here, you define the LED pin at the top of the code, something like #define LED PB0 and then consistently only use LED in the main body, you’ll only have to change PB0 to PB5 in the one place where it’s defined, right up at the top of your code or in a suitably named include file.
- Resgisters : fixed memory locations with side effects, can read and write like normal variables, each register byte is bits, each bit like a switch
    - DDRx data-direction registers (port x) :
        - These registers control whether each pin is configured for input or output the data direction.
        - After a reset or power-up, the default state is all zeros, corresponding to the pins being configured for input.
        - To enable a pin as output, you write a one to its slot in the DDR.
    - PORTx port x data registers :
        - When the DDRx bits are set to one (output) for a given pin, the PORT register controls whether that pin is set to logic high or low (i.e., the VCC voltage or ground).
        - Switching between these voltage levels could, for instance, turn on and off attached LEDs.
        - With the DDR configured for input, setting the PORT bits on a pin will control whether it has an internal pull-up resistor attached or whether it’s in a “hi-Z” (high-impedance) state, effectively electrically disconnected from the circuit, but still able to sense voltage.
    - PINx port x input pins address :
        - The PIN register addresses are where you read the digital voltage values for each pin that’s configured as input.
        - Each PINx memory location is hooked up to a comparator circuit that detects whether the external voltage on that pin is high or low.
        - You can’t write to them, so they’re not really memory, but you can read from the PINx registers like a normal variable in your code to see which pins have high and low voltages on them.
- bitwise operators :
    - `OR` bitwise : if i want to turn on `PB1` and `PB2` ledS i should consider the following :
        ```
        0b00000010 = (1<<PB1)
        0b01000000 = (1<<PB7)
        0b01000010 = (1<<PB1) | (1<<PB7)
        ```
        - For each bit position, a bitwise OR returns 1 if either bit in the comparison is 1. OR returns a 1 if this bit is 1 or that bit is 1. OR returns 0 only
        - when both bits are 0:
        ```
         1010
        |1100
        =1110
        ```

    - `XOR` bitwise : if i want to change the status of one led i should use this operator as follows :
        ```
        0b00001111
        ^0b00000010
        0b00001101
        ```
        - XOR (or “exclusive or”) returns 1 if only one of the two bits compared is a 1. If both bits are 1 or if both bits are 0, XOR returns 0:
        ``` 
         1010
        ^1100
        =0110
        ```

    - `AND` bitwise : if i want to clear a specific bit like :
        ```
        0b00001111
        &0b11111101
        0b00001101
        ```
        Bitwise AND compares two bits and returns 1 only if both of the bits are 1. If either of the bits are 0, AND returns 0:
        ```
         1010
        &1100
        =1000
        ```
    - `NOT` bitwise : also to clear bit :
        ```
        0b11111101=~(1<<PB1)
        ```
        - NOT takes all the bits and flips their logical sense —each 1 becomes a 0 and each 0 becomes a 1.
        - It’s also the only logical operator that takes only one input:
        ```
        ~1100
        =0011
        ```
    - so the approperiate way is :
        ```
        PORTB = PORTB & ~(1<<PB1)
        OR
        PORTB & = ~(1<<PB1)
        ```
    - to set bit :
        ```
        PORTB | = (1<<PB1)
        ```
    - to clear bit :
        ```
        PORTB & = ~(1<<PB1)
        ```
    - to toggle bit :
        ```
        PORTB ^ = (1<<PB1)
        ```
- MOSFET trickery
    - if you want to program an avr chip and there are loads connected to it, so we can use mosfet to control the conductivity of the ground terminal of the loads
    - the AVR uses its RESET pin to enter programming mode.
    - the RESET pin (PC6, blue wire from the programmer) is held at 5 V by the AVR when the chip is running, and pulled low to 0 V by the programmer to signal the AVR to enter programming mode.
- `PORTB = (1<<PB1) = (1<<1)`
- The _BV() Macro : 
    -The _BV() macro is just our bit-shift roll in disguise.
    - In fact, it’s even defined as: `#define _BV(bit) (1 << (bit))`
    - So should you use _BV(2) or (1 << 2)? Well, theyend up being exactly the same thing.
- different ways to toggle leds pattern `PORTB =(1<<i)` , `PORTB = ~(1<<i)` , `PORTB |= (1<<i)` , `PORTB &= ~(1<<i)`
- Setting Bits with OR
    - set an individual bit in a register, leaving all the other bits as they were.
    - `PORTB |= (1 << 2);`
- A bitmask :
    - is just a normal old byte, but we’re thinking of it as being made up of ones and zeros in particular places that we specify rather than representing a numerical value.
    - We use a bitmask, along with a bitwise logical operator, to change some bits in a target byte.
    - I like to think of bitmasks almost like stencils used for spray painting. You cut away parts of the stencil where you want to change (paint) the underlying surface, and you leave the stencil intact where you don’t want paint to go.
    - In particular, if we want to turn on some bits in PORTB while leaving the others untouched, we’ll create a bitmask with ones in the bit locations we’d like turned on. This works because a one ORed with anything will return a one. So we read in PORTB and OR it with the bitmask. The result should be the unaltered contents of PORTB everywhere that we had a zero, and ones everywhere our bitmask had a one.
    - If we write this back out to PORTB, we’re set—PORTB has all its old bits intact, except those where there was a 1 in the bitmask have been turned on.
- Toggling Bits with XOR
    - Now imagine that you want to flip a bit or two. You don’t really care if it’s on or off right now, you just want it in the other state, whatever that is.
    - `PORTB ^= (1 << 2);`
    - for short. You can, of course, toggle more than one bit at once with something like:
        - `PORTB ^= ((1 << 2) | (1 << 4));`
- Clearing a Bit with AND and NOT
    - `PORTB &= ~(1 <<2);`
        ```
         (1 << 2) -> 0b00000100
        ~(1 << 2) -> 0b11111011
        ```PORTB & = ~(1<<3);
- `uint8_t` : unsigned int 8 bits
- `uint16_t` : unsigned int 16 bits
- `uint8_t` : from 0 to 255 if the maximum value `255` is reached it will count from the begining `0` again





- i should check that site for [newly added stuff](http://littlehacks.org) 
- search for bruce land's cornell university engineering course