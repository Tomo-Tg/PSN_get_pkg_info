# PSN_get_pkg_info.py (c) 2018-2019 by "windsurfer1122"
Extract package information from header and PARAM.SFO of PS3/PSX/PSP/PSV/PSM and PS4 packages.

## Goals
* One-for-all solution to retrieve all header data and PARAM.SFO data from PSN packages
* Decryption of PS3 encrypted data to get all data
* Support of all known package types: PS3/PSX/PSP, PSV/PSM, PS4
* Extraction of PS3/PSX/PSP/PSV/PSM packages similar to pkg2zip and pkg_dec
  * PSP: Extraction as EBOOT.PBP for [NPdrm 0.9 plugin](https://github.com/qwikrazor87/npdrm_free) on PSP or on PSV with [Adrenaline](https://github.com/TheOfficialFloW/Adrenaline).<br>
    Extraction as ISO/CSO is not supported yet, there are other tools for this like [ISO~PBP Converter](https://sites.google.com/site/theleecherman/IsoPbpConverter) and [CISO Multi Compressor](https://sites.google.com/site/theleecherman/cisomulticompressor) plus homebrew [Takka](http://takka.tfact.net/2011/)'s [ISO Tool 1.981](https://wololo.net/downloads/index.php/download/7918) to integrate updates/patches and [Disc Change 2.6](https://www21.atwiki.jp/improper_code/pages/73.html#id_32933629) ([DL](https://www21.atwiki.jp/improper_code?cmd=upload&act=open&pageid=73&file=disc_change_2_6.zip)). And also [UMDGen](http://www.psx-place.com/resources/umd-gen-4-00.208/).<br>
* Easy enhancement of interpreting data (=done at the very end with all data at hand)
* Support http download streaming to avoid harddisk usage
* Support multiple output formats
* Support multiple debug verbosity levels
* Easy to maintain and no compiler necessary (=interpreter language)
* Cross platform support
  * Decision: Python 3
    * Compatible with Python 2 (target version 2.7)
      * Identical output
      * Forward-compatible solutions preferred
* Modular and flexible code for easy enhancement and/or extensions (of course there's always something hard-coded left)

## Execution
For available options execute: `PSN_get_pkg_info.py -h`<br>
It is recommended to place `--` before the package sources, to avoid them being used as targets, e.g. `PSN_get_pkg_info.py --raw -- 01.pkg 02.pkg` will never kill the 01.pkg!<br>
Use at your own risk!<br>
If you state URLs then only the necessary bytes are downloaded into memory. Note that the options "--raw" downloads the complete package once without storing the original data on the file system.

## Contributions welcome
* Especially information about how to interpret data is needed, e.g. content id
* See TODO.MD what is still left to do

## Requirements
* Python Modules
  * [pycryptodomex](https://www.pycryptodome.org/) (note the X at the end of the module name)
  * [requests](http://python-requests.org/)
  * [aenum](https://bitbucket.org/stoneleaf/aenum)

### Installing on Debian
1. Python 3, which is the recommended version, and most modules can be installed via apt.<br>
Install Python 3 and some modules via the following apt packages: `python3 python3-pip python3-requests`.<br>

1. Python 2 is the default on Debian, but comes with an outdated pip version until Debian 8.<br>
Note that with Python 2 ZRIF support is not possible at all.<br>
__Starting with Debian 9 "Stretch"__ install Python 2 modules via the following apt packages: `python-pip python-future python-requests`.<br>
For __Debian up to 8 "Jessie"__ use the pip version from the original [PyPi](https://pypi.org/project/pip/) source:<br>
   ```
   apt-get purge python-pip python-dev python-future
   apt-get autoremove
   wget https://bootstrap.pypa.io/get-pip.py
   python2 get-pip.py
   pip2 install --upgrade future
   ```

1. Install further necessary Python modules via pip.
   * Install pycryptodomex module:
     * Python 3: `pip3 install --upgrade pycryptodomex`
     * Python 2: `pip2 install --upgrade pycryptodomex`
   * Install aenum module:
     * Python 3: `pip3 install --upgrade aenum`
     * Python 2: `pip2 install --upgrade aenum`

### Installing on Windows
1. Install Python<br>
   Checked with Python 3.7 x64 on Windows 10 x64 Version 1803.
   * Get it from the [Python homepage](https://www.python.org/)
   * Install launcher for all users
   * Add Python to PATH<br>
     Adds %ProgramFiles%\Python37 + \Scripts to PATH
   * __Use Customize Installation (!!! necessary for advanced options !!!)__
   * Advanced Options
     * Install for all users

1. Install necessary Python modules via pip.
   * Start an __elevated(!!!)__ Command Prompt (Run As Admin via Right Click)
   * Update PIP itself first: `python -m pip install --upgrade pip`
   * Install requests module: `pip install --upgrade requests`
   * Install pycryptodomex module: `pip install --upgrade pycryptodomex`
   * Install aenum module: `pip install --upgrade aenum`
   * Exit Command Prompt: `exit`

Executing python scripts can be done via Windows Explorer or a Command Prompt. Normally no elevation is necessary for script execution, except when the python script wants to change something in the system internals.

## Using a HTTP Proxy with Python
* Linux: `export HTTP_PROXY="http://192.168.0.1:3128"; export HTTPS_PROXY="http://192.168.0.1:1080";`

## Original Source
git master repository at https://github.com/windsurfer1122

## License
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

## Additional Credits for Ideas and Several Details
* AnalogMan
* https://playstationdev.wiki/ (previously https://vitadevwiki.com/ & https://www.pspdevwiki.com/)
* http://www.psdevwiki.com/
* mmozeiko
* st4rk
* qwikrazor87
* jk3y
