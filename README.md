# shadow detect firmware OTA updates

## two files: 

* version.txt (contains the current version number)
* firmware.bin (contains the compiled firmware for the version)

# scans currently implemented:

* subnet size calcualtor - takes the gateway ip and subnet mask, calculates beginning and end ip addresses of network
* arp_scan - sends out an arp query for every ip address in the network, gathers mac addresses (used in all other scans from then on)
* ssdp_scan - probes for ssdp services
* ssdp_tv_scan - probes for ssdp dial services
* ssdp_location - on finding location info on ssdp or ssdp_tv scans, fetches the location info and parses
* DHCP listener - listens for, and records dhcp packets
* MDNs / Bonjour services scan - searches the network for specific bonjour / mdns services
    * http
    * workstation
    * smb
    * ftp
    * ipp
    * printer
    * amzn-alexa
    * amzn-wplay
    * spotify-connect
    * pdl-datastream
    * googlecast
    * googlezone
    * nintendoswitch
    * matter
    * visiocast
    * afpovertcp
    * airport
    * appletv
    * appletv-pair
    * airplay
    * companion-link
    * tivo-remote
    * device-info
    * dns-sd
    * dns-update
    * domain
    * honeywell-vid
    * sip
    * apple-mobdev2
    * mediaremotetv
    * companion-link
    * raop
    * sleep-proxy
    * homekit
    * touch-able
    * dns-sd
    * matterrc
* NBNS scan - queries and collects the NetBios machine names from the network
* SMB version scan - queries the available SMB versions
* SMB NATIVEOS scan - queries the native_os version on smb services
* SMB GSS-API build number scan
* iphone_scan - checks all devices returned by arp_scan for open port 62078
* sip_scan - checks all devices returned by arp_scan for open ports 5060 and 5061
* port_scan - checks all devices returned by arp_scan for open ports
    * 9, 21, 22, 23, 25, 53, 67, 68, 80, 88, 110, 135, 137, 138, 139, 143, 153, 161, 162, - 220, 443, 445, 587, 8080, 993, 995, 1080, 1194, 1900, 3306, 5060, 5061 62078
* hostname scan [dns over mdns]
* icmp scanner
* Wifi AP Scan [unused]
* mdns_broadcast - [unused] listens for mdns broadcast packets, extrracts PTR and TXT information, periodically uploads to cloud
* ssdp_broadcast - [unused] listens for ssdp broadcast packets, periodically uploads to cloud
____________________________

# changelog

* v270 - dhcp modify MAC_AND_IP_ADDRESSES map
* v267 - potential bugfix for confirmed bonjour dupes
* v266 - potential bugfix for confirmed bonjour dupes
* v265 - bugfix for potential bonjour dupes
* v264 - bugfix for potential smb dupes
* v263 - bugfix for ssdplocation dupes
* v262 - bugfix for nbns + potential hostname dupes
* v261 - bugfix for nbns dupes
* v260 - reinstate popup thing and menu for AP mode
* v257 - dont wipe device if wedont get a token back from a timeout
* v256 - some telemetry information - ping, rssi, etc
* v255 - icmp scanner
* v254 - reboot if STA_DISCONNECTED / wifi onStatusChange callback
* v253 - nulled pointers + clearing arp cache each loop
* v252 - "ATLANTIC" - new implementation of arp scanner, without nested while loops - experiment
* v251 - mutexes in new arp implementation
* v250 - different arp implementation (ICMP Ping and lookup mac in cache)
* v246 - mutex for thread-safe arp array
* v245 - windows build number change / experiment
* v244 - reinstate 100ms delay in arp scanner to avoid dupes
* v243 - ssdp_location individual uploads, overview wouth count to investigate
* v242 - separate ssdp_location upload for logging on serverside, trimming down onboarding
* v241 - DHCP scan
* v240 - move to global maps and mutexes - getting too many issues with async read/write
* v236 - bugfix - when finding the mac_str with no entry - added a function.
* v235 - experiment - arp scan remove 0.0.0.0 alternative way
* v234 - experiment - reinstate some older changes to arp scan
* v233 - experiment - reinstate some older changes to arp scan
* v232 - reinstate 100ms delay in arp scan
* v231 - rewrite all to use refs not pointers. separate ssdp_data from ssdp_location, refactor
* v230 - test for ssdp upload after > 5 items
* v229 - test for ssdp get_content - return just the location url
* v228 - test for ssdp get_content - hardcoded string return to narrow it down
* v227 - test for ssdp get_content - dont return nullptr
* v226 - restart if upload connection fails (covers wifi being dropped and other scenarios)
* v225 - ssdp location back off
* v224 - ssdp location back on
* v223 - using .empty() instead of comparing to .end()
* v222 - experiment, removing other characters from ssdp datas before fetching with get_content
* v221 - fixing hostname scan
* v220 - experiment, disable get_content
* v219 - experiment, "0" when no location, instead of nullptr
* v218 - rewrite all scans to use std::string in almost all places
* v217 - experiment, no break in for condition nbns scan
* v216 - experiment, x.replace()
* v215 - experiment, get_content on
* v214 - experiment, get_content
* v212 - experiment, no get_content
* v211 - dont have multiple ssdp scans per loop
* v210 - Upgrade to arduinoJson7 / SW_VER sent in every request
* v202 - SSDP scan memory increase and rewrite
* v201 - comment out SIP scan for testing
* v200 - separating architecture for the various boards and modifying update procedure
* v127 - fixing crashes, adding support for board with built-in LED
* v126 - separate ssdp + ssdp TV scans again as its not picking up as much with the combined scan
* v125 - increase buffer for login token as causeing crashes in boxes
* v124 - dont return on upload error, reset box / clear doc on upload fail
* v123 - dont send blank hostnames
* v122 - ARP scan fix issues
* v121 - HOSTNAME scan [dns query over mdns]
* v120 - SSDP location scan fix issues
* v119 - dont upload location response if its zeros
* v118 - dont upload smb scan if empty - alternative
* v117 - dont upload smb scan if empty
* v116 - fixing a panic()
* v115 - memory optimisations
* v114 - check if its possible to match wifimanager and app themes ( partially - we can add custom css and get a close-enough match)
* v112 - small bugfix on ssdp upload / overflow if too many scans
* v111 - move to platformio and separate code
* v110 - mac address in every scan
* v109 - SMB2 GSS-API Build number scan!
* v108 - bug fixes against 105 / upload ssdp individually
* v107 - bug fixes against 105 / upload ssdp individually
* v106 - bug fixes against 105 / upload ssdp individually
* v105 - NBNS, ssdp, ssdp location data clearing before uploads
* v104 - SMB version, SMB NativeOS, NBNS fixes
* v103 - SMB version scan, SMB NativePS scan, NBNS scan fixes
* v102 - sip scan
* v101 - always send up gateway_ip address with the scans
* v100 - dynamic company_name in scan_upload function
* v99 - small internal http server to get ip address for requesting machine (for web navgator agent os_version determination)
* v98 - change how SSDP scans are packaged
* v97 - change how SSDP scans are uploaded to fix bug
* v96 - minor bugfixes against v92
* v95 - minor bugfixes against v92
* v94 - minor bugfixes against v92
* v93 - minor bugfixes against v92
* v92 - Bonjour Services Scan rewrite - queries and collects the bnojour / mDNS machine names from the network; MDNS PTR and TXT scan - extracts info - from mDNS responses on network via library 
* v91 - NBNS scan - queries and collects the NetBios machine names from the network; MDNS PTR and TXT scan - extracts info from mDNS responses on network
* v90 - dont downlaod the location file form ssdp services multiple times
* v89 - changing format of portscan data array[port => state] and "ssdp/mdns broadcast/ssdp broadcast" ip, mac + location from an array in an array to - key=>value json objects 
* v88 - turning ssdp locations and broadcasts back into individual uploads
* v87 - bundling ssdp locations and broadcasts into single uploads
* v86 - lots of incremental changes and tweaks
* v85 - separate ssdp broadcast, mdns broadcast ssdp scans
* v84 - separate ssdp broadcast, mdns broadcast ssdp scans
* v83 - separate ssdp broadcast, mdns broadcast ssdp scans
* v82 - ssdp scan tweaking
* v81 - calculate_subnet, ssdp scan tweaking
* v80 - rewrite of ssdp json formating to use maps
* v79 - rewrite of ssdp json formating to use maps
* v78 - rewrite of ssdp json formating to use maps
* v77 - rewrite of ssdp json formating to use maps
* v76 - rewrite of ssdp json formating to use maps
* v75 - rewrite of ssdp json formating to use maps
* v74 - rewrite of ssdp json formating to use maps
* 
* v73 - testing out ota via github
* v72 - testing out ota via github
* v71 - last roger build, first repo commits around here
* ... roger builds
* v1 initial build (w/ roger)
