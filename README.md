# UART Implementation in Verilog

This repository contains a simple implementation of a Universal Asynchronous Receiver/Transmitter (UART) written in Verilog HDL. It is designed to be easily integrated with FPGA projects and has been tested on the Xilinx Artix-7 FPGA using the Arty Development Board from Digilent.

## Overview

This UART implementation provides basic functionality for serial communication. It includes both transmitter and receiver modules and is suitable for educational purposes and as a peripheral in various FPGA projects. The design is tested with a 50MHz clock and can be adapted for higher speeds with proper pin buffering.

## Tools

- **[Icarus Verilog](http://iverilog.icarus.com/)**: Verilog simulation and synthesis tool.
- **[GTKWave](http://gtkwave.sourceforge.net/)**: Waveform viewer for simulation results.

To install the tools on Ubuntu, run:

```sh
$> sudo apt-get install iverilog gtkwave
```
## Simulation
To run the testbenches for the UART modules, use the provided Makefile:
```$> make rx tx
```
This command will compile and execute the testbenches for both the receiver (uart_rx) and transmitter (uart_tx) modules, and generate waveform files in the ./work/ directory for analysis.

Certainly! Here is the full README file in Markdown format:

```markdown
```
This command will compile and execute the testbenches for both the receiver (`uart_rx`) and transmitter (`uart_tx`) modules, and generate waveform files in the `./work/` directory for analysis.

## Implementation Details

The UART modules were synthesized using the Xilinx default synthesis strategy and the constraints file provided in the `./constraints` directory. The following resource utilization was reported on the Arty Development Board:

| Module   | Slice LUTs | Slice Registers | Slices | LUT as Logic | LUT FF Pairs |
|----------|------------|-----------------|--------|--------------|--------------|
| `uart_rx` | 51         | 47              | 26     | 51           | 29           |
| `uart_tx` | 35         | 31              | 18     | 35           | 21           |

## Modules

### `impl_top`

Top-level module for synthesizing a simple echo test with the UART components.

### `uart_rx`

UART Receiver Module:

```verilog
module uart_rx(
    input                   clk          , // System clock input.
    input                   resetn       , // Active-low asynchronous reset.
    input                   uart_rxd     , // UART receive data pin.
    input                   uart_rx_en   , // Receive enable signal.
    output                  uart_rx_break, // Indicates a BREAK condition.
    output                  uart_rx_valid, // Indicates valid data received.
    output [PAYLOAD_BITS:0] uart_rx_data   // Received data.
);

parameter   BIT_RATE = 9600;      // UART line bit rate.
parameter   CLK_HZ   = 100000000; // Clock frequency in hertz.
parameter   PAYLOAD_BITS    = 8;  // Number of data bits per UART packet.
parameter   STOP_BITS       = 1;  // Number of stop bits per UART packet.
```

### `uart_tx`

UART Transmitter Module:

```verilog
module uart_tx(
    input                     clk         , // System clock input.
    input                     resetn      , // Active-low asynchronous reset.
    output                    uart_txd    , // UART transmit data pin.
    output                    uart_tx_busy, // Indicates if the module is busy.
    input                     uart_tx_en  , // Enable signal to send data.
    input  [PAYLOAD_BITS-1:0] uart_tx_data  // Data to be transmitted.
);

parameter   BIT_RATE = 9600;      // UART line bit rate.
parameter   CLK_HZ   = 100000000; // Clock frequency in hertz.
parameter   PAYLOAD_BITS    = 8;  // Number of data bits per UART packet.
parameter   STOP_BITS       = 1;  // Number of stop bits per UART packet.
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For further questions or issues, please contact:

- **Project Lead**: [Your Name](mailto:yourname@example.com)
- **Project Repository**: [GitHub Repository](https://github.com/yourusername/uart-verilog)

Feel free to fork and contribute to this project!
```

Replace placeholders such as `[Your Name]` and `[GitHub Repository]` with your actual contact details and repository URL. This README provides a comprehensive overview of the project, tools, usage instructions, and module details.
```
