CPL ADC Board
===============

The CPL ADC Board is an AD7732 based fully differential two-channel, 15.075 kHz, 24-bit, +/-10V analog to digital converter.

[The ADC PCB board design](https://oshpark.com/shared_projects/mnPGlqKT).

Its digital interface is composed of an 8-bit wide data bus and a clock line. The data is clocked out asynchronously with a maximum rate of 1MHz. Once programmed, at runtime one can select which channels are active as well as the sampling frequency. One can also select at runtime how many of the 8 data bus bits are used for transferring data ot the host (the minimum is 2 bits) if the host doesn't have enough free lines. At the largest sampling rates with both channels enabled, the chip buffers 0.14 seconds of data. In addition to the ADC data, additional error information is sent along with every data points. A synchronization signal is sent every few data points to ensure the host stays synchronized with the board. Finally, as defined in the protocol, each bit is sent twice - the second time being the one's complement of the bit to reduce errors.

The CPL ADC Board is composed from an AD7732 ADC and an interfacing microcontroller – an AVR ATmega1284P. The AD7732 functions as the analog to digital converter while the microcontroller serves as the controller, buffer, and interface. The analog inputs are 3.5mm phone connectors, with the sleeve as the negative input and the tip as positive input. If the pin is not connected and the port is empty, both input on the ADC get shorted to ground. On the digital side, all pins have internal pull ups enabled (20-50 kOhms) when the board is not initialized.

See [CPL ADC](https://github.com/matham/CPL_ADC) for the microcontroller firmware.

Brief specifications
--------------------

* **Clock input**: Asynchronous, 1MHz maximum frequency.
* **Secondary input**: pin 7 of the data bus is also used as a clock and input during initialization (see protocol).
* **Data bus**: 2-8 output pins, clocked by clock pin from host asynchronously. The pins start counting down from pin 7 (see protocol).
* **Automatic reset**: 2 sec duration after initialization.
* **Port pull-up**: 20-50 kOhms.
* **Reset pin pull-up**: 20-60 kOhms.
* **Tclk,min**: the minimum pulse width.
