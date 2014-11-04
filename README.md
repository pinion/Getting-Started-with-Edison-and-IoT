Instruction for a new Intel Edison Board
=====
### all this information was collected using the kind help of the people at the @HWHackathon in Dublin #HackDublin ###
#### in specific: ####
[Alex T](alextgalileo.altervista.org) of Intel <br>
the wonderful people at [Emutex Labs](http://www.emutexlabs.com/project)<br>
[Sandeep Mistry](https://github.com/sandeepmistry) whom ever you are :) <br>
Clarke Kevin of Intel <br>
Stephen Houston of Intel<br>

<br>

First of all
-----
1. read the getting started page 
    + [Getting Started](https://communities.intel.com/docs/DOC-23147)
2. upgrade - flash using wired or wifi
    + [Mac Wired](https://communities.intel.com/docs/DOC-23193)
    + [Windows Wired](https://communities.intel.com/docs/DOC-23192)
    + [Linux Wired](https://communities.intel.com/docs/DOC-23200)
3. run `configure_edison --setup` - general setup
4. run `configure wifi` - if you need to set up wifi (step 3 should take care of that)


quick log fix
-----
removes the need for repartioning of rootfs
Logs can consume all rootfs space.

```
mkdir /home/var
cd /var
mv log /home/var
ln -s /home/var/log
```

add repositories for easier workflow
-----

#### add the following /etc/opkg/base-feeds.conf ####

src all     http://iotdk.intel.com/repos/1.1/iotdk/all<br>
src x86 http://iotdk.intel.com/repos/1.1/iotdk/x86<br>
src i586    http://iotdk.intel.com/repos/1.1/iotdk/i586<br>
src/gz all http://repo.opkg.net/edison/repo/all<br>
src/gz edison http://repo.opkg.net/edison/repo/edison<br>
src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32<br>
src mraa-upm http://iotdk.intel.com/repos/1.1/intelgalactic<br>

run `opkg update`

Install git
-----
run `opkg install git`

Install MRAA - hardware communication layer
-----
run `opkg install libmraa0`

Install libusb - for hid devices
-----
run `opkg install libusb-1.0-dev`

Configure Bluetooth
-----
run `opkg install bluez5-dev`

#### Start Bluetooth ####
```
rfkill unblock bluetooth
hciconfig hci0 up
```
use `bluetoothctl` and `hcitool` to send commands


#### node.js related ####
```
npm install -g ble-scanner
npm install -g async
npm install -g noble
npm install -g bleno
```


node-red
-----
#### _non of this is needed. it depends on the use_ ####
```
git clone https://github.com/node-red/node-red.git
cd node-red
npm install
```

`npm install -g mongodb js2xmlparser arduino-firmata fs.notify serialport feedparser redis`

#### additional nodes ####
```
clone the repository directly from GitHub into the nodes/ directory:
cd node-red/nodes/
git clone https://github.com/node-red/node-red-nodes.git
```

#### remove what you do not need! ####

node-blink1 blinkstick node-hid heatmiser node-hue-api hidstream mqlight stomp-client wake_on_lan msgpack-js node-dweetio komponist nma growl node-prowl pushbullet pusher pushover-notifications snapchat twilio simple-xmpp aws-sdk level sqlite3 pg mysql suncalc node-stringprep firmata serialport sensortag wemo noble

```
npm install node-blink1 blinkstick node-hid heatmiser node-hue-api hidstream mqlight stomp-client wake_on_lan msgpack-js node-dweetio komponist nma growl node-prowl pushbullet pusher pushover-notifications snapchat twilio simple-xmpp aws-sdk level sqlite3 pg mysql suncalc node-stringprep firmata serialport sensortag wemo noble
```


Mapping of GPIO in Yocto
-----
#### GPIO mapping ####
[Edison GPIO mapping to linux](http://www.emutexlabs.com/project/215-intel-edison-gpio-pin-multiplexing-guide)


Start Coding > Intel DevKit
-----

#### The Intel Development Kit for IoT (IoTDK) is a complete solution to create and test applications for Intel IoT platforms like the Intel® Galileo and Edison maker boards <http://xdk.intel.com/>####
<br>
```
systemctl enable xdk-daemon
systemctl restart xdk-daemon
```

Good to know:
-----
#### reconfigure edison ####
`configure_edison --setup`

#### unblock wifi / bluetooth ####
```
rfkill unblock wifi
rfkill unblock bluetooth
```
#### lists all available packages ####
`opkg list – list available package to be installed`

#### enable and start connman at boot:####
`systemctl enable connman && systemctl start connman`





