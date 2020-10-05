############
Amazon Alexa
############

In the end of Alexa integration you will be able to control your HARDWARIO projects using Alexa.
Result of this article will be controlling `LED strip <https://shop.hardwario.com/led-strip-rgbw-1m-144-leds/>`_.

**********
Installing
**********

You need to install plugin to Node-RED (functions).
Open HARDWARIO Playground on your computer.
If you want use your computer for this integration, just open **Functions** tab in the menu.
However, if you want to use `HARDWARIO Hub <https://shop.hardwario.com/raspberry-pi-4b-4gb-set/>`_, you have to see on main page available hubs like on
following screenshot just click on one and it will open in your browser.
**?????????????????????????????????????????????????????????????????**

Now you have to install plugin which will allow you to control HARDWARIO TOWER - Industrial IoT Kit with Alexa.
Click on Hamburger menu in top right corner > Manage palette > Install and search for ``node-red-contrib-alexa-home-skill``.
You should see alexa category with ``alexa home`` and ``alexa home response`` in nodes under the **alexa** category.

.. thumbnail:: ../_static/integrations/alexa/node_red_alexa_category.png
   :width: 60%
   :alt: Alexa Nodes


We will be using service `Node-RED Alexa Home Skill Bridge <https://alexa-node-red.bm.hardill.me.uk>`_ where you have to register an account.

So now you have installed plugin on your Computer or Hub and registred account.
However it is not all. Open `Alexa app <https://www.amazon.com/gp/help/customer/display.html?nodeId=201602060>`_ on your
smartphone or use browser on your computer on `desktop app <https://www.amazon.com/ap/signin?showRmrMe=1&openid.return_to=https%3A%2F%2Falexa.amazon.com%2F&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.assoc_handle=amzn_dp_project_dee&openid.mode=checkid_setup&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0&>`_.
Navigate to Skills and install `Node-RED skill <https://www.amazon.com/dp/B01N0D97FZ/?ref-suffix=ss_copy>`_. After installing you have to Sign in using account that you have created.

*****************
Setting up device
*****************

Login in on Node-RED Alexa Home Skill Bridge and click on devices. Click add device and fill it with following parameters. Name it by yourself.


.. thumbnail:: ../_static/integrations/alexa/alexa_screen-4.PNG
   :width: 60%
   :alt: Alexa Screen

Then click Ok. Go to Alexa app or desktop app and click on Smart Home > Devices > Discover and you should see your device you've just added.

.. thumbnail:: ../_static/integrations/alexa/alexa_screen-5.PNG
   :width: 60%
   :alt: Alexa Screen

Now place an ``alexa home`` node to flow and double-click on it. You should see setting page.
Click on little pencil next to the account and login in with account you've just created in Installing part.

.. thumbnail:: ../_static/integrations/alexa/alexa_screen-3.PNG
   :width: 40%
   :alt: Alexa Screen

If you click on refresh icon, you would be able to choose devices you added on Node-RED Alexa Home Skill Bridge website and click Done.

Hardware
********

As I said in the beginning. We will be controlling HARDWARIO LED strip.
Prepare MicroUSB cable, Core Module and Power Module with DC source.
Now connect Core Module to the computer via MicroUSB cable and open HARDWARIO Playground on your computer.
In Playground navigate to the **Firmware** tab and you should be able to see connected device.
Choose hardwario/bcf-radio-power-controller and version depends on your LED strip.
I bought **rgbw144** and click **Flash firmware**.

.. thumbnail:: ../_static/integrations/alexa/playground_flash_firmware.PNG
   :width: 60%
   :alt: Flash Firmware

Now open your **Devices** tab (on HARDWARIO Hub if you want to have Alexa there) and Click start pairing.
Assembly hardware like in following video, plug it in to electricity and plug in LED strip.

??????????VIDEO SOMEHOW???????????

You should see connected device in device section on Hub or your computer. Do not forget to click **Stop pairing!**

.. thumbnail:: ../_static/integrations/alexa/playground_devices_paired_device.png
   :width: 60%
   :alt: Devices Tab

Now click **Functions** tab and you should see ``alexa home`` node from previous section.

.. thumbnail:: ../_static/integrations/alexa/playground_functions_alexa_home.png
   :width: 60%
   :alt: Functions Tab

Now click hamburger menu in top right corner > Import > Clipboard and copy following code there:

.. code-block:: json

    [{"id":"70cb2802.0f4e08","type":"switch","z":"3abb2073.f7b74","name":"color switch","property":"payload.hue","propertyType":"msg","rules":[{"t":"eq","v":"0x0","vt":"str"},{"t":"eq","v":"0x78","vt":"str"},{"t":"eq","v":"0xf0","vt":"str"}],"checkall":"true","repair":false,"outputs":3,"x":450,"y":260,"wires":[["1c18841e.37453c"],["e925ec80.33ace"],["53fd3cc4.1f87a4"]]},{"id":"1c18841e.37453c","type":"change","z":"3abb2073.f7b74","name":"red","rules":[{"t":"set","p":"payload","pt":"msg","to":"\"#ff0000\"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":650,"y":160,"wires":[["ccaf0313.3f267"]]},{"id":"ccaf0313.3f267","type":"mqtt out","z":"3abb2073.f7b74","name":"","topic":"node/power-controller:0/led-strip/-/color/set","qos":"","retain":"","broker":"29fba84a.b2af58","x":1190,"y":200,"wires":[]},{"id":"e925ec80.33ace","type":"change","z":"3abb2073.f7b74","name":"green","rules":[{"t":"set","p":"payload","pt":"msg","to":"\"#008000\"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":650,"y":220,"wires":[["ccaf0313.3f267"]]},{"id":"6beeac02.679194","type":"switch","z":"3abb2073.f7b74","name":"off switch","property":"payload","propertyType":"msg","rules":[{"t":"false"}],"checkall":"true","repair":false,"outputs":1,"x":440,"y":340,"wires":[["d0dbd430.16a4d8"]]},{"id":"d0dbd430.16a4d8","type":"change","z":"3abb2073.f7b74","name":"off","rules":[{"t":"set","p":"payload","pt":"msg","to":"\"#000000(00)\"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":650,"y":340,"wires":[["ccaf0313.3f267"]]},{"id":"53fd3cc4.1f87a4","type":"change","z":"3abb2073.f7b74","name":"blue","rules":[{"t":"set","p":"payload","pt":"msg","to":"\"#0000ff\"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":650,"y":280,"wires":[["ccaf0313.3f267"]]},{"id":"29fba84a.b2af58","type":"mqtt-broker","z":"","broker":"127.0.0.1","port":"1883","clientid":"","usetls":false,"compatmode":true,"keepalive":"60","cleansession":true,"birthTopic":"","birthQos":"0","birthPayload":"","willTopic":"","willQos":"0","willPayload":""}]

.. thumbnail:: ../_static/integrations/alexa/playground_functions_imported_flow.PNG
   :width: 60%
   :alt: Functions Tab

Connected with your node to functions you imported and deploy.
You have to wait 5 seconds until alexa plugin connects to servers and than say "Alexa, turn [your device] to red". That's it!
