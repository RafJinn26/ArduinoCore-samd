# MattairTech Arduino SAM M0+ Core

This documentation is currently under construction.

This is a fork from arduino/ArduinoCore-samd on GitHub. This will be used to maintain
Arduino support for SAM M0+ boards including the MattairTech MT-D21E and the MT-D11
(see https://www.mattairtech.com/). It adds support for new devices like the L21, C21, and
D11. It also adds new clock sources, like a high speed crystal or internal oscillator.

This core is intended to be installed using Boards Manager (see below). To update from a
previous version, click on MattairTech SAM M0+ Boards in Boards Manager, then click Update.

**Differences from Arduino in Versioning**
The MattairTech version number does not correspond to either the IDE version or to the
upstream ArduinoCore-samd version. See the CHANGELOG for details on which upstream
commits have been merged in to the MattairTech core.


## What's New Beta (1.6.8-beta). See Beta Builds section for installation instructions.

1.6.8-beta-b0:
* Added L21 and C21 support. Improved D11D and D11C support.
  * Use Tools->Microcontroller menu to select mcu.
* Both the core and bootloader have added support for:
  * external high-speed crystal (400KHz - 32MHz) using PLL
  * external 32.768KHz crystal using PLL
  * internal oscillator with USB calibration using DFLL
  * internal oscillator using DFLL in open-loop mode (or 48MHz RC oscillator with C21)
  * PLL_FRACTIONAL_ENABLED and PLL_FAST_STARTUP options
  * The clock source is selectable in the Tools->Clock Source menu
* New Tools->Serial Config menu for selecting different combinations of serial peripherals
* New Tools->Bootloader Size menu allows selection of bootloader size
* New Tools->USB Config menu simplifies USB configuration compared to previous core
* Updated variant.cpp table format for future CCL and GCLK use. See VARIANT_COMPLIANCE_CHANGELOG.
* Updated bootloader.
* Updated bossac upload tool (fixed support for SAML and SAMC)
* New CMSIS-Atmel package (this is different than from Arduino)
* Merged in all changes from upstream through SAMD CORE 1.6.14 (April 2017)


## What's New Release (1.6.6). NOTE: This is out of date, use the beta for now.

* 1.6.6-mt3:
  * Fixes compilation with CDC_UART and CDC_ONLY settings

* 1.6.6-mt2:
  * Changes the default Communication setting to CDC_UART (from CDC_HID_UART)

* 1.6.6-mt1:
  * New documentation section 'Special Notes'. Please read!
  * Updated ASCII pinouts to be more readable and less ambiguous.
  * Updated the Signed driver for Windows (extras directory) (see CHANGELOG for details)
  * Merged in changes from upstream (see CHANGELOG for details)
  * Fix warnings about deprecated recipe.ar.pattern
  * Merged in changes from upstream SAMD CORE 1.6.2 2015.11.03 (see CHANGELOG for details)


## Specifications

TODO: Update for L21 and C21

Feature                 |	MT-D21E										|	MT-D11
------------------------|---------------------------------------------------------------------------------------|------------------------------------------------------
Microcontroller		|	ATSAMD21ExxA, 32-Bit ARM Cortex M0+						|	ATSAMD11D14AM, 32-Bit ARM Cortex M0+
Clock Speed		|	48 MHz										|	48 MHz
Flash Memory		|	256 KB (D21E18A) / 128 KB (D21E17A) / 64 KB (D21E16A) / 32 KB (D21E15A)		|	16 KB (4KB used by USB SAM-BA bootloader)
SRAM			|	32 KB (D21E18A) / 16 KB (D21E17A) / 8 KB (D21E16A) / 4 KB (D21E15A)		|	4 KB
EEPROM			|	None (emulation may be available in the future)					|	None (emulation may be available in the future)
Digital Pins		|	22										|	17
Analog Input Pins	|	10, 12-bit ADC channels								|	10, 12-bit ADC channels
Analog Output Pins	|	1, 10-bit DAC									|	1, 10-bit DAC
PWM Output Pins		|	12										|	8
External Interrupts	|	15 (1 NMI)									|	9 (1 NMI)
USB			|	Device and Host (CDC and HID)							|	Device and Host (CDC and HID)
UART (Serial)		|	2										|	1
SPI			|	1										|	1
I2C (TWI)		|	1										|	1
Operating Voltage	|	3.3V (Do not connect voltages higher than 3.3V!)				|	3.3V (Do not connect voltages higher than 3.3V!)
DC Current per I/O Pin	|	7 mA										|	7 mA



## Board Variants

Pin configuration and peripheral assignment information is now in the README.md for each board variant.
README.md also now includes technical information on the new PinDescription table format.

* [MattairTech MT-D21E Rev B (SAMx21Exxx)](https://github.com/mattairtech/ArduinoCore-samd/tree/master/variants/MT_D21E_revB/README.md)

* [MattairTech MT-D21E Rev A (SAMD21ExxA)](https://github.com/mattairtech/ArduinoCore-samd/tree/master/variants/MT_D21E/README.md)

* [MattairTech MT-D11 (SAMD11D14AM)](https://github.com/mattairtech/ArduinoCore-samd/tree/master/variants/MT_D11/README.md)

* [MattairTech Generic D11C14A](https://github.com/mattairtech/ArduinoCore-samd/tree/master/variants/Generic_D11C14A/README.md)

* MattairTech x21J based board (coming June)

* MattairTech Generic D11D14AS (coming soon)

* MattairTech Generic D11D14AM (coming soon)

* MattairTech Generic x21E (coming soon)

* MattairTech Generic x21G (coming soon)

* MattairTech Generic x21J (coming soon)

* [Arduino Zero (arduino.cc)](https://github.com/mattairtech/ArduinoCore-samd/tree/master/variants/arduino_zero/README.md)

* [Arduino M0 (arduino.org)](https://github.com/mattairtech/ArduinoCore-samd/tree/master/variants/arduino_mzero/README.md)



## Tools Menu Additions

Depending on the board variant, different menu options will appear in the Tools menu. 


### Microcontroller Menu

This menu will appear with boards that have multiple microcontroller options.


### Clock Source Menu

There are up to four clock source choices, depending on board variant and microcontroller. They are:

* 32KHZ_CRYSTAL (default)
* HIGH_SPEED_CRYSTAL
* INTERNAL_OSCILLATOR
* INTERNAL_USB_CALIBRATED_OSCILLATOR

See Clock Source section for more information.


### Bootloader Size Menu

With the D21, L21, and C21, the bootloader size can be configured as:

* 8KB_BOOTLOADER (default)
* 16KB_BOOTLOADER
* NO_BOOTLOADER

With the D11, the bootloader size can be configured as:

* 4KB_BOOTLOADER (default)
* NO_BOOTLOADER

Choose NO_BOOTLOADER if not using a bootloader (an external programmer will be used for sketch upload).


### Serial Config Menu

This menu is used to select different combinations of serial peripherals. This is useful especially for
the D11, which has a reduced pin count and number of SERCOMs. It can also be used to reduce FLASH and
SRAM usage by selecting fewer UART peripherals, which are instantiated in the core, rather than only
when including a library (like SPI and WIRE). Most board variants support two UART as an option.


### USB Config Menu

This menu will appear with all microcontrollers except the C21, which does not have USB. The options are:

* CDC_ONLY (default)
* CDC_HID
* WITH_CDC
* HID_ONLY
* WITHOUT_CDC
* USB_DISABLED

Choose an option that best matches your code and library usage. Each option results in a different USB PID.
Choose an option with CDC if you want auto-reset to function, or the serial monitor over USB. If CDC is
not enabled, Serial will refer to Serial1 instead of SerialUSB. These options can be used to optimize FLASH
and SRAM usage by allowing CDC to be disabled (or USB completely disabled).


## Clock Source

TODO
There are up to four clock source choices, depending on board variant and microcontroller. They are:

* 32KHZ_CRYSTAL (default)
* HIGH_SPEED_CRYSTAL
* INTERNAL_OSCILLATOR
* INTERNAL_USB_CALIBRATED_OSCILLATOR

 * If CLOCKCONFIG_32768HZ_CRYSTAL or
 * CLOCKCONFIG_HS_CRYSTAL is defined, then the PLL will be used. If
 * CLOCKCONFIG_HS_CRYSTAL is defined, then HS_CRYSTAL_FREQUENCY_HERTZ must
 * also be defined with the crystal frequency in Hertz. CLOCKCONFIG_INTERNAL
 * uses the DFLL in open-loop mode, except with the C21 which lacks a DFLL, so
 * the internal 48MHz RC oscillator is used instead. CLOCKCONFIG_INTERNAL_USB
 * can be defined for the D21, D11, or L21. It will also use the DFLL in
 * open-loop mode, except when connected to a USB port with data lines (and
 * not suspended), where it will calibrate against the USB SOF signal.

/* If CLOCKCONFIG_HS_CRYSTAL is defined, then HS_CRYSTAL_FREQUENCY_HERTZ
 * must also be defined with the external crystal frequency in Hertz.
 */
#if ((HS_CRYSTAL_FREQUENCY_HERTZ < 400000UL) || (HS_CRYSTAL_FREQUENCY_HERTZ > 32000000UL))
#error "board.init.c: HS_CRYSTAL_FREQUENCY_HERTZ must be between 4000000UL and 32000000UL"
#endif

#if defined(PLL_FAST_STARTUP)
#if (HS_CRYSTAL_FREQUENCY_HERTZ < 1000000UL)
#error "board.init.c: HS_CRYSTAL_FREQUENCY_HERTZ must be at least 1000000UL when PLL_FAST_STARTUP is defined"
#else
#define HS_CRYSTAL_DIVISOR	1000000UL
#endif
#else
#define HS_CRYSTAL_DIVISOR	32000UL
#endif

#define HS_CRYSTAL_DIVIDER	(HS_CRYSTAL_FREQUENCY_HERTZ / HS_CRYSTAL_DIVISOR)
#define DPLLRATIO_FLOAT		(96000000.0 / ((float)HS_CRYSTAL_FREQUENCY_HERTZ / HS_CRYSTAL_DIVIDER))

#if defined(PLL_FRACTIONAL_ENABLED)
#define DPLLRATIO_LDR		(uint16_t)DPLLRATIO_FLOAT
#define DPLLRATIO_LDRFRAC	(uint8_t)((DPLLRATIO_FLOAT - (uint16_t)DPLLRATIO_FLOAT) * 16.0)
#else
#define DPLLRATIO_LDR		(uint16_t)DPLLRATIO_FLOAT
#define DPLLRATIO_LDRFRAC	0
#endif

Switch Generic Clock Generator 0 to PLL. Divide by two and the CPU will run at 48MHz.

// Constants for Clock generators
#define GENERIC_CLOCK_GENERATOR_MAIN      (0u)
#define GENERIC_CLOCK_GENERATOR_XOSC      (1u)
#define GENERIC_CLOCK_GENERATOR_OSCULP32K (2u) /* Initialized at reset for WDT (D21/D11) */
#define GENERIC_CLOCK_GENERATOR_OSC_HS    (3u)

/* If the PLL is used (CLOCKCONFIG_32768HZ_CRYSTAL, or CLOCKCONFIG_HS_CRYSTAL
 * defined), then PLL_FRACTIONAL_ENABLED can be defined, which will result in
 * a more accurate 48MHz output frequency at the expense of increased jitter.
 */

/* If both PLL_FAST_STARTUP and CLOCKCONFIG_HS_CRYSTAL are defined, the crystal
 * will be divided down to 1MHz - 2MHz, rather than 32KHz - 64KHz, before being
 * multiplied by the PLL. This will result in a faster lock time for the PLL,
 * however, it will also result in a less accurate PLL output frequency if the
 * crystal is not divisible (without remainder) by 1MHz. In this case, define
 * PLL_FRACTIONAL_ENABLED as well.
 */

/* The fine calibration value for DFLL open-loop mode is defined here.
 * The coarse calibration value is loaded from NVM OTP (factory calibration values).
 */
#define NVM_SW_CALIB_DFLL48M_FINE_VAL     (512)

* What to do with unused default internal RC oscillator:
#if (SAMD21)
/* Modify PRESCaler value of OSC8M to have 8MHz */
/* Put OSC8M as source for Generic Clock Generator 3 */
#elif (SAML21)
/* Note that after reset, the L21 starts with the OSC16M set to 4MHz, NOT the DFLL@48MHz as stated in some documentation. */
/* Modify FSEL value of OSC16M to have 8MHz */
/* Put OSC16M as source for Generic Clock Generator 3 */
#endif


### External High-Speed Crystal
TODO

### External 32.768KHz Crystal
TODO

### Internal Oscillator with USB Calibration
TODO

### Internal Oscillator
TODO



## Analog Reference

TODO: Analog reference selection

 * For values <= 5, the actual register value is used.
 * For values > 5 (SAML and SAMC only), the SUPC_VREF_SEL register value is: (ulMode - 6).
 * Values for the Supply Controller (SUPC) reference on the L21 or C21.
 * Used when AR_INTREF is selected as the reference.

typedef enum _eAnalogReference
{
#if (SAMD)
  AR_INTERNAL1V0 = 0,
  AR_INTERNAL_INTVCC0 = 1,
  AR_INTERNAL_INTVCC1 = 2,
  AR_EXTERNAL_REFA = 3,
  AR_EXTERNAL_REFB = 4,
  AR_DEFAULT = 5,	// On the SAMD, this also uses 1/2 gain on each input
#elif (SAML21)
  AR_INTREF = 0,
  AR_INTERNAL_INTVCC0 = 1,
  AR_INTERNAL_INTVCC1 = 2,
  AR_EXTERNAL_REFA = 3,
  AR_EXTERNAL_REFB = 4,
  AR_INTERNAL_INTVCC2 = 5,
  AR_INTREF_1V0 = 6,
  AR_INTREF_1V1 = 7,
  AR_INTREF_1V2 = 8,
  AR_INTREF_1V25 = 9,
  AR_INTREF_2V0 = 10,
  AR_INTREF_2V2 = 11,
  AR_INTREF_2V4 = 12,
  AR_INTREF_2V5 = 13,
  AR_DEFAULT = AR_INTERNAL_INTVCC2,
  AR_INTERNAL1V0 = AR_INTREF,		// Default INTREF for SAML is 1.0V
#elif (SAMC21)
  AR_INTREF = 0,
  AR_INTERNAL_INTVCC0 = 1,
  AR_INTERNAL_INTVCC1 = 2,
  AR_EXTERNAL_REFA = 3,
  AR_EXTERNAL_DAC = 4,
  AR_INTERNAL_INTVCC2 = 5,
  AR_INTREF_1V024 = 6,
  AR_INTREF_2V048 = 7,
  AR_INTREF_4V096 = 8,
  AR_DEFAULT = AR_INTERNAL_INTVCC2,
  AR_INTERNAL1V0 = AR_INTREF,		// Default INTREF for SAMC is 1.024V
#else
  #error "wiring_analog.c: Unsupported chip"
#endif
  AR_INTERNAL = AR_INTERNAL_INTVCC0,
  AR_INTERNAL2V23 = AR_INTERNAL_INTVCC0,	// 2.23V only when Vcc = 3.3V
  AR_INTERNAL1V65 = AR_INTERNAL_INTVCC1,	// 1.65V only when Vcc = 3.3V
  AR_EXTERNAL = AR_EXTERNAL_REFA,
} eAnalogReference ;



## Random TODO Notes

* TONE: TC5 does not exist on the D11. Using TC2 instead (TC1 on the D11C14 as TC2 is not routed to pins). It will conflict with the 2 associated TC analogWrite() pins.
* D21: Enables wakeup capability on pin in case being used during sleep (WAKEUP always enabled on SAML and SAMC)
* All pins (digital and analog) setup in STARTUP mode (enable INEN and set default pull direction to pullup (pullup will not be enabled))
* INEN enabled for both input and output (but not analog)
* pinPeripheral now handles disabling the DAC (if active). Note that on the L21, the DAC output would
  interfere with other peripherals if left enabled, even if the anaolog peripheral is not selected.
* Pull resistors enabled only if pin attributes allow and only if pin is not configured as output.
* Pull direction (pullup or pulldown) is now set with pinMode only (defaults to pullup if pinMode never called).



## Chip Specific Notes

### SAMD21

* When USB is disabled, pullups will be enabled on PA24 and PA24 to avoid excessive current consumption (<1mA) due to floating pins.
  Note that it is not necessary to enable pull resistors on any other pins that are floating.
  Errata: Disable pull resistors on PA24 and PA25 manually before switching to a peripheral.


### SAML21

* There are two DACs, DAC0 and DAC1. Both are supported. Because changing the configuration of one DAC requires disabling both,
  there will be about a 40us period when the second DAC is disabled. Most of this time is due to an errata that requires a delay of
  at least 30us when turning off the DAC while refresh is on. The L21 DACs have a refresh setting which must be enabled in this core.
* The analog reference has additional options on the L21 and C21. See Analog Reference below.
* On the L21, SERCOM5 is in a low power domain. The Fm+ and HS modes of I2C (wire) are not supported.
* The SAML and SAMC have double-buffered TCs, which are supported in the core.
* The CHANGE and RISING interrupt modes on pin A31 do not seem to work properly on the L21.
* The L21 has two performance levels that affect power consumption. During powerup, the L21 starts at the lowest performance level (PL0).
  The startup code changes to the highest performance level (PL2) in order to support 48MHz and USB (among other things).
* Two Flash Wait States are inserted for the L21 and C21 (the D21/D11 use one wait state).


### SAMC21

* There are two SAR ADCs. Both are supported. The PinDescription table determines the peripheral instance and pin mapping.
* The analog reference has additional options on the L21 and C21. See Analog Reference below.
* The SAML and SAMC have double-buffered TCs, which are supported in the core.
* Two Flash Wait States are inserted for the L21 and C21 (the D21/D11 use one wait state).
* The C21 requires internal pull resistors to be activated on floating pins to minimize power consumption (not needed on D21/D11 or L21).
* The C21 uses the minimum sampling time so that rail-to-rail and offset compensation works. Offset compensation adds 3 ADC clock cycles,
  so the total is 4 clock cycles. The D21, D11, and L21 use the maximum sampling time.


### SAMD11

* The D11D has three SERCOM. The D11C has two sercom (no sercom2).
* When USB is disabled, pullups will be enabled on PA24 and PA24 to avoid excessive current consumption (<1mA) due to floating pins.
  Note that it is not necessary to enable pull resistors on any other pins that are floating.
  Errata: Disable pull resistors on PA24 and PA25 manually before switching to a peripheral.

#### Reducing SRAM/FLASH Usage

TODO


### Differences Between MattairTech and Arduino Cores

* TODO
* Table summarizing which core files are modified and by how much
* Changes due to adding/changing features vs porting to new chip



## Serial Monitor

To print to the Serial Monitor over USB, use 'Serial'. Serial refers to SerialUSB (Serial1 and Serial2 are UARTs).
Unlike most Arduino boards (ie. Uno), SAM M0+ boards do not automatically reset when the serial monitor is opened.
To see what your sketch outputs to the serial monitor from the beginning, the sketch must wait for the SerialUSB
port to open first. Add the following to setup():

```
while (!Serial) ;
```

Remember that if the sketch needs to run without SerialUSB connected, another approach must be used.
You can also reset the board manually with the Reset button if you wish to restart your sketch. However, pressing
the Reset button will reset the SAM M0+ chip, which in turn will reset USB communication. This interruption means
that if the serial monitor is open, it will be necessary to close and re-open it to restart communication.

When USB CDC is not enabled, Serial will instead refer to Serial1, which is the first UART.


## Code Size and RAM Usage (1.6.5-mt2)

TODO: Update this. Maybe just for D11 and move to D11 Chip Specific Notes.

Sketch and Configuration    | MT-D21E (Flash + RAM) | MT-D11 (Flash + RAM)
----------------------------|-----------------------|-----------------------
Blink (CDC + HID + UART)    |     7564 + 1524       |     7452 + 1424
Blink (CDC + UART)          |     6588 + 1496       |     6484 + 1396
Blink (CDC Only)            |     5248 + 1304       |     5192 + 1300
Blink (UART Only)           |     3828 + 336        |     3716 + 236
Blink (No USB or UART)      |     2472 + 144        |     2416 + 140
Datalogger (No USB or UART) |     10340 + 948       |     10260 + 944

* 180 bytes of flash can be saved on the MT-D11 by using PIN_MAP_COMPACT (see 'New PinDescription Table' below).
* Datalogger compiled without USB or UART support, but with SPI and SD (with FAT filesystem) support. Serial output was disabled.
* Note that USB CDC is required for auto-reset into the bootloader to work (otherwise, manually press reset twice in quick succession).
* USB uses primarily 3 buffers totaling 1024 bytes. The UART uses a 96 byte buffer. The banzai() function (used for auto-reset) resides in RAM and uses 72 bytes.
* Any combination of CDC, HID, or UART can be used (or no combination), by using the Tools->Communication menu.


### Detailed Memory Usage Output After Compilation

The flash used message at the end of compilation is not correct. The number shown
represents the .text segment only. However, Flash usage = .text + .data segments
(RAM usage = .data + .bss segments). In this release, two programs are run at the
end of compilation to provide more detailed memory usage. To enable this output, go
to File->Preferences and beside "Show verbose output during:", check "compilation".

Just above the normal flash usage message, is the output from the size utility.
However, this output is also incorrect, as it shows .text+.data in the .text field,
but 0 in the .data field. However, the .text field does show the total flash used.
The .data field can be determined by subtracting the value from the normal flash
usage message (.text) from the value in the .text field (.text+.data). The .bss
field is correct.

Above the size utility output is the output from the nm utility. The values on the
left are in bytes. The letters stand for: T(t)=.text, D(d)=.data, B(b)=.bss, and
everything else (ie: W) resides in flash (in most cases).


## Installation

### Driver Installation

#### Windows

Prior to core version 1.6.6-mt1, sketches compiled with both CDC and HID USB code by default, thus requiring a CDC
driver for the bootloader and a CDC-HID driver for sketches. Now that PluggableUSB is supported, sketches compile
with only CDC code by default. Thus, only one driver is needed. Since HID and MIDI are currently supported (and
MSD potentially in the future), driver installation will be required for each different combination of USB devices.
There are currently four USB composite device combinations that include CDC as well as a CDC only device. Each
supported combination has a unique USB VID:PID pair, and these are listed in the .inf file. Once the first device
is installed (the CDC only device), future installations *might* be automatic, otherwise, you may direct the
installer to the same .inf file. The drivers are signed and support both 32 and 64 bit versions of Windows XP(SP3),
Vista, 7, 8, and 10. Note that the Windows 10 generic CDC drivers work as well.


1. If you do not already have the SAM-BA bootloader installed, see below.
2. Download https://www.mattairtech.com/software/MattairTech_CDC_Driver_Signed.zip and unzip into any folder.
   Note that the Windows 10 generic CDC drivers work as well.
3. Plug in the board. The LED should fade when the bootloader is running (or blink if the test sketch is running).
4. Windows will detect the board. Point the installer to the folder from above to install the bootloader driver.
5. If you don't intend on using Arduino, you can skip the rest of this list. See Using Bossac Standalone below.
6. If you do not already have the test firmware installed (comes preinstalled), see Using Bossac Standalone below.
7. Press the reset button to run the test firmware (if needed). The LED will blink.
8. Windows will detect the board. Point the installer to the above folder to install the sketch driver (if needed).
9. Continue with SAM M0+ Core Installation below.

#### Linux

0. No driver installation is needed.
1. On some distros, you may need to add your user to the same group as the port (ie: dialout) or set udev rules:
   * See the file https://github.com/mattairtech/ArduinoCore-samd/tree/master/drivers/99-mattairtech-USB-CDC.rules.
2. You MAY have to install and use Arduino as the root user in order to get reliable access to the serial port.
   * This is true even when group permissions are set correctly, and it may fail after previously working.
   * You can also create/modify a udev rule to set permissions on the port so *everyone* can read / write.
3. If you are running modemmanager (ie: Ubuntu), disable it, or use the udev rules file above.
4. Continue with SAM M0+ Core Installation below.

#### OS X

OS X support currently in beta (see below), the following instructions are only for 1.6.6-mtX and below.
1. Only the 256 KB chip variants work with the OS X version of the upload tool, bossac.
2. First, you will need to open boards.txt and change mattairtech_mt_d21e_bl8k.upload.tool to equal arduino:bossac.
3. Open platform.txt and change tools.bossac.path to equal{runtime.tools.bossac-1.6.1-arduino.path}.
4. No driver installation is needed.
5. Plug in the board. You may get a dialog box asking if you wish to open the “Network Preferences”:
   * Click the "Network Preferences..." button, then click "Apply".
   * The board will show up as “Not Configured”, but it will work fine.
5. Continue with SAM M0+ Core Installation below.


### SAM M0+ Core Installation

* To update from a previous version, click on MattairTech SAM M0+ Boards in Boards Manager, then click Update.

1. The MattairTech SAM M0+ Core requires Arduino 1.6.7 or above (including 1.8.x).
2. In the Arduino IDE, click File->Preferences.
3. Click the button next to Additional Boards Manager URLs.
4. Add https://www.mattairtech.com/software/arduino/package_MattairTech_index.json.
5. Save preferences, then open the Boards Manager.
6. Install the Arduino SAM M0+ Boards package. Use version 1.6.2 or higher.
7. Install the MattairTech SAM M0+ Boards package.
8. Close Boards Manager, then click Tools->Board->MattairTech MT-D21E (or MT-D11).
9. Select the MCU with the now visible Tools->Microcontroller menu (if present).
10. If you do not already have the bootloader or blink sketch installed, see SAM-BA USB CDC Bootloader below.
11. Plug in the board. The blink sketch should be running.
12. Click Tools->Port and choose the COM port. Note that the board indicated may not match the chosen board.
13. You can now upload your own sketch.


### Uploading the First Sketch

1. In the Arduino IDE (1.6.7 or above), open File->Examples->01.Basics->Blink.
2. Change the three instances of '13' to 'LED_BUILTIN'.
3. Be sure the correct options are selected in the Tools menu (see AVR Core Installation above).
4. With the board plugged in, select the correct port from Tools->Port.
5. Click the Upload button. After compiling, the sketch should be transferred to the board.
6. Once the bootloader exits, the blink sketch should be running.


## SAM-BA USB CDC Bootloader (Arduino compatible)

The SAM-BA bootloader has both a CDC USB interface, and a UART interface. It is compatible with the Arduino IDE, or
it can be used with the Bossac tool standalone. With Arduino, auto-reset is supported (automatically runs the
bootloader while the sketch is running) as well as automatic return from reset. The SAM-BA bootloader described
here adds to the Arduino version, which in turn is based on the bootloader from Atmel. The Arduino version added
several features, including three new commands (Arduino Extended Capabilities) that increase upload speed. The
bootloader normally requires 8 KB FLASH, however, a 4 KB version can be used for the D11 chips.

Bossac is a command line utility for uploading firmware to SAM-BA bootloaders. It runs on Windows. Linux, and OS X.
It is used by Arduino to upload firmware to SAM and SAM M0+ boards. The version Bossac described here adds to the
Arduino version (https://github.com/shumatech/BOSSA, Arduino branch), which in turn is a fork from the original
Bossa (http://www.shumatech.com/web/products/bossa). It adds support for more SAM M0+ chips (D21, L21, C21, and D11).

Note that only the Arduino or Mattairtech versions of bossac are currently supported for SAM M0+ chips.
Neither the stock bossac (or Bossa) nor the Atmel SAM-BA upload tool will work.

Arduino Extended Capabilities:

   * X: Erase the flash memory starting from ADDR to the end of flash.
   * Y: Write the content of a buffer in SRAM into flash memory.
   * Z: Calculate the CRC for a given area of memory.

The bootloader can be started by:

   * Tapping reset twice in quick succession (BOOT_DOUBLE_TAP).
   * Holding down button A (BOOT_LOAD_PIN) while powering up.
   * Clicking 'Upload Sketch' in the Arduino IDE, which will automatically start the bootloader (when CDC is enabled).
   * If the application (sketch) area is blank, the bootloader will run.

Otherwise, it jumps to application and starts execution from there. The LED will light during bootloader execution.
Note that the 4KB bootloader does not support the Arduino Extended Capabilities.
However, BOOT_DOUBLE_TAP does fit into the SAMD11 4KB bootloader.

When the Arduino IDE initiates the bootloader, the following procedure is used:

1. The IDE opens and closes the USB serial port at a baud rate of 1200bps. This triggers a “soft erase” procedure.
2. The first row of application section flash memory is erased by the MCU. If it is interrupted for any reason, the erase procedure will likely fail.
3. The board is reset. The bootloader (which always runs first) detects the blank flah row, so bootloader operation resumes.
4. Opening and closing the port at a baud rate other than 1200bps will not erase or reset the SAM M0+.

**See [bootloaders/zero/README.md](https://github.com/mattairtech/ArduinoCore-samd/tree/master/bootloaders/zero/README.md) for more technical information on the bootloader.**


### Bootloader Firmware Installation

#### Bootloader Installation Using the Arduino IDE

1. If you do not already have the MattairTech SAM M0+ core installed, see SAM M0+ Core Installation above.
2. Plug in the SAM M0+ board. The bootloader must be running to (press reset twice within 500ms).
3. Plug an Atmel ICE into USB, then connect it to the powered SAM M0+ board. A green LED should light on the Atmel ICE.
4. Click Tools->Programmer->Atmel ICE.
5. Click Tools->Board->MattairTech MT-D21E (or whichever board you are using).
6. Click Tools->Microcontroller and select your MCU (if menu present).
7. Click Tools->Burn Bootloader. Ignore any messages about not supporting shutdown or reset.
8. Continue with driver installation above.

A running sketch may interfere with the bootloader installation process. Be sure you are running the existing bootloader or using a blank chip.

#### Bootloader Installation Using Another Tool (ie: Atmel Studio, openocd)

1. Download the bootloader from https://www.mattairtech.com/software/arduino/SAM-BA-bootloaders-zero-mattairtech.zip.
2. Unzip to any directory. Be sure that a bootloader is available for your particular MCU.
3. Follow the procedures for your upload tool to upload the firmware.
   * Perform a chip erase first. Be sure no BOOTPROT bits are set.
   * Install the binary file to 0x00000000 of the FLASH.
   * You can optionally set the BOOTPROT bits to 8KB (or 4KB for the MT-D11). The Arduino installation method does not set these.
   * You can optionally set the EEPROM bits or anything else. The Arduino installation method uses factory defaults.
4. Continue with driver installation above.


### Bootloader Binaries

The bootloaders/zero/binaries directory contains all of the SAM-BAm0+
bootloaders built by the build_all_bootloaders.sh script.

#### MattairTech Boards
MattairTech boards are all configured with only one interface:
SAM_BA_USBCDC_ONLY (except C21, which uses SAM_BA_UART_ONLY).
CLOCKCONFIG_CLOCK_SOURCE is set to CLOCKCONFIG_INTERNAL_USB
(CLOCKCONFIG_INTERNAL for the C21). Only the main LED is defined.
BOOT_LOAD_PIN is not defined, but BOOT_DOUBLE_TAP_ENABLED is.

#### Arduino/Genuino Boards
Arduino/Genuino boards are all configured with both interfaces.
CLOCKCONFIG_CLOCK_SOURCE is set to CLOCKCONFIG_32768HZ_CRYSTAL.
All LEDs that are installed for each board are defined (and some
have LED_POLARITY_LOW_ON set). BOOT_LOAD_PIN is not defined, but
BOOT_DOUBLE_TAP_ENABLED is.

#### Generic Boards
The generic boards are all configured to minimize external hardware
requirements. Only one interface is enabled: SAM_BA_USBCDC_ONLY
(except C21, which uses SAM_BA_UART_ONLY). CLOCKCONFIG_CLOCK_SOURCE
is set to CLOCKCONFIG_INTERNAL_USB (CLOCKCONFIG_INTERNAL for the C21),
so no crystal is required. No LEDs are defined. BOOT_LOAD_PIN is not
defined, but BOOT_DOUBLE_TAP_ENABLED is, since it uses the reset pin.


### Using Bossac Standalone

TODO: Update https://www.mattairtech.com/software/SAM-BA-bootloader-test-firmware.zip with new chips (L21 and C21).

When using Bossac standalone, you will need to ensure that your application starts at 0x00002000 for 8 KB bootloaders,
and 0x00001000 for 4 KB bootloaders. This is because the bootloader resides at 0x00000000. This can be accomplished
by passing the following flag to the linker (typically LDFLAGS in your makefile; adjust for your bootloader size):

```
Wl,sectionstart=.text=0x2000
```

You can also use a linker script. See the MattairTech SAM M0+ package for examples.
Be sure to generate and use a binary file. Many makefiles are set up to generate an elf, hex, and bin already.

Download Bossac from:

* https://www.mattairtech.com/software/arduino/bossac-1.7.0-mattairtech-1-mingw32.tar.gz (Windows 32 bit and 64 bit)
* https://www.mattairtech.com/software/arduino/bossac-1.7.0-mattairtech-1-x86_64-linux-gnu.tar.gz (Linux 64 bit)
* https://www.mattairtech.com/software/arduino/bossac-1.7.0-mattairtech-1-i686-linux-gnu.tar.gz (Linux 32 bit)
* https://www.mattairtech.com/software/arduino/bossac-1.7.0-mattairtech-1-x86_64-apple-darwin.tar.gz (OS X 64 bit)

Linux 64 bit users can also download Bossa (GUI) and bossash (shell) from:

* https://www.mattairtech.com/software/arduino/Bossa-1.7.0-mattairtech-1-x86_64-linux-gnu.tar.gz (Linux 64 bit)

As an example, bossac will be used to upload the test firmware (blink sketch):

1. Download firmware from https://www.mattairtech.com/software/SAM-BA-bootloader-test-firmware.zip and unzip.
2. If you have not already installed the bootloader driver, see Driver Installation above.
3. Be sure there is a binary that matches your chip. On the command line (change the binary to match yours):

```
bossac.exe -d --port=COM5 -U true -i -e -w -v Blink_Demo_ATSAMD21E18A.bin -R
```
4. On Linux --port might be /dev/ttyACM0. If the device is not found, remove the --port argument for auto-detection.
5. See http://manpages.ubuntu.com/manpages/vivid/man1/bossac.1.html for details.
6. The board should reset automatically and the sketch should be running.



## New PinDescription Table

Technical information on the new PinDescription table format is now in the README.md
that accompanies each board variant. See board variants above.

### Note that a new column (GCLKCCL) was added for 1.6.8-beta-b0.
MATTAIRTECH_ARDUINO_SAMD_VARIANT_COMPLIANCE in variant.h is used to track versions.
If using board variant files with the old format, the new core will still read the
table the old way, losing any new features introduced by the new column. Additionally,
new definitions have been added for L21 and C21 support.

### Each pin can have multiple functions.
The PinDescription table describes how each of the pins can be used by the Arduino
core. Each pin can have multiple functions (ie: ADC input, digital output, PWM,
communications, etc.), and the PinDescription table configures which functions can
be used for each pin. This table is mainly accessed by the pinPeripheral function in
wiring_private.c, which is used to attach a pin to a particular peripheral function.
The communications drivers (ie: SPI, I2C, and UART), analogRead(), analogWrite(),
analogReference(), attachInterrupt(), and pinMode() all call pinPeripheral() to
verify that the pin can perform the function requested, and to configure the pin for
that function. Most of the contents of pinMode() are now in pinPeripheral().

### Pin Mapping
There are different ways that pins can be mapped. Typically, there is no relation
between the arduino pin number used, and the actual port pin designator. Thus, the 
pcb must be printed with the arduino numbering, otherwise, if the port pin is printed,
a cross reference table is needed to find the arduino pin number. However, this results
in the least amount of space used by the table. Another method, used by default by the
MT-D21E and MT-D11, maps Arduino pin numbers to the actual port pin number (ie: Arduino
pin 28 = Port A28). This works well when there is only one port (or if the PORTB pins
are used for onboard functions and not broken out). PIO_NOT_A_PIN entries must be added
for pins that are used for other purposes or for pins that do not exist (especially the
D11), so some FLASH space may be wasted. For an example of both types, see variant.cpp
from the MT-D11 variant.

### See Board Variants above for more technical information on the PinDescription table.

### See WVariant.h in cores/arduino for the definitions used in the table.



## Possible Future Additions/Changes

* Timer library is currently under development (like TimerOne, plus input capture, plus ??)
* OS X support currently in beta testing
* Reduce SRAM usage by USB endpoint buffers by only allocating endpoints actually used (D11 especially)

* USB Host mode CDC ACM (partially complete; BSD-like license?)
* Features for lower power consumption (library?)
* Reliability and security enhancements
* Enhanced SD card library
* Optional use of single on-board LED as USB activity LED
* MSC (Mass Storage) USB Device Class
* Polyphonic tone
* Wired-AND, Wired-OR for port pins
* High-speed port pin access (IOBUS)
* Libraries for some hardware I plan on using:
  * TFT LCD (CFAF128128B-0145T)
  * Motor controller
  * IR decoder
  * I2S DAC/AMP and I2S MEMS microphone
  * Battery management IC
  * XBee/Xbee Pro devices
  * RS485
  * Several I2C (Wire) sensor devices: 
    * Accelerometer/magnetometer (LSM303CTR)
    * Barometer/altimeter (LPS22HBTR)
    * Humidity/temperature
    * Light/color sensor


## ChangeLog

The Changelog has moved to a separate file named CHANGELOG. The most recent changes are still in the 'What's New' section above.


## Troubleshooting

TODO: Update

* **On Linux, disable modem manager**

* **Do not perform a manual auto-reset (using a terminal program to change baud to 1200)**

* **Boards Manager must be opened twice to see some updates**

* **Errors when compiling, uploading, or burning the bootloader**
* Be sure to install the Arduino samd core before installing the MattairTech sam m0+ core. If you have problems upgrading
the IDE to 1.6.6, you may need to uninstall both the Arduino and MattairTech cores, then re-install in the proper order.
Use Arduino core 1.6.2 or above.

* **Tools->Communications menu**
* Currently, the Tools->Communications menu must be used to select the communications configuration. This configuration
must match the included libraries. For example, when including the HID and Keyboard libraries, you must select an
option that includes HID (ie: CDC_HID_UART). This menu is currently needed to select the USB PID that matches the
USB device configuration (needed for Windows). This may become automatic in a future release.

* Be sure that the Tools->Communications menu matches the sketch and libraries you are compiling.
* Different combinations of USB devices will result in different COM port assingments in Windows.

* **Incude platform specific libraries**
* You may need to manually include platform specific libraries such as SPI.h, Wire.h, and HID.h.


## Bugs or Issues

If you find a bug you can submit an issue here on github:

https://github.com/mattairtech/ArduinoCore-samd/issues

Before posting a new issue, please check if the same problem has been already reported by someone else to avoid duplicates.


## Contributions

Contributions are always welcome. The preferred way to receive code cotribution is by submitting a Pull Request on github.


## Beta Builds

Periodically, a beta is released for testing.

The beta builds are available through Boards Manager. If you want to install them:
  1. Open the **Preferences** of the Arduino IDE.
  2. Add this URL `https://www.mattairtech.com/software/arduino/beta/package_MattairTech_index.json` in the **Additional Boards Manager URLs** field, and click OK.
  3. Open the **Boards Manager** (menu Tools->Board->Board Manager...)
  4. Install **MattairTech SAM M0+ Boards - Beta build**
  5. Select one of the boards under **MattairTech SAM M0+ Beta Build XX** in Tools->Board menu
  6. Compile/Upload as usual

The Arduino IDE will notify the user if an update to the beta is available, which can then be installed automatically.
Alternatively, if a particular beta is needed, replace the url in step 2 with:
  `https://www.mattairtech.com/software/arduino/beta/package_MattairTech_sam_m0p-${VERSION}-beta-b${BUILD_NUMBER}_index.json`
where ${VERSION} and ${BUILD_NUMBER} match the beta name as shown in the CHANGELOG (ie: package_MattairTech_sam_m0p-1.6.7-beta-b0_index.json).
In this case, the IDE will not notify the user of updates.


## License and Credits

This core has been developed by Arduino LLC in collaboration with Atmel.
This fork developed by Justin Mattair of MattairTech LLC.

```
  Copyright (c) 2015 Arduino LLC.  All right reserved.

  This library is free software; you can redistribute it and/or
  modify it under the terms of the GNU Lesser General Public
  License as published by the Free Software Foundation; either
  version 2.1 of the License, or (at your option) any later version.

  This library is distributed in the hope that it will be useful,
  but WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
  See the GNU Lesser General Public License for more details.

  You should have received a copy of the GNU Lesser General Public
  License along with this library; if not, write to the Free Software
  Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
```
