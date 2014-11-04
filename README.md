# Instruction for a new Intel Edison Board #

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
------
removes the need for repartioning of rootfs
Logs can consume all rootfs space.

```
mkdir /home/var
cd /var
mv log /home/var
ln -s /home/var/log
```

add repositories for easier workflow
------

#### add the following /etc/opkg/base-feeds.conf ####

src all     http://iotdk.intel.com/repos/1.1/iotdk/all<br>
src x86 http://iotdk.intel.com/repos/1.1/iotdk/x86<br>
src i586    http://iotdk.intel.com/repos/1.1/iotdk/i586<br>
src/gz all http://repo.opkg.net/edison/repo/all<br>
src/gz edison http://repo.opkg.net/edison/repo/edison<br>
src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32<br>
src mraa-upm http://iotdk.intel.com/repos/1.1/intelgalactic<br>

run `opkg update`

git
-----
run `opkg install git`

MRAA - hardware communication layer
-----
run `opkg install libmraa0`


bluetooth
-----
run `opkg install bluez5-dev`

### start bluetooth ###
```
rfkill unblock bluetooth
hciconfig hci0 up
bluetoothctl and hcitool to send commands
```

node.js specific settings
-----
### bluetooth related ###
run `npm install -g ble-scanner`

#### ** this d00d is brilliant!  ####
[Sandeep Mistry Github page](https://github.com/sandeepmistry)

`npm install -g async` - required by noble.js<br>
`npm install -g noble`<br>
`npm install -g bleno`<br>

#### REST interface ####
`npm install -g restify`

node-red
----
```
git clone https://github.com/node-red/node-red.git<br>
cd node-red<br>
npm install –production<br>
```

### node-red setup ###

#### non of this is needed. it depends on the use ####
`npm install -g mongodb js2xmlparser arduino-firmata fs.notify serialport feedparser redis`

#### additional nodes ####
```
clone the repository directly from GitHub into the nodes/ directory:<br>
cd node-red/nodes/<br>
git clone https://github.com/node-red/node-red-nodes.git<br>
```

#### remove what you do not need! ####
```
npm install node-blink1 blinkstick node-hid heatmiser node-hue-api hidstream mqlight stomp-client wake_on_lan msgpack-js node-dweetio komponist nma growl node-prowl pushbullet pusher pushover-notifications snapchat twilio simple-xmpp aws-sdk level sqlite3 pg mysql suncalc node-stringprep firmata serialport sensortag wemo noble<br>
```


Mapping of GPIO in Yocto
------
#### GPIO mapping ####
[Edison GPIO mapping to linux](http://www.emutexlabs.com/project/215-intel-edison-gpio-pin-multiplexing-guide)


Start Bluetooth
-----
```
rfkill unblock bluetooth<br>
hciconfig hci0 up<br>
```

`bluetoothctl and hcitool to send commands`

#### Bluetooth with Node ####
```
npm install -g async - required by noble.js<br>
npm install noble - try: node advertisement-discovery.js<br>
npm install bleno - try: node test-ibeacon.js<br>
npm install sensortag – try: node test.js<br>
```


Start Coding > Intel DevKit
-----

#### The Intel Development Kit for IoT (IoTDK) is a complete solution to create and test applications for Intel IoT platforms like the Intel® Galileo and Edison maker boards – link (external)####
<br>
```
systemctl enable xdk-daemon<br>
systemctl restart xdk-daemon<br>
```

Good to know:
-----
#### reconfigure edison ####
`configure_edison --setup`

#### unblock wifi / bluetooth ####
```
rfkill unblock wifi<br>
rfkill unblock bluetooth<br>
```
#### lists all available packages ####
`opkg list – list available package to be installed`

#### enable and start connman at boot:####
`systemctl enable connman && systemctl start connman`





