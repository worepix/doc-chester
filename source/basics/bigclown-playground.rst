####################
HARDWARIO Playground
####################

HARDWARIO Playground is free **Windows, macOS** and **Linux** software that enables you to:

- **Flash firmware** to Core Module
- **Manage wireless network** with Radio Dongle and nodes
- **Create programs** with visual programming in the **Node-RED**
- **Visualize** measured values and control nodes with Dashboard

.. image:: ../_static/basics/playground/playground_node-red.PNG
   :align: center
   :scale: 80%
   :alt: Playground Functions Tab

*****************************
Download HARDWARIO Playground
*****************************

Use `HARDWARIO Playground download page <https://www.hardwario.com/download/>`_ which always have the links of the latest version.

.. image:: ../_static/basics/playground/download_page.png
   :align: center
   :scale: 80%
   :alt: Playground Functions Tab

Builds are also in `github releases <https://github.com/hardwario/bch-playground/releases>`_.

***************
Video tutorials
***************

If you like video tutorials, you can watch quick guide to the HARDWARIO Playground in 5 videos.
They explain flashing, pairing, Dashboard and Node-RED

..  youtube:: https://www.youtube.com/watch?v=nzFtmhLNy-I&list=PLfRfhTxkuiVw0s9UQ8x5irref-EBwOghF&index=1

Devices
*******

On this tab you connect to the Radio Dongle. Choose the Radio Dongle (``bc-usb-dongle``) from the list and click Connect


.. image:: ../_static/basics/playground/playground_devices-connect.png
   :align: center
   :scale: 90%
   :alt: Playground Device

After connecting to the Radio Dongle you could see all the paired wireless nodes.
The node alias is later used in MQTT message topic (``node/climate-monitor:0/..``),
**so change it only when you know what are you doing.**

.. image:: ../_static/basics/playground/playground_devices-paired.png
   :align: center
   :scale: 90%
   :alt: Playground Paired Devices

.. _pairing-new-devices:

**Pairing new modules:**

#. Disconnect power from the wireless node (remove batteries or Battery Module, disconnect the USB cable, remove DC jack from Power Module)
#. Click on the **Start pairing** button
#. Apply power to the wireless module
#. Repeat with all the modules you want to pair

.. youtube:: https://www.youtube.com/watch?v=ESrTEdV9PJQ&list=PLfRfhTxkuiVw0s9UQ8x5irref-EBwOghF&index=3

Functions
*********

This tab is the `Node-RED <https://nodered.org/about/>`_ visual programming tool. See :doc:`Projects <projects>` how to use this visual programming tool.

.. image:: ../_static/basics/playground/playground_node-red_flow.png
   :align: center
   :scale: 80%
   :alt: Playground Functions Flow

.. youtube:: https://www.youtube.com/watch?v=VW_-RCIZ9rY&list=PLfRfhTxkuiVw0s9UQ8x5irref-EBwOghF&index=4

*********
Dashboard
*********

Here you can display gauges, graphs, buttons and other widgets. See the !!!!!!!Projects!!!!!!!!!!!!! how to use Dashboard.

.. image:: ../_static/basics/playground/playground_dashboard.png
   :align: center
   :scale: 80%
   :alt: Playground Dashboard

********
Messages
********

Here you can see all the messages from wireless nodes. You can copy the topics to clipboard and use them in Node-RED in the ``topic`` textbox.

.. image:: ../_static/basics/playground/playground_messages.png
   :align: center
   :scale: 90%
   :alt: Playground Messages

Firmware
********

This tab allows you to flash pre-compiled firmware for all HARDWARIO projects from out GitHub.
List of firmware is downloaded automatically.
Choose the firmware or start typing to find project you like to try. You can also flash binary or HEX file from your computer.

Always make sure you are flashing the right Device, usually ``bc-core-module``.
If you would like to update Radio Dongle, disconnect it first in the Devices tab.

.. youtube:: https://www.youtube.com/watch?v=3IXLBQ5M6Us&list=PLfRfhTxkuiVw0s9UQ8x5irref-EBwOghF&index=2

.. image:: ../_static/basics/playground/playground_firmware.PNG
   :align: center
   :scale: 80%
   :alt: Playground Firmware

***************
Troubleshooting
***************

Cannot find the Radio Dongle or Core Module in the device list

- On Windows 7 and macOS please install the `FTDI VCP drivers <https://www.ftdichip.com/Drivers/VCP.htm>`_
- On Ubuntu you need to be in ``dialout`` user group. Please use command ``sudo usermod -a -G dialout $USER`` and restart computer
- HARDWARIO Playground cannot flash older Core Module Revision 1. Please use the ``bcf`` tool. :doc:`See version comparison <../hardware/core-module-r1-and-r2-comparison>`
