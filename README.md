# diskover - File system crawler, storage search engine and analytics powered by Elasticsearch

[![License](https://img.shields.io/github/license/shirosaidev/diskover.svg?label=License&maxAge=86400)](./LICENSE)
[![Release](https://img.shields.io/github/release/shirosaidev/diskover.svg?label=Release&maxAge=60)](https://github.com/shirosaidev/diskover/releases/latest)
[![Sponsor Patreon](https://img.shields.io/badge/Sponsor%20%24-Patreon-brightgreen.svg)](https://www.patreon.com/diskover)
[![Donate PayPal](https://img.shields.io/badge/Donate%20%24-PayPal-brightgreen.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CLF223XAS4W72)
[![Buy PRO](https://img.shields.io/badge/Buy%20%24-PRO-red.svg)](https://www.patreon.com/diskover)

<img align="left" width="249" height="189" src="docs/diskover.png?raw=true" hspace="5" vspace="5" alt="diskover">

diskover is an open source file system crawler and disk space usage software that uses [Elasticsearch](https://www.elastic.co) to index and manage data across heterogeneous storage systems. Using diskover, you are able to more effectively search and organize files and system administrators are able to manage storage infrastructure, efficiently provision storage, monitor and report on storage use, and effectively make decisions about new infrastructure purchases.

As the amount of file data generated by business' continues to expand, the stress on expensive storage infrastructure, users and system administrators, and IT budgets continues to grow.

Using diskover, users can identify old and unused files and give better insights into data change, file duplication and wasted space.

diskover is written and maintained by Chris Park (shirosai) and runs on Linux and OS X/macOS using Python 2/3.

<div align="center"><img src="https://github.com/shirosaidev/diskover/blob/master/docs/diskover-diagram1.png?raw=true" alt="diskover diagram" width="800" height="525"/></div>

## Screenshots

diskover crawler and workerbots running in terminal<br>
<img align="left" width="400" src="https://github.com/shirosaidev/diskover/raw/master/docs/diskover-crawler-terminal-screenshot.png?raw=true" alt="diskover crawler">
<img width="400" src="https://github.com/shirosaidev/diskover/raw/master/docs/diskover-workerbot-terminal-screenshot.png?raw=true" alt="diskover worker bot"><br>
[diskover-web](https://github.com/shirosaidev/diskover-web) (diskover's web file manager, analytics app, file system search engine, rest-api)<br>
<img align="left" width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-dashboard-screenshot.png?raw=true" alt="diskover-web dashboard">
<img align="left" width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-filetree-screenshot.png?raw=true" alt="diskover-web file tree">
<img align="left" width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-advancedsearch-screenshot.png?raw=true" alt="diskover-web advanced search">
<img width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-tags-screenshot.png?raw=true" alt="diskover-web tags"><br>
Kibana dashboards/saved searches/visualizations and support for Gource<br>
<img align="left" width="400" src="docs/kibana-dashboarddark2-screenshot.png?raw=true" alt="kibana-screenshot">
<img width="400" src="docs/diskover-gource1-screenshot.png?raw=true" alt="diskover-gource">

### diskover Gource videos

<a href="https://youtu.be/InlfK8GQ-kM"><img align="left" width="400" src="https://img.youtube.com/vi/InlfK8GQ-kM/0.jpg" alt="gource video"></a>
<a href="https://youtu.be/qKLJjZ0TMqA"><img width="400" src="https://img.youtube.com/vi/qKLJjZ0TMqA/0.jpg" alt="gource video"></a>

## Installation Guide

### Requirements

* `Linux or OS X/macOS` (tested on OS X 10.11.6, Ubuntu 16.04/18.04)
* `Python 2.7. or Python 3.5./3.6.` (tested on Python 2.7.14, 3.5.3, 3.6.4) Python 3 recommended.
* `Python elasticsearch client module`
* `Python requests module`
* `Python scandir module`
* `Python progressbar2 module`
* `Python redis module`
* `Python rq module`
* `Elasticsearch 5` (local or [AWS ES Service](https://aws.amazon.com/elasticsearch-service/), tested on Elasticsearch 5.4.2, 5.6.4) Elasticsearch 6 is not supported yet.
* `Redis` (tested on 4.0.8)

Install the above Python modules using pip.

### Optional Installs

* [diskover-web](https://github.com/shirosaidev/diskover-web) (diskover's web file manager and analytics app)
* [Redis RQ Dashboard](https://python-rq.org/docs/monitoring/) (for monitoring redis queue)
* [sharesniffer](https://github.com/shirosaidev/sharesniffer) (for scanning your network for file shares and auto-mounting for crawls)
* [Kibana](https://www.elastic.co/products/kibana) (for visualizing Elasticsearch data, tested on Kibana 5.4.2, 5.6.4)
* [X-Pack](https://www.elastic.co/downloads/x-pack) (Kibana plugin for graphs, reports, monitoring and http auth)
* [Gource](http://gource.io) (for Gource visualizations of diskover Elasticsearch data, see videos above)
* `Python qumulo-api module` (for using Qumulo storage api, --qumulo cli option, install with pip, Python 2.7. only)

### Download

```sh
$ git clone https://github.com/shirosaidev/diskover.git
$ cd diskover
```

[Download latest version](https://github.com/shirosaidev/diskover/releases/latest)

### Community edition VS diskover PRO

The community edition of diskover allows up to a max 8 worker bots. To crawl using unlimited workers you will need to purchase a license for diskover pro. diskover pro also allows searching for dupes (finddupes) and comparing index data (hotdirs). To purchase diskover PRO, see diskover's Patreon page for pricing https://www.patreon.com/diskover. You can also buy pro license using PayPal.

### OVA image file (for vmware, etc)

If you don't want to set up everything yourself, I have an OVA file running the latest version of diskover/diskover-web. Fastest and best way to get up and running with diskover. diskover PRO license includes download link for ova's.

### Requirements

You need to have at least **Python 2.7. or Python 3.5.** and have installed required Python dependencies using `pip`.

```sh
$ pip install -r requirements.txt
```

## Getting Started

Copy diskover config `diskover.cfg.sample` to `diskover.cfg` and edit for your environment.

Start diskover worker bots (a good number might be cores x 2) with:

```sh
$ cd /path/with/diskover
$ python diskover_worker_bot.py
```
**Up to max 8 worker bots with community edition and unlimited with PRO**

Worker bots can be added during a crawl to help with the queue. To run a worker bot in burst mode (quit after all jobs done), use the -b flag. If the queue is empty these bots will die, so use `rq info` or `rq-dashboard` to see if they are running. Run `diskover-bot-launcher.sh` to spawn and kill multiple bots. Bots can be run on any host in the network as long as they have the same nfs/cifs mountpoint as rootdir (-d path) and can connect to ES and Redis (see wiki for more info).

Start diskover main job dispatcher and file tree crawler with:

```sh
$ python /path/to/diskover.py -d /rootpath/you/want/to/crawl -i diskover-indexname -a
```

**Defaults for crawl with no flags is to index from . (current directory) and files >0 Bytes and 0 days modified time. Empty files and directores are skipped (unless you use -s 0 and -e flags). Use -h to see cli options.**

## User Guide

[Read the wiki](https://github.com/shirosaidev/diskover/wiki) for more documentation on how to use diskover.

## Discussions/Questions

For discussions or questions about diskover, please ask on [Google Group](https://groups.google.com/forum/?hl=en#!forum/diskover).

## Bugs

For bugs about diskover, please use the [issues page](https://github.com/shirosaidev/diskover/issues).

## Sponsor diskover

To continue developing diskover and keep making it better, please consider sponsoring the project on [Patreon](https://www.patreon.com/diskover) or [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CLF223XAS4W72). Thank you so much to all the users and supporters!

## License

See the [license file](https://github.com/shirosaidev/diskover/blob/master/LICENSE).
