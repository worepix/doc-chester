####################
About Battery Module
####################

.. image:: ../_static/hardware/about_battery/battery-module.png
   :align: center
   :scale: 51%
   :alt: Battery Module

The **Battery Module** is designed as a power supply source for the battery-operated units.
The integrated low-power buck converter provides an excellent efficiency from the **four AAA 1.5 V Alkaline cells**.
It also features an extra 5-pin socket where you can connect a HARDWARIO tag.

The load disconnect circuit can disconnect the batteries if any other power supply source is connected to the system (e.g. AC adapter or USB cable).
The **battery voltage can be measured** on one of the analog inputs of the standardized header (P0/A0/TXD0).

If the for AAA batteries are not suitable for your application, you can use the **external voltage input**, which can handle up to 10 V.
You can find the external input on the two pins in the middle. These pins are compatible with the popular JST connector used for Lithium batteries.

Another useful feature is a **prototyping area** for soldering your circuits.

+--------------------------------------------------------+---------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| `E-Shop <https://shop.hardwario.com/battery-module/>`_ | `Schematic drawing <https://github.com/hardwario/bc-hardware/tree/master/out/bc-module-battery>`_ | `SDK Library <https://sdk.hardwario.com/group__bc__module__battery>`_ | `Header File <https://github.com/hardwario/bcf-sdk/blob/master/bcl/inc/bc_module_battery.h>`_ | `Source File <https://github.com/hardwario/bcf-sdk/blob/master/bcl/src/bc_module_battery.c>`_ |
+--------------------------------------------------------+---------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+

----------------------------------------------------------------------------------------------

********
Features
********

- High-efficiency buck converter TPS62745 (TI)
- Ultra-low quiescent current: 400 nA
- Recommended battery types:
    - 4x AAA 1.5 V Alkaline or
    - 4x AAA Eneloop NiMH
- Output supply voltage: 3.1 V
- Battery disconnect circuit
- Battery voltage measurement using an ADC input
- Prototyping area for soldering custom circuits
- One extra position for HARDWARIO tag
- Operating voltage range: 3.3 to 10 V
- Operating temperature range: -20 to 70 °C
- Mechanical dimensions: 88 x 55 mm

