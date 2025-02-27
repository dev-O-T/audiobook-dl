# Note: This is a fork from jo1gi's repo!
Tested only with Storytel. Others can be broken.
## Differences to jo1gi's repo:
- Migrated from requests to curl_cffi to workaround CloudFlare block with Storytel
- Updated UserAgent string
- Added ebook support for storytel
- - use parameter --ebook 1

# audiobook-dl
![GitHub release](https://img.shields.io/github/v/release/jo1gi/audiobook-dl)
![GitHub top language](https://img.shields.io/github/languages/top/jo1gi/audiobook-dl)
![License](https://img.shields.io/github/license/jo1gi/audiobook-dl)
[![Donate using Ko-Fi](https://img.shields.io/badge/donate-kofi-00b9fe?logo=ko-fi&logoColor=00b9fe)](https://ko-fi.com/jo1gi)

CLI tool for downloading audiobooks from online sources.

## Supported Services
audiobook-dl currently supports downloading from the following sources:
- [audiobooks.com](https://audiobooks.com)
- [Blinkist](https://www.blinkist.com)
- [Chirp](https://www.chirpbooks.com/)
- [eReolen](https://ereolen.dk)
- [Everand (previously Scribd)](https://everand.com)
- [Librivox](https://librivox.org)
- [Nextory](https://nextory.com)
- [Overdrive / Libby](https://www.overdrive.com/)
- [Podimo](https://podimo.com)
- [Saxo](https://saxo.com)
- [Storytel](https://www.storytel.com/) / [Mofibo](https://mofibo.com)
- [YourCloudLibrary](https://www.yourcloudlibrary.com/)

[More info](./supported_sites.md)

## Installation
audiobook-dl can be installed from the repo itself or through pip.

If you want to use the newest version (can be unstable) run:
```shell
pip install "git+https://github.com/dev-O-T/audiobook-dl.git"
```
or
```shell
git clone https://github.com/dev-O-T/audiobook-dl.git
cd audiobook-dl
python3 setup.py install
```

Some features require [ffmpeg](https://ffmpeg.org/) which can be installed
through most package managers or from [ffmpeg.org/download.html](https://ffmpeg.org/download.html).

## Authentication

### Cookies
audiobook-dl uses Netscape cookie files for authentication in most cases. I use
[this](https://github.com/rotemdan/ExportCookies) extension to export my cookies
from the browser.

Cookies can be placed in current dir as `cookies.txt` or be given with the
`--cookie` argument.

### Login
[Some sources](./supported_sites.md) support authentication through login with
username and password (and sometimes library). Use the `--username` and
`--password` arguments or enter them through an interactive prompt.

## Downloading audiobooks
```shell
audiobook-dl -c <cookie file> <url>
```
**Most sites require you to provide the listening page not not just the
information page**

**Storytel**
```shell
audiobook-dl --username <username> --password <password> --library Storytel <url>
```

## Arguments

| Argument          | Value                                                             |
|-------------------|-------------------------------------------------------------------|
| url               | The url of the page where you listen to the audiobook             |
| -c/--cookie       | Path to a Netscape cookie file                                    |
| --combine         | Combine all output files into a single file (requires ffmpeg)     |
| --cover           | Only download cover                                               |
| -d/--debug        | Print debug information                                           |
| -o/--output       | Output location                                                   |
| --remove-chars    | List of characters that will be removed from output path          |
| --no-chapters     | Don't include chapters in output file                             |
| --output-format   | Output file format                                                |
| --verbose-ffmpeg | Show ffmpeg output in terminal                                    |
| --username        | Username to source (Required when using login)                    |
| --password        | Password to source (Required when using login)                    |
| --library         | Specific library on service (Sometimes required when using login) |

## Output
By default, audiobook-dl saves all audiobooks to `{title}` relative to the
current path. This can be changed with the `--output` argument. Path can be
customized by audiobook with the following fields:
- `title`
- `author`
- `series`
- `narrator`

Not all fields are available for all audiobooks.

The file extension can be changed with the `--output-format` argument.

## Configuration
audiobook-dl can be configured using a configuration file, which should be placed at:
- Windows: `C:\\Users\\$user\\AppData\\Local\\jo1gi\\audiobook-dl\\audiobook-dl.toml`
- Mac: `/Users/$user/Library/Application Support/audiobook-dl/audiobook-dl.toml`
- Linux `$XDG_CONFIG_DIR/audiobook-dl/audiobook-dl.toml`

### Authentications
Source credentials can be provided in the configuration file:
```toml
[sources.yourcloudlibrary]
username = "yourusername"
password = "supersecretpassword"
library = "hometown"
```

Cookie files can be specified in a similar way:
```toml
[sources.everand]
cookie_file = "./everand_cookies.txt"
```
Paths are relative to the configuration directory.
