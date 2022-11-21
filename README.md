# Realme OTA Downloader
![License](https://img.shields.io/github/license/R0rt1z2/realme-ota)
![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/R0rt1z2/realme-ota?include_prereleases)
![GitHub Issues](https://img.shields.io/github/issues-raw/R0rt1z2/realme-ota?color=red)

## Requirements
* Python 3.9 (or newer).

## Installation
### Windows
For convenience, a script has been provided to take care of installing all the requirements and the tool automatically (this has only been tested under Windows 10 and 11 using [Windows Terminal](https://github.com/microsoft/terminal)).
```powershell
# (Requires privilegies)
Invoke-WebRequest https://cdn.r0rt1z2.com/realme-ota/Install.ps1 | Invoke-Expression
```

### Linux
```bash
sudo apt install python3-pip
```
```bash
pip3 install --upgrade git+https://github.com/R0rt1z2/realme-ota
```

## Installation On Termux
```bash
apt update && apt upgrade -y
```
```bash
apt install git python
```
```bash
python3 -m pip install --upgrade pip
```
```bash
pip3 install --upgrade git+https://github.com/R0rt1z2/realme-ota
```

## Usage
```bash
usage: realme-ota [-h] [-v {0,1,2,3,4,5} | -s] [-r {0,1,2,3}] [-g GUID]
               [-i IMEI [IMEI ...]] [-b] [-d DUMP] [-o ONLY]
               product_model ota_version {1,2,3,4} [nv_identifier]

positional arguments:
  product_model         Product Model (ro.product.name).
  ota_version           OTA Version (ro.build.version.ota).
  {1,2,3,4}             RealmeUI Version (ro.build.version.realmeui).
  nv_identifier         NV (carrier) identifier (ro.build.oplus_nv_id) (if
                        none, provide 0 or omit).

optional arguments:
  -h, --help            show this help message and exit
  -v {0,1,2,3,4,5}, --verbosity {0,1,2,3,4,5}
                        Set the verbosity level. Range: 0 (no logging) to 5
                        (debug). Default: 4 (info).
  -s, --silent          Enable silent output (purge logging). Shortcut for
                        '-v0'.

request options:
  -r {0,1,2,3}, --region {0,1,2,3}
                        Use custom region for the request (GL = 0, CN = 1, IN
                        = 2, EU = 3).
  -g GUID, --guid GUID  The guid of the third line in the file
                        /data/system/openid_config.xml (only required to
                        extract 'CBT' in China).
  -i IMEI [IMEI ...], --imei IMEI [IMEI ...]
                        Specify one or two IMEIs for the request.
  -b, --beta            Try to get a test version (IMEI probably required).

output options:
  -d DUMP, --dump DUMP  Save request response into a file.
  -o ONLY, --only ONLY  Only show the desired value from the response.
```

## Extra Explanation
```bash
Find usage:
realme-ota --help
```
```bash
Get build.prop values:
getprop ro.product.name
getprop ro.build.version.ota
getprop ro.build.version.realmeui
getprop ro.build.oplus_nv_id
```
```bash
Examples:
# Realme 8 Pro (RMX3081)
realme-ota -r 2 -d /sdcard/out.txt RMX3081 RMX3081NV87_11.A.41_1410_202108181828 2 0
```
```bash
# Realme 9 Pro 5G (RMX3471)
realme-ota -r 2 -d /sdcard/ota.txt RMX3471 RMX3471_11.C.01_0000_000000000000 3 0
```
```bash
# Realme 3 Pro (RMX1851)
realme-ota -r 2 -d out.txt RMX1851 RMX1851EXNV1B_11.F.05_1050_202109230624 2 00011011

Help to Understand:

Command = realme-ota

--region = 2              [India]
--dump = out.txt          [directory]

product_model = RMX1851   [Device: codename]

ota_version = RMX1851EXNV1B_11.F.05_1050_202109230624  

realmeUI_Version = 2      [Realme UI 2 (Android 11).]

nv_identifier/nv_carrier = 00011011
```

## Additional notes
* If your request returns `flow limit` or status code `500`, try to wait a few minutes and then request again.
* Since Android 11 (RUI2), Realme started using components, which means you won't be able to get a full OTA link.
* The `--beta` option might not work correctly, it has not been fully tested!

## License
* This tool is licensed under the GNU (v3) General Public License. See `LICENSE` for more details.
