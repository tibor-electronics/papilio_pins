# Papilio Pins

It is the intent of this project to help developers with the pin assignments on the Paplio boards offered by Gadget Factory.

## Diagrams

Currently, two diagrams have been defined. One for the Papilio One and one for a prototype board called the Papilio RAM. Note that the P/RAM board will most likely change names in the future. The diagrams are useful when creating a UCF (constraints) file for a Papilio HDL design.

The Papilios offer a collection of headers divided into wing slots. Each pin in a wing slot has a wing letter and a pin index. Each wing pin is connected to a pin on the board's FPGA. The diagrams show the mapping of each wing pin to its corresponding FPGA pin, making it easy to determine which FPGA pins to use in your constraints file.

## Conversion Tool

When creating an HDL design, eventually you may want to relocate your wing pin assignment. For instance, you may be moving your design to another type of board or to another location on the same board. The pin_converter project provides a tool to help with this.

### Requirements

The pin_converter tool is a command-line Java application. This means you need to have Java installed on your machine and in your command-line path.

### Running

I'll add some bat and shell scripts at some point, but in the meantime, you'll need to use something like the following from the command-line

    java -jar pin_converter.jar --sourceType "p1" --destinationType "pram" P1.ucf > PRAM.ucf

In this example, this is saying that the source file to process is using pin assignments for a Papilio One, the output should use pin assignments for a Papilio RAM, the source file is P1.ucf and the output should be piped to PRAM.ucf.

### Examples

Show a list of switches with brief descriptions. Most switches have short and long versions. The usage information will show all versions of a switch

    java -jar pin_converter.jar

The following examples assume that you have a shell script named pinconv that wraps the above call and passes along the command-line arguments.

Move all Papilio One Wings (A, B, and C) to Papilio RAM (2 variations)

    pinconv --sourceBoard "Papilio One" --destinationBoard "Papilio RAM" P1.ucf > PRAM.ucf
    pinconv --sourceBoard p1 --destinationBoard pram --inputFile P1.ucf --outputFile PRAM.ucf --transform

Move Papilio One A wing to Papilio RAM D wing

    pinconv --sourceBoard p1 --destinationBoard pram --move "A->D" P1.ucf > PRAM.ucf

Move Papilio One A wing its B wing

    pinconv --sourceBoard p1 --move "A->B" P1.ucf > P1-2.ucf

Move Papilio One's AH wing slot to its AL wing slot

    pinconv --sourceBoard p1 --move "AH->AL" P1.ucf > P1-2.ucf

Move Papilio One's AH wing slot to its AL wing slot and move BL to BH

    pinconv --sourceBoard p1 --move "AH->AL,BL->BH" P1.ucf > P1-2.ucf

Reverse the Papilio One's A wing

    pinconv --sourceBoard p1 --move "A[15:0]->A[0:15]" P1.ucf > P1-2.ucf

Generate generic Papilio One UCF file

    pinconv --destinationBoard "Papilio One" --generate

Generate generic Papilio One UCF file, limiting which headers are emitted

    pinconv --destinationBoard "Papilio One" --generate CLK,A,BL

Generate Papilio One UCF file, placing B/LED wing

    pinconv --destinationBoard "Papilio One" --placeWing "B/LED->A" --generate CLK,A

Generate Papilio One UCF file, placing multiple B/LED wings

    pinconv --destinationBoard "Papilio One" --placeWing "B/LED->AL,AH" --generate CLK,A,B

Generate Papilio One UCF file, placing B/LED and PS/2 wings (2 variations)

    pinconv --destinationBoard "Papilio One" --placeWing "B/LED->A;PS/2->BH" --generate CLK,A,BH
    pinconv -dst "Papilio One" -pw "B/LED->A" -pw PS/2->BH -gn CLK,A,BH
