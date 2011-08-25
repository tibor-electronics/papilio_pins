# Papilio Pins

It is the intent of this project to help developers with the pin assignments on the Paplio boards offered by Gadget Factory.

## Diagrams

Currently, two diagrams have been defined. One for the Papilio One and one for a prototype board called the Papilio RAM. Note that the P/RAM board will most likely change names in the future. The diagrams are useful when creating a UCF (constraints) file for a Papilio HDL design.

The Papilios offer a collection of headers divided into wing slots. Each pin in a wing slot has a wing letter and a pin index. Each wing pin is connected to a pin on the board's FPGA. The diagrams show the mapping of each wing pin to its corresponding FPGA pin, making it easy to determine which FPGA pins to use in your constraints file.