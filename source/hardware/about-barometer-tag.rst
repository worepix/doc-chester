###################
About Barometer Tag
###################

.. |pic1| thumbnail:: ../_static/hardware/about_barometer/barometer-tag.png
    :width: 300em
    :height: 300em

+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
| |pic1|                 | | The **Barometer Tag** allows you to measure absolute pressure in the range from 20 kPa to 110 kPa, or altitude above the sea level in meters. |
|                        | | It uses a low-power I²C sensor **MPL3115A2** with an absolute accuracy of ±0.4 kPa. It features a very low active and standby current.        |
|                        | |                                                                                                                                               |
|                        | | Monitoring of absolute pressure is useful for weather forecast and it is also an important                                                    |
|                        | | parameter in biometeorology because the absolute pressure can affect our health.                                                              |
+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
| |shopping-cart| `E-Shop <https://shop.hardwario.com/barometer-tag/>`_ | |microchip| `Schematic drawing <https://github.com/hardwario/bc-hardware/tree/master/out/bc-tag-barometer>`_ | |folder-open| `SDK Library <https://sdk.hardwario.com/group__bc__tag__barometer>`_ | |code| `Header File <https://github.com/hardwario/bcf-sdk/blob/master/bcl/inc/bc_tag_barometer.h>`_ | |code| `Source File <https://github.com/hardwario/bcf-sdk/blob/master/bcl/src/bc_tag_barometer.c>`_ |
+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+

----------------------------------------------------------------------------------------------

********
Features
********

- Absolute pressure sensor MPL3115A2 (NXP)
- The sensor only needs I²C bus
- Pressure range: from 20 kPa to 110 kPa
- Altitude range: from -698 to 11,775 m
- Absolute accuracy: ±0.4 kPa
- Optional interrupt output
- Power consumption:
    - 40 µA average current (1 Hz sample rate)
    - 2 µA standby current
- Operating voltage range: 2.0 V to 3.6 V
- Operating temperature range: -40 to 85 °C
- Mechanical dimensions: 16 x 16 mm
