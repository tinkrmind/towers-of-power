# Towers of Power

My blog and code repo for [Towers of Power](https://github.com/saycel/towers-of-power) course at ITP, Spring 2018.

## Week 1

### Class notes

BTS: Base Transciever Station
BSC: Base Station COmputer


### Getting your IMSI and IMEI number

Each GSM/CDMA device has a IMEI(Internation Mobile Equipment Identity) associated with it. It's supposed to uniquely identify the device. Many apps([eg](http://www.imeichangerapk.com/)) claim to change the IMEI number of a rooted android phone. I'm not sure how well any of them work, and since changing IMEI number of a phone is illegal in the states, I don't intend to find out. The IMEI number is easily available under the phone settings> About phone> IMEI. Since I have a dual SIM phone, I have two IMEI numbers as well.

      AA80BB02CC30DD3
      AA80BB02CC30DD6


IMSI(International Mobile Subscriber Identity) number is stored in a SIM card and is used to identify the SIM. I couldn't find it on the phone and had to remove the SIM card to get at it. The numbers lasered on my SIM card are :

      AA01BB0CC M01.03 DD77EE93FF

IMSI numbers are supposed to be 14-15 digits long, so there's something fishy here. By consulting [wikipedia](https://en.wikipedia.org/wiki/International_mobile_subscriber_identity), I'm guessing the 03 in M01.03 is the [MCC(Mobile country code)](https://en.wikipedia.org/wiki/Mobile_country_code) corresponding to USA. Which would make DD77EE93FF my MSIN(mobile subscription identification number).

### Setting up OpenVPN

After following the [instructions](https://github.com/saycel/towers-of-power/tree/2018/openvpn), I was able to connect to the raspberry pi via VPN from home. To make sure the VPN always worked, I added a cron job to start openvpn every time the pi reboots.

      # Open cron tab
      $ sudo crontab -e

      # Add this to end of file
      @reboot sudo openvpn /etc/openvpn/client.conf

The pi is accessible from IP address 10.8.0.5. Of course, I also changed the password and added a firewall. I used my favorite UFW firewall, more or less the same way I [always do](https://github.com/tinkrmind/connectedDevices/blob/master/secureYourPi.md) but this time I added exception for port 1194, because openvpn uses it.

      sudo ufw allow 1194

## Week 2

### Possible homework:

Make a procedurally generated antenna to pick up weather satellite data and render satellite imagery.

*References:*

* RTL SDR NOAA data download [tutorial](https://www.rtl-sdr.com/rtl-sdr-tutorial-receiving-noaa-weather-satellite-images/)
* [Weather satellite data to image converter](http://www.wxtoimg.com/)
* And of course Dhruv Mehrotra's [Satellite Sounds](http://satellite-sounds.dhruvmehrotra.info/) project
* [Instructable](https://www.instructables.com/id/Downloading-NOAA-satellite-images-cheaply-and-easi/) on downloading NOAA data with RTL SDR
* [Quadrifilar helicoidal antenna design guide](https://www.jcoppens.com/ant/qfh/calc.en.php)
