# MyJDownloader-RCE

This "exploit" is an authenticated RCE to get a reverse shell of a device using JDownloader2, and it has to be connected to a MyJDownloader account.

The python script uses the [public API of MyJDownloader](https://my.jdownloader.org/developers/) to install the `EventScripter` extension and deploy
a payload to download and execute a PowerShell reverse shell. To access the public API valid credentials must be provided.

The script was tested on Windows 10 Pro 21H1.

## Installation

Script depends on two other repositories:

- [EvilRATPy](https://github.com/dix0nym/EvilRATPy)
- [My.Jdownloader-API-Python-Library](https://github.com/dix0nym/My.Jdownloader-API-Python-Library) (currently a custom fork of the Python API)

Clone the repo with its submodules:

`git clone --recurse-submodules https://github.com/dix0nym/MyJDownloader-RCE.git`

## Usage

```bash
$ python3 exploit.py --help

usage: exploit.py [-h] [-e EMAIL] [-p PASSWORD] [-s SCRIPT] lhost lport

Script to get RevShell via MyJdownloader

positional arguments:
  lhost                 ip address of attacker
  lport                 port of attacker

options:
  -h, --help            show this help message and exit
  -e EMAIL, --email EMAIL
                        email of MyJdownloader user
  -p PASSWORD, --password PASSWORD
                        password of MyJdownloader user
  -s SCRIPT, --script SCRIPT
                        location of custom event script
```

## Background

In an attempt to update and replace my current VPN setup remotely I lost access to my homelab. I was 400 km away from the homelab's location.
My only "access" at that time was a JDownloader instance connected to my MyJDownloader account running on a Windows machine. So I tried hard to find a way to get some kind of access on that machine.
First I found that you can install extension via the web interface, and then I tried `Scheduler`, but it couldn't execute any custom scripts/commands. I found the `EventScripter`, and it took quite a while to get a working payload.
Finally, I got a working reverse shell and I cloud finish the VPN setup. So a Happy End!

And here we are - quite a bit more sophisticated - in the mentioned situation the attempts less focused and more like trying different payloads in the web interface, hoping one would work...