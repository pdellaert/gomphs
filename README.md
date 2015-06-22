# gomphs

Simple tool to ping multiple hosts at once with a CLI and web-based overview.

## Download
[Binaries] (https://github.com/42wim/gomphs/releases)

## Usage 
Needs to be run as root (raw sockets for icmp)  
When using hostnames with ipv4 and ipv6 addresses, preference goes to ipv4. (-expand option shows both)

```
# gomphs
Usage of ./gomphs:
  -expand=false: use all available ip's (ipv4/ipv6) of a hostname (multiple A, AAAA)
  -hosts="": ip addresses/hosts to ping, space seperated (e.g "8.8.8.8 8.8.4.4 google.com 2a00:1450:400c:c07::66")
  -nocolor=false: disable color output
  -port="8887": port the webserver listens on
  -showrtt=false: show roundtrip time in ms
  -web=false: enable webserver
```

##### no options
```
. host is up
! host is down
```

##### showrtt
Add -showrtt on commandline   

When rtt > 1s it will just show ">1s"  
When rtt < 0ms it will just show 0  

After 25 pings the header will be repeated

##### expand 
Add -expand on commandline  

When using expand this also prints an extra (onetime) header so you know what ip addresses belong to what number.
See examples.

##### webserver
Add -web on commandline  

The web GUI is by default available via http://<server-running-gomphs>:8887/stream  
Use -port to use another port.

When an IP address/host isn't reachable, this will drop to -10 on the Y-axis. 

## Examples

##### using web, expand and showrtt
```
# gomphs -hosts="facebook.com slashdot.org www.linkedin.com" -showrtt -expand -web
```
 ![stream](http://i.snag.gy/Ow7kK.jpg)

##### using expand
Facebook resolves into 2 addresses (ipv4/ipv6), see 5 and 6 in example.  
When using expand this also prints an extra (onetime) header so you know what ip addresses belong to what number

[![asciicast](https://asciinema.org/a/4hh0lgl8j23ibycubz60vko3r.png)](https://asciinema.org/a/4hh0lgl8j23ibycubz60vko3r)

## Building
Install Go using your package manager or from the website https://golang.org/doc/install
Download gomphs source or use git

Example

```
$ git clone https://github.com/42wim/gomphs.git
$ cd gomphs
$ go build
```
