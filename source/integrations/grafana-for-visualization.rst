#########################
Grafana for Visualization
#########################

`Grafana <https://grafana.com>`_ is an open platform for beautiful analytics and monitoring.
It allows you to create a nice looking dashboards that will give you quick insights into your sensor data.

.. image:: ../_static/integrations/grafana/grafana-for-visualization_grafana.png
   :alt: Grafana Visualization

************
Requirements
************
You will need these components to make it work:

- **Debian-based Linux**, or **macOS**
- **Mosquitto** - MQTT broker

.. caution::

    This setup has been tested on:

    - **Raspberry Pi 3** + **Raspbian Jessie**
    - **Turris Omnia** + **Ubuntu 16.04** (via LXC container)
    - **macOS 10.13**

****************************
Installing InfluxDB on Linux
****************************

Install dependency packages
***************************

.. code-block:: console

    sudo apt install apt-transport-https curl -y

Add repository key
******************

.. code-block:: console

    curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -

Add repository to source list
*****************************

.. tabs::

    .. tab:: Debian
        :title: Debian/Raspbian

        .. code-block:: console

            echo "deb https://repos.influxdata.com/debian stretch stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

    .. tab:: Ubuntu
        :title: Ubuntu

        .. code-block:: console

            echo "deb https://repos.influxdata.com/ubuntu/ xenial stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

Update the package list and install the packages
************************************************

.. code-block:: console

    sudo apt update && sudo apt install influxdb

Now you can start the InfluxDB service
**************************************

.. code-block:: console

    sudo systemctl start influxdb

***************************
Installing Grafana on Linux
***************************

Install dependencies
********************

.. code-block:: console

    sudo apt install adduser libfontconfig -y

Based on your target platform, select the appropriate procedure
***************************************************************

.. tabs::

    .. tab:: Rpi
        :title: Raspberry Pi and Omnia LXC

            **Step 1: You can manualy download latest version from `Grafana <https://github.com/fg2it/grafana-on-raspberry/releases/latest>`_, or you can use the following helper to download it for you**

            .. code-block:: console

                wget $(wget "https://api.github.com/repos/fg2it/grafana-on-raspberry/releases/latest" -q -O - | grep browser_download_url | grep armhf.deb | head -n 1 | cut -d '"' -f 4) -O grafana.deb

            **Step 2: Then install the package**

            .. code-block:: console

                sudo dpkg -i grafana.deb


    .. tab:: Desktop
        :title: Desktop (Ubuntu and Debian)

            **Step 1: Add repository key**

            .. code-block:: console

                curl -sL https://packages.grafana.com/gpg.key | sudo apt-key add -

            **Step 2: Add repository to source list**

            .. code-block:: console

                echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

            **Step 3: Then update the package list and install the package**

            .. code-block:: console

                sudo apt update && sudo apt install grafana -y

Reload the systemd configuration
********************************

.. code-block:: console

    sudo systemctl daemon-reload

Enable Grafana on boot
**********************

.. code-block:: console

    sudo systemctl enable grafana-server

Now you can start the Grafana server
************************************

.. code-block:: console

    sudo systemctl start grafana-server

Continue in the section :ref:`Connect Mosquitto and InfluxDB. <connect-mosquitto-influx>`

****************************
Installing InfluxDB on macOS
****************************

Open the Terminal application.
******************************

Make sure you have `Homebrew <https://brew.sh>`_ installed.
***********************************************************

Install InfluxDB
****************

.. code-block:: console

    brew install influxdb

Enable InfluxDB service
***********************

.. code-block:: console

    brew services start influxdb

***************************
Installing Grafana on macOS
***************************

Open the Terminal application.
******************************

Make sure you have `Homebrew <https://brew.sh>`_ installed.
***********************************************************

Install Grafana
***************

.. code-block:: console

    brew install grafana

Enable Grafana service
**********************

.. code-block:: console

    brew services start grafana

.. _connect-mosquitto-influx:

******************************
Connect Mosquitto and InfluxDB
******************************

Install the MQTT to InfluxDB service
************************************

.. code-block:: console

    sudo pip3 install --upgrade mqtt2influxdb

Create the ``/etc/hardwario`` directory
***************************************

.. code-block:: console

    sudo mkdir /etc/hardwario

Open the configuration file
***************************

.. tip::
    For text editing, we use nano editor. You can save changes by pressing key combination ``Ctrl + O`` and exit editor by pressing ``Ctrl + X``.

.. code-block:: console

    sudo nano /etc/hardwario/mqtt2influxdb.yml

Paste this snippet to the configuration file
********************************************

Configuration possibilities and structure are described at article about :ref:`mqtt2influxdb <configure-mqtt2influxdb>`.

.. code-block:: yaml

    /etc/hardwario/mqtt2influxdb.yml

    mqtt:
        host: 127.0.0.1
        port: 1883
    ​
    influxdb:
        host: 127.0.0.1
        port: 8086
        database: node
    ​
    points:
        - measurement: temperature
            topic: node/+/thermometer/+/temperature
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
                channel: $.topic[3]
        ​
        - measurement: relative-humidity
            topic: node/+/hygrometer/0:4/relative-humidity
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
        ​
        - measurement: illuminance
            topic: node/+/lux-meter/0:0/illuminance
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
        ​
        - measurement: pressure
            topic: node/+/barometer/0:0/pressure
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
        ​
        - measurement: co2
            topic: node/+/co2-meter/-/concentration
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
        ​
        - measurement: voltage
            topic: node/+/battery/+/voltage
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
        ​
        - measurement: button
            topic: node/+/push-button/+/event-count
            fields:
                value: $.payload
            tags:
                id: $.topic[1]
                channel: $.topic[3]

Configuration file test
***********************

.. code-block:: console

    mqtt2influxdb -c /etc/hardwario/mqtt2influxdb.yml --test

Start the MQTT to InfluxDB service
**********************************

.. code-block:: console

    pm2 start `which python3` --name "mqtt2influxdb" -- `which mqtt2influxdb` -c /etc/hardwario/mqtt2influxdb.yml

Save the PM2 state (so it will start after reboot)
**************************************************

.. code-block:: console

    pm2 save

.. tip::
    If you want to see temperature records from database in CSV format, use this command:

    .. code-block:: console

        influx -database node -execute "select * from temperature;" -format csv

    Then you must restart the service when you change the configuration file

    .. code-block:: console

        pm2 restart mqtt2influxdb

*****************
Configure Grafana
*****************

Open the Grafana web interface at http://localhost:3000/ or http://hub.local:3000/ or http://ip:3000/ and log in
****************************************************************************************************************

- Enter the **User** ``admin``
- Enter the **Password** ``admin``

Create a data source
********************

Select **Add data source** and then:

- Enter the **Name**: ``node``
- Select the **Type**: ``InfluxDB``
- Enter the **URL**: ``http://localhost:8086``
- Enter the **Database**: ``node``

Finish by clicking on the **Add** button. At this moment **Grafana** will try to connect to the **data source** and replies back with
the message **Data source is working.**

.. image:: ../_static/integrations/grafana/grafana-for-visualization_datasource.png
   :alt: Grafana Data Source Check

Download ``dashboard.json`` or copy the content of this file to clipboard
*************************************************************************

:download:`dashboard.json <../_static/integrations/grafana/doc/dashboard.json>`

Import the visualization dashboards, click the Grafana icon (top left button), select Dashboards in the menu, then choose Import
********************************************************************************************************************************

.. image:: ../_static/integrations/grafana/grafana-for-visualization_menu-import-dashboard.png
   :alt: Grafana Menu Import

Upload the ``dashboard.json`` file or paste the JSON from clipboard
*******************************************************************

Choose node as a data source and click on Import
************************************************

.. image:: ../_static/integrations/grafana/grafana-for-visualization_import-dashboard-select-datasource.png
   :alt: Grafana Select Datasource

Result for `Wireless Climate Monitor <https://www.hackster.io/jakub-smejkal/radio-climate-monitor-96de57>`__ and `Wireless CO2 Monitor <https://www.hackster.io/jakub-smejkal/radio-co2-monitor-311d2c>`_​_
*************************************************************************************************************************************************************************************************************

.. image:: ../_static/integrations/grafana/_integrations_grafana-for-visualization_demo-dashboard.png
   :alt: Grafana Test Results
