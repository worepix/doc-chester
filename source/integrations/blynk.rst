##########################
Blynk - Mobile App Builder
##########################

`The Blynk <http://www.blynk.cc/>`_ is a mobile front end builder and signaling relay (MQTT). This let's you quicky create control and display for your IoT things.
Here we will guide you the process of putting together the hardware and connecting it to the cloud.
The cloud in turn gets interconnected with the project on your phone withing the Blynk app.
The local side of the project is hosted on the BigClown Raspian which has all the necessary components prepared for interconnection.
When everything will be finished then you would have an ability to turn on and off the relay, switch the LED strip on and off,
change the light intensity using slider and also you would be able to watch the temperature (and other values collected) acompanied by graphs.

*************************************
Blynk example projects with HARDWARIO
*************************************
!!!!!!!!!!!!!!!!!!!!!TODO!!!!!!!!!!!!!!!!!!!!

*********
Blynk app
*********

.. image:: ../_static/integrations/blynk/blynk-for-mobile-applications_blynk.png
   :align: center
   :scale: 51%
   :alt: Blynk App Example

***************
Setup Blynk app
***************

The very first step needed is to install and configure the application on your mobile device. In order to interconnect things you would have to create account.
The Blynk gives you two options either create account by email or use OAuth2 login of Facebook. Decide yourself which is better for you.

.. tip::

    If you do not want to share your email, which we would consider quite safe in this case, then just create a testing email account for this purpose.

Step 1: If you do not want to share your email, which I would consider quite safe in this case, then just create a testing email account for this purpose.
**********************************************************************************************************************************************************

Step 2: After starting the app you have to create account. No email confirmation is needed, it is up to you to be careful when filling in the email address, typos might lead to unrecoverable account. The email address is used for token distribution, thus pretty important.
********************************************************************************************************************************************************************************************************************************************************************************

.. tip::

    Blynk also offers the off-line version of the server called `Local blynk server <http://docs.blynk.cc/#blynk-server>`_
    with `Github sources <https://github.com/blynkkk/blynk-server>`_. The off-line here stands for no-Internet setup.

********************
Create Blynk project
********************

In order to create a UI for your application you have to first create a project.

- Choose the project name
- Choose **HARDWARIO** device
- Connection type is **WiFi**

**************
Node-RED setup
**************

In node red, install the Blynk package ``node-red-contrib-blynk-ws`` if you cannot see **Blynk** nodes.
Also follow one of the project tutorials above where installation and creating and connecting of nodes is explained.

**********************************
ZeRGBA to hex RGB values - Example
**********************************

Blynk color values needs to be transformed to proper hexadecimal RGB string. You can use **function** block in the **Node-RED** and paste the code below.
Remember to configure ZeRGBa to **MERGE mode** and the range of values has to be **set for all three channels to 0 - 255**

!!!!!!!!!!!!!!!!!!!TODO EXAMPLE!!!!!!!!!!!!!!!!!!!!!!!!!

.. code-block:: javascript
    :linenos:

    var node = "generic-node:3"
    msg.topic = "node/" + node + "/led-strip/-/color/set";

    var r = Number(msg.arrayOfValues[0]).toString(16);
    var g = Number(msg.arrayOfValues[1]).toString(16);
    var b = Number(msg.arrayOfValues[2]).toString(16);

    r = (r.length < 2) ? "0" + r : r;
    g = (g.length < 2) ? "0" + g : g;
    b = (b.length < 2) ? "0" + b : b;

    msg.payload = "\"#" + r + g + b + "\"";

    return msg;
