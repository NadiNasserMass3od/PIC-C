# PIC C

## ccs C compile

## Priphral

- [1. General Purpose I/O](#general-purpose-io)
- [2. Interrupts](#interrupts)
<!-- - [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)
- [1. General Purpose I/O](#general-purpose-io)

2. Input Capture
1. I2C
1. ADC
1. -->

# General Purpose I/O

These options let the user configure and use the I/O pins on the device. These functions will affect the pins that are listed in the device header file.

## Relevant Functions:

### output_high(pin)

- Sets the given pin to high state.

### output_low(pin)

- Sets the given pin to the ground state.

### output_float(pin)

- Sets the specified pin to the input mode. This will allow the pin to float high to represent a high on an open collector type of connection.

### output_x(value)

- Outputs an entire byte to the port.

### output_bit(pin,value)

- Outputs the specified value (0,1) to the specified I/O pin.

### input(pin)

- The function returns the state of the indicated pin.

### input_state(pin)

- This function reads the level of a pin without changing the direction of the pin as INPUT() does.

### set_tris_x(value)

- Sets the value of the I/O port direction register. A '1' is an input and '0' is for output.

### input_change_x( )

- This function reads the levels of the pins on the port, and compares them to the last time they were read to see if there was a change, 1 if there was, 0 if there was not.

### set_open_drain_x(value)

- This function sets the value of the I/O port Open-Drain register. A | makes the output open-drain and 0 makes the output push-pull.

### set_input_level_x(value)

- This function sets the value of the I/O port Input Level Register. A 1 sets the input level to ST and 0 sets the input level to TTL.

### [PCD] set_open_drain_x()

- Sets the value of the I/O port Open-Drain Control register. A '1' sets it as an open-drain output, and a '0' sets it as a digital output.

## Relevant Preprocessor:

### #USE STANDARD_IO(port)

- This compiler will use this directive be default and it will automatically inserts code for the direction register whenever an I/O function like output_high() or input() is used.

### #USE FAST_IO(port)

- This directive will configure the I/O port to use the fast method of performing I/O. The user will be responsible for setting the port direction register using the set_tris_x() function.

### #USE FIXED_IO (port_outputs=;in,pin?)

- This directive set particular pins to be used an input or output, and the compiler will perform this setup every time this pin is used.

## Relevant Interrupts:

None

## Relevant Include Files:

None, all functions are built-in

## Relevant getenv() Parameters:

PIN:pb ----Returns a 1 if bit b on port p is on this part

## Example Code:

```c
void main(){
    Int8 Tris_value= 0x0F;
    int1 Pin_value;
    set_tris_b(Tris_value); //Sets B0:B3 as input and B4:B7 as output
    output_high(PIN_B7); //Set the pin B7 to High
    If(input(PIN_B0)){ //Read the value on pin B0, set B7 to low if
        output_high(PIN_B7);  //pin B0 is high
    }
}
```

# Interrupts

The following functions allow for the control of the interrupt subsystem of the microcontroller. With these functions, interrupts can be enabled, disabled, and cleared. With the preprocessor directives, a default function can be called for any interrupt that does not have an associated ISR, and a global function can replace the compiler generated interrupt dispatcher.

## Relevant Functions:

### disable_interrupts()

- Disables the specified interrupt.

### enable_interrupts()

- Enables the specified interrupt.

### ext_int_edge()

- Enables the edge on which the edge interrupt should trigger. This can be either rising or falling edge.

### clear_interrupt()

- This function will clear the specified interrupt flag. This can be used if a global isr is used, or to prevent an interrupt from being serviced.

### interrupt_active()

- This function checks the interrupt flag of specified interrupt and returns true if flag is set.

### interrupt_enabled()

- This function checks the interrupt enable flag of the specified interrupt and returns TRUE if set.

## Relevant Preprocessor:

### #DEVICE HIGH_INTS=

- This directive tells the compiler to generate code for high priority interrupts.

### #INT_XXX fast

- This directive tells the compiler that the specified interrupt should be treated as a high priority interrupt.

### [PCD] #INT_XXX level=x

- x is an int 0-7, that selects the interrupt priority level for that interrupt.

### [PCD] #INT_XXX fast

- This directive makes use of shadow registers for fast register save. This directive can only be used in one ISR

## Relevant Interrupts:

### #int_default

- This directive specifies that the following function should be called if an interrupt is triggered but no routine is associated with that interrupt.

### #int_global

- This directive specifies that the following function should be called whenever an interrupt is triggered. This function will replace the compiler generated interrupt dispatcher.

### #int_xxx

- This directive specifies that the following function should be called whenever the xxx interrupt is triggered. If the compiler generated interrupt dispatcher is used, the compiler will take care of clearing the interrupt flag bits. Functional Overview

## Relevant Include Files:

None, all functions are built-in

## Relevant getenv() Parameters:

None

## Example Code:

```c
#define LED PIN_A0
#define INT PIN_B0
#INT_EXT                                // This must be before the isr function
void ext_isr(void) {                    // This isr function for External Interrupt
  output_toggle(LED);
}
void main() {
  ext_int_edge(INT_EXT, H_TO_L);        // This for set External Interrupt edge
  clear_interrupt(INT_EXT);             // This for clear Interrupt flage         
  enable_interrupts(INT_EXT);           // This for enable External Interrupt
  enable_interrupts(GLOBAL);            // This for enable Global Interrupt
  while (TRUE);
}
```
