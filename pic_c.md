# PIC C

## ccs C compile

## Priphral

- [1. General Purpose I/O](#general-purpose-io)
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
- [1. General Purpose I/O](#general-purpose-io)

2. Input Capture
1. I2C
1. ADC
1. -->

# General Purpose I/O

## Relevant Functions:

These options let the user configure and use the I/O pins on the device. These functions
will affect the pins that are listed in the device header file.

### output_high(pin)

- Sets the given pin to high state.

### output_low(pin)

- Sets the given pin to the ground state.

### output_float(pin)

- Sets the specified pin to the input mode. This will allow the pin to float
  high to represent a high on an open collector type of connection.

### output_x(value)

- Outputs an entire byte to the port.

### output_bit(pin,value)

- Outputs the specified value (0,1) to the specified I/O pin.

### input(pin)

- The function returns the state of the indicated pin.

### input_state(pin)

- This function reads the level of a pin without changing the direction of
  the pin as INPUT() does.

### set_tris_x(value)

- Sets the value of the I/O port direction register. A '1' is an input and '0'
  is for output.

### input_change_x( )

- This function reads the levels of the pins on the port, and compares
  them to the last time they were read to see if there was a change, 1 if there was,
  0 if there was not.

### set_open_drain_x(value)

- This function sets the value of the I/O port Open-Drain register. A |
  makes the output open-drain and 0 makes the output push-pull.

### set_input_level_x(value)

- This function sets the value of the I/O port Input Level Register. A 1
  sets the input level to ST and 0 sets the input level to TTL.

### set_open_drain_x()

- Sets the value of the I/O port Open-Drain Control register. A '1' sets it
  as an open-drain output, and a '0' sets it as a digital output.

## Relevant Preprocessor:

### USE STANDARD_IO(port)

- This compiler will use this directive be default and it will
  automatically inserts code for the direction register whenever an I/O function like
  output_high() or input() is used.

### USE FAST_IO(port)

- This directive will configure the I/O port to use the fast method of
  performing I/O. The user will be responsible for setting the port direction register
  using the set_tris_x() function.

### USE FIXED_IO (port_outputs=;in,pin?)

- This directive set particular pins to be used an
  input or output, and the compiler will perform this setup every time this pin is
  used.

## Relevant Interrupts:

None

## Relevant Include Files:

None, all functions are built-in

## Relevant getenv() Parameters:

PIN:pb ----Returns a 1 if bit b on port p is on this part
