# EPG

Tools for downloading the EPG (Electronic Program Guide) for thousands of TV channels from hundreds of sources.

## Table of contents

- ✨ [Installation](#installation)
- 🚀 [Usage](#usage)
- 💫 [Update](#update)
- 📺 [Playlists](#playlists)
- 🗄 [Database](#database)
- 👨‍💻 [API](#api)
- 📚 [Resources](#resources)
- 💬 [Discussions](#discussions)
- 🛠 [Contribution](#contribution)
- 📄 [License](#license)

## Installation

First, you need to install [Node.js](https://nodejs.org/en) on your computer. You will also need to install [Git](https://git-scm.com/downloads) to follow these instructions.

After that open the [Console](https://en.wikipedia.org/wiki/Windows_Console) (or [Terminal](<https://en.wikipedia.org/wiki/Terminal_(macOS)>) if you have macOS) and type the following command:

```sh
git clone --depth 1 -b master https://github.com/iptv-org/epg.git
```

Then navigate to the downloaded `epg` folder:

```sh
cd epg
```

And install all the dependencies:

```sh
npm install
```

## Usage

To start the download of the guide, select one of the [supported sites](SITES.md) and paste its name into the command below:

```sh
npm run grab -- --site=example.com
```

And once the download is complete, the guide will be saved to the `guide.xml` file.

```sh
Usage: npm run grab -- [options]

Options:
  -s, --site <name>             Name of the site to parse
  -c, --channels <path>         Path to *.channels.xml file (required if the "--site" attribute is
                                not specified)
  -o, --output <path>           Path to output file (default: "guide.xml")
  -l, --lang <code>             Filter channels by language (ISO 639-2 code)
  -t, --timeout <milliseconds>  Override the default timeout for each request
  -d, --delay <milliseconds>    Override the default delay between request
  --days <days>                 Override the number of days for which the program will be loaded
                                (defaults to the value from the site config)
  --maxConnections <number>     Limit on the number of concurrent requests (default: 1)
  --cron <expression>           Schedule a script run (example: "0 0 * * *")
  --gzip                        Create a compressed version of the guide as well (default: false)
```

### Access the guide by URL

You can make the guide available via URL by running your own server:

```sh
npm run serve
```

After that, the guide will be available at the link:

```
http://localhost:3000/guide.xml
```

In addition it will be available to other devices on the same local network at the address:

```
http://<your_local_ip_address>:3000/guide.xml
```

### Parallel downloading

By default, the guide for each channel is downloaded one by one, but you can change this behavior by increasing the number of simultaneous requests using the `--maxConnections` attribute:

```sh
npm run grab -- --site=example.com --maxConnections=10
```

But be aware that under heavy load, some sites may start return an error or completely block your access.

### Use custom channel list

Create an XML file and copy the descriptions of all the channels you need from the [/sites](sites) into it:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<channels>
  <channel site="arirang.com" lang="en" xmltv_id="ArirangTV.kr" site_id="CH_K">Arirang TV</channel>
  ...
</channels>
```


And then specify the path to that file via the `--channels` attribute:

```sh
npm run grab -- --channels=path/to/custom.channels.xml
```

### Run on schedule

If you want to download the guide automatically on a schedule, you need to pass a valid [cron expression](https://crontab.guru/) to the script using the `--cron` attribute:

```sh
npm run grab -- --site=example.com --cron="0 0 * * *"
```

## Update

If you have downloaded the repository code according to the instructions above, then to update it will be enough to run the command:

```sh
git pull
```

And then update all the dependencies:

```sh
npm install
```

If you want to download all of the websites at once, you can put this into a .bat file.

Create a .bat file with the name "download_sites.bat" and input this code:

```sh
@echo off

:: Change directory
cd C:\Users\justi\epg

:: Define the list of sites
set "sites=9tv.co.il abc.net.au allente.dk allente.fi allente.no allente.se andorradifusio.ad anteltv.com.uy arianaafgtv.com arianatelevision.com arirang.com artonline.tv awilime.com bein.com beinsports.com berrymedia.co.kr cablego.com.pe cableplus.com.uy canalplus.com cgates.lt clickthecity.com cosmote.gr cubmu.com dens.tv digiturk.com.tr directv.com.uy dishtv.in disneystar.com dsmart.com.tr dstv.com elcinema.com ena.skylifetv.co.kr energ eek.cl entertainment.ie firstmedia.com flixed.io foxsports.com.au foxtel.com.au frikanalen.no gatotv.com getafteritmedia.com guida.tv guidatv.sky.it horizon.tv i.mjh.nz i24news.tv indihometv.com ionplustv.com ipko.com knr.gl kvf.fo m.tving.com magticom.ge mako.co.il maxtv.hrvatskitelekom.hr maxtvgo.mk mediagenie.co.kr mediaklikk.hu mediaset.it melita.com meo.pt meuguia.tv mewatch.sg mi.tv mncvision.id mon-programme-tv.be movistarplus.es mtel.ba mts.rs mujtvprogram.cz myafn.dodmedia.osd.mil mysky.com.ph mytvsuper.com nhk.or.jp nhkworldpremium.com nostv.pt novacyprus.com novasports.gr nuevosiglo.com.uy nzxmltv.com ontvtonight.com osn.com pbsguam.org player.ee.co.uk pickx.be playtv.unifi.com.my plex.tv programacion-tv.elpais.com programacion.tcc.com.uy programetv.ro programme-tv.net programme-tv.vini.pf programtv.onet.pl raiplay.it reportv.com.ar rthk.hk rtmklik.rtm.gov.my rtp.pt ruv.is sat.tv shahid.mbc.net siba.com.co singtel.com sjonvarp.is sky.co.nz sky.de skylife.co.kr streamingtvguides.com superguidatv.it taiwanplus.com tapdmv.com teliatv.ee telkussa.fi telsu.fi tivu.tv toonamiaftermath.com turksatkablo.com.tr tv-programme.telecablesat.fr tv.blue.ch tv.cctv.com tv.dir.bg tv.lv tv.magenta.at tv.mail.ru tv.movistar.com.pe tv.nu tv.post.lu tv.trueid.net tv.yandex.ru tv2go.t-2.net tv24.co.uk tv24.se tvcesoir.fr tvcubana.icrt.cu tvgids.nl tvguide.com tvguide.myjcom.jp tvhebdo.com tvheute.at tvim.tv tvireland.ie tvmi.mt tvmusor.hu tvpassport.com vidio.com virginmediatelevision.ie virgintvgo.virginmedia.com visionplus.id vtm.be walesi.com.fj watch.sportsnet.ca watchyour.tv wavve.com web.magentatv.de webtv.delta.nl worldfishingnetwork.com xumo.tv zap.co.ao zuragt.mn"

:: Loop through sites and run command
for %%s in (%sites%) do (
    echo Downloading %%s...
    npm run grab -- --site=%%s --maxConnections=10
)

pause
```
This .bat file takes all the websites mentioned in the link above, and runs eatch and every one of them. Depending on your network speed, the download rate might vary

## Playlists

Playlists with already linked guides can be found in the [iptv-org/iptv](https://github.com/iptv-org/iptv) repository.

## Database

All channel data is taken from the [iptv-org/database](https://github.com/iptv-org/database) repository. If you find any errors please open a new [issue](https://github.com/iptv-org/database/issues) there.

## API

The API documentation can be found in the [iptv-org/api](https://github.com/iptv-org/api) repository.

## Resources

Links to other useful IPTV-related resources can be found in the [iptv-org/awesome-iptv](https://github.com/iptv-org/awesome-iptv) repository.

## Discussions

If you have a question or an idea, you can post it in the [Discussions](https://github.com/orgs/iptv-org/discussions) tab.

## Contribution

Please make sure to read the [Contributing Guide](https://github.com/iptv-org/epg/blob/master/CONTRIBUTING.md) before sending [issue](https://github.com/iptv-org/epg/issues) or a [pull request](https://github.com/iptv-org/epg/pulls).

And thank you to everyone who has already contributed!

### Backers

<a href="https://opencollective.com/iptv-org"><img src="https://opencollective.com/iptv-org/backers.svg?width=890" /></a>

### Contributors

<a href="https://github.com/iptv-org/epg/graphs/contributors"><img src="https://opencollective.com/iptv-org/contributors.svg?width=890" /></a>

## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](LICENSE)
