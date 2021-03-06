# sonos-weblinks

This project consists of

1. an NMAP NSE script to scan a network for Sonos devices and
2. an XSL file to style the resulting XML output from the NSE script into a handy webpage with links to web interface items for each device.

The dynamic nature of the scan avoids the need to maintain a static list of links as you add devices or change IP addresses.

# pre-requisites

- A host with network access to the Sonos devices
- NMAP (https://nmap.org) installed and working on the host
- The files from this repository downloaded to the host
- A web server installed and working on the host
- Network access to the internet for Bootstrap and jQuery CDN downloads

# usage

Execute an NMAP scan with the following syntax:

<code>nmap -sC -p 1400 --script /path/to/sonos-weblinks/sonos-info.nse --open --stylesheet http://webserver.local/path/to/sonos-weblinks.xsl -oX /path/to/sonos-weblinks/sonos_nmap.xml 000.000.000.000/24</code>

Make sure to use the correct path fors your host/webserver and specify the relevant subnet to scan.

You may wish to use crontab to the schedule the NMAP scan to occur on a regular basis.

# results

The NMAP scan will create an XML file containing all Sonos devices found on the scanned network. For each Sonos Device the following data is included in the output:

- Model Name
- Model Number
- Model Description
- Hardware Version
- Zone Name
- Serial Number
- Software Version
- IP Address
- MAC Address
- Extra Info (from status page)
- Information about it's position in the STP hierarchy on your network

If you open this XML file in your browser it will use the XSL transform to render a web page containing useful information and links for managing and troubleshooting your Sonos devices. These links include:

- Status
- Support Info
- Device Description
- Reboot
- Tools
- WiFi Region
- Advanced Configuration
- WiFi Control (On/Off/Persist-Off)

Links to reference documents describing the use of these Sonos features are included in the rendered web page.
