#############
About NFC Tag
#############

.. image:: ../_static/hardware/about_nfc/nfc-tag.png
   :align: center
   :scale: 51%
   :alt: NFC Tag

The **NFC Tag** operates as a **dual port memory**. You have the the NFC protocol from one side and the I²C bus interface from the other side.
It features a 1 kB EEPROM memory.
The chip does not have to be powered when being accessed from the NFC side.

.. note::

    NFC (or Near Field Communication) is a great technology for transferring data on a short distance (a couple of centimeters).
    This attribute makes this technology appealing for security key provisioning. Many smartphones are today equipped with the NFC technology.

+-------------------------------------------------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------+----------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| `E-Shop <https://shop.hardwario.com/nfc-tag/>`_       | `Schematic drawing <https://github.com/hardwario/bc-hardware/tree/master/out/bc-tag-nfc>`_       | `SDK Library <https://sdk.hardwario.com/group__bc__tag__nfc>`_ | `Header File <https://github.com/hardwario/bcf-sdk/blob/master/bcl/inc/bc_tag_nfc.h>`_ | `Source File <https://github.com/hardwario/bcf-sdk/blob/master/bcl/src/bc_tag_nfc.c>`_ |
+-------------------------------------------------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------+----------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+

----------------------------------------------------------------------------------------------

********
Features
********

- Integrated NFC tag NT3H2111 (NXP)
- Communication using I²C bus
- 1 kB EEPROM memory
- Optional interrupt output
- Optional energy harvesting output
- Operating current: 240 µA
- Operating voltage range: 1.7 V to 3.6 V
- Operating temperature range: -20 to 70 °C
- Mechanical dimensions: 16 x 16 mm

