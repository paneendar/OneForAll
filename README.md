# OneForAll

[![Build Status](https://travis-ci.org/shmilylty/OneForAll.svg?branch=master)](https://travis-ci.org/shmilylty/OneForAll)
[![codecov](https://codecov.io/gh/shmilylty/OneForAll/branch/master/graph/badge.svg)](https://codecov.io/gh/shmilylty/OneForAll)
[![Maintainability](https://api.codeclimate.com/v1/badges/1287668a6b4c72af683e/maintainability)](https://codeclimate.com/github/shmilylty/OneForAll/maintainability)
[![License](https://img.shields.io/github/license/shmilylty/OneForAll)](https://github.com/shmilylty/OneForAll/tree/master/LICENSE)
[![python](https://img.shields.io/badge/python-3.6+-blue)](https://github.com/shmilylty/OneForAll/tree/master/)
[![python](https://img.shields.io/badge/release-v0.4.5-brightgreen)](https://github.com/shmilylty/OneForAll/releases)

👊**OneForAll is a powerful subdomain collection tool**  📝[English Document](https://github.com/shmilylty/OneForAll/tree/master/docs/en-us/README.md)

![Example](./docs/usage_example.svg)

## 🚀Getting Started Guide

📢Please be sure to take a moment to read this document to help you quickly become familiar with OneForAll!

<details>
<summary><b>🐍Installation requirements</b></summary>

OneForAll is based on [Python 3.6.0]( https://www.python.org/downloads/release/python-360/) developed and tested, OneForAll requires a version higher than Python 3.6.0 to run.
To install the Python environment, please refer to [Python 3 Installation Guide](https://pythonguidecn.readthedocs.io/zh/latest/starting/installation.html#python-3). Check the Python and pip3 versions by running the following commands:
```bash
python -V
pip3 -V
```
If you see output similar to the following, it means there is no problem with the Python environment:
```bash
Python 3.6.0
pip 19.2.2 from C:\Users\shmilylty\AppData\Roaming\Python\Python36\site-packages\pip (python 3.6)
```
</details>

<details>
<summary><b>✔Installation steps (git version)</b></summary>

1. **download**

Since the project is **under development**, it will be updated and iterated continuously. When downloading, please use `git clone` to clone the latest code repository, which will also facilitate subsequent updates. It is not recommended to download from Releases because the version in Releases Updates are slow and inconvenient.
This project has been mirrored in [Code Cloud](https://gitee.com/shmiylty/OneForAll.git)(Gitee). It is recommended to use Code Cloud for cloning in China, which is faster:


```bash
git clone https://gitee.com/shmilylty/OneForAll.git
```
or:
```bash
git clone https://github.com/shmilylty/OneForAll.git
```

2. **Install**

You can install OneForAll dependencies through pip3. The following is an example of using **pip3** to install dependencies under **Windows system**: Note: If your Python3 is installed in the system Program Files directory, such as: `C:\Program Files\Python36`, then please run the command prompt cmd as an administrator to execute the following command!

```bash
cd OneForAll/
python3 -m pip install -U pip setuptools wheel -i https://mirrors.aliyun.com/pypi/simple/
pip3 install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/
python3 oneforall.py --help
```

For other system platforms, please refer to [Dependency Installation](https://github.com/shmilylty/OneForAll/tree/master/docs/installation_dependency.md). If you find that compiling a certain dependent library fails during the dependency installation process, you can refer to it. [FAQs and Answers.md](https://github.com/shmilylty/OneForAll/tree/master/docs/troubleshooting.md) The solutions are in the document. If you still can't solve the problem, please join the group to provide feedback.

3. **renew**

Execute the following command to **update** the project (modifications to `/config/setting.py` and `/config/api.py` can be saved):

```bash
git stash # Temporarily store local changes
git fetch --all # Pull project updates
git pull # Download coverage
git stash pop # Release local modifications
```
</details>

<details>
<summary><b>✔Installation steps (docker version)</b></summary>

First download and edit the configuration file, add your own `api` and personalization settings, and keep the original file structure



```
config
├── api.py
├── default.py
├── __init__.py
├── log.py
└── setting.py
```

Pull the image and execute it, replacing `~/.config` with the path to the folder where your own configuration file is located.

```shell
docker pull shmilylty/oneforall
docker run -it --rm -v ~/results:/OneForAll/results -v ~/.config:/OneForAll/config shmilylty/oneforall --target example.com run
```
The parameters are added directly to the end of the command, and the results will be output in the local directory `~/results`. If you need to save them to other locations, you can modify them yourself.
</details>


<details>
<summary><b>✨Usage Demonstration</b></summary>

If you installed the dependencies through pip3, use the following command to run the example:
```bash
python3 oneforall.py --target example.com run
python3 oneforall.py --targets ./example.txt run
```

![Example](./docs/usage_example.svg)

</details>

<details>
<summary><b>🧐Result Description</b></summary>

Let’s take the `python3 oneforall.py --target example.com run` command as an example. After OneForAll is executed normally with the default parameters, the corresponding results will be generated in the results directory:

![Result](./images/Result.png)

`example.com.csv` is the collection result of subdomains under each main domain.

`all_subdomain_result_1583034493.csv` is the summary result of subdomains collected every time OneForAll is run, including `example.com.csv`, which is convenient for obtaining all results in batch collection scenarios.

`result.sqlite3` is a database that stores the SQLite3 results collected from subdomains each time OneForAll is run. Its database structure is as follows:

![Database](./images/Database.png)

A table similar to `example_com_origin_result` stores the initial subdomain collection results of each module.

Tables similar to `example_com_resolve_result` store the results of parsing subdomains.

A table similar to `example_com_last_result` stores the last subdomain collection result (it will be generated after more than two collections).

A table similar to `example_com_now_result` stores the current subdomain collection results. In general, just pay attention to this table.

See [field explanation](./docs/field.md) for more information.
</details>

<details>
<summary><b>🤔Help</b></summary>

The command line parameters only provide some common parameters. For more detailed parameter configuration, please see [setting.py](https://github.com/shmiylty/OneForAll/tree/master/config/setting.py). If you think Feedback on some parameters that are frequently used in the command interface or any missing parameters is very welcome. Due to well-known reasons, if you want to use some blocked collection interfaces, please first go to [setting.py](https://github.com/shmiylty/OneForAll/tree/master/config/setting.py) to configure the agent. Some collection interfaces The module needs to provide an API (most of which can be obtained for free by registering an account). If you need to use it, please go to [api.py](https://github.com/shmiylty/OneForAll/tree/master/config/api.py) to configure the API. information, please ignore the relevant error message if you do not use it. (For detailed modules, please read [Collection Module Description](https://github.com/shmiylty/OneForAll/tree/master/docs/collection_modules.md))

The OneForAll command line interface is implemented based on [Fire](https://github.com/google/python-fire/). For more advanced usage of Fire, please refer to [Using Fire CLI](https://github.com/google/ python-fire/blob/master/docs/using-cli.md).

[oneforall.py](https://github.com/shmiylty/OneForAll/tree/master/oneforall.py) is the main program entrance, oneforall.py can call [brute.py](https://github.com/ shmilylty/OneForAll/tree/master/brute.py), [takerover.py](https://github.com/shmilylty/OneForAll/tree/master/takerover.py) and [dbexport.py](https:// github.com/shmilylty/OneForAll/tree/master/dbexport.py) and other modules, brute.py was independently created to facilitate subdomain blasting, takerover.py was independently created to facilitate subdomain takeover risk checking, and takerover.py was independently created to facilitate database The export is independent of dbexport.py. These modules can be run independently, and the parameters they accept are richer. If you want to use these modules individually, please refer to [Usage Help](https://github.com/shmilylty/OneForAll/tree /master/docs/usage_help.md)

❗Note: When you encounter some problems or doubts during use, please first search in [Issues](https://github.com/shmiylty/OneForAll/issues) to find the answer. You can also refer to [Common Questions and Answers](https://github.com/shmiylty/OneForAll/tree/master/docs/troubleshooting.md).

**oneforall.py usage help**

The following help information may not be the latest, you can use `python oneforall.py --help` to get the latest help information.

```bash
python oneforall.py --help
```
```bash
NAME
     oneforall.py - OneForAll help information

SYNOPSIS
     oneforall.py COMMAND | --target=TARGET <flags>

DESCRIPTION
     OneForAll is a powerful subdomain collection tool

     Example:
         python3 oneforall.py version
         python3 oneforall.py --target example.com run
         python3 oneforall.py --targets ./domains.txt run
         python3 oneforall.py --target example.com --valid None run
         python3 oneforall.py --target example.com --brute True run
         python3 oneforall.py --target example.com --port small run
         python3 oneforall.py --target example.com --fmt csv run
         python3 oneforall.py --target example.com --dns False run
         python3 oneforall.py --target example.com --req False run
         python3 oneforall.py --target example.com --takeover False run
         python3 oneforall.py --target example.com --show True run

     Note:
         The parameter alive has optional values True and False respectively indicating that the export is alive and all subdomain results are
         Optional values for the parameter port include 'default', 'small', 'large', see config.py configuration for details
         The optional formats of parameter fmt are 'csv', 'json'
         The parameter path defaults to None and uses the OneForAll result directory to generate the path.

ARGUMENTS
     TARGET
         Single domain name (choose one of the two required parameters)
     TARGETS
         File path of one domain name per line (choose one of the two required parameters)

FLAGS
     --brute=BRUTE
         s
     --dns=DNS
         DNS resolution subdomain (default True)
     --req=REQ
         HTTP request subdomain (default True)
     --port=PORT
         Request verification of the port range of the subdomain (default only detects port 80)
     --valid=VALID
         Export only surviving subdomain results (default False)
     --fmt=FMT
         Result saving format (default csv)
     --path=PATH
         Results saving path (default None)
     --takeover=TAKEOVER
         Check for subdomain takeover (default False)
```
</details>

## 🎉Project Introduction

Project address: [https://github.com/shmilylty/OneForAll](https://github.com/shmilylty/OneForAll)

The importance of information collection in penetration testing is self-evident. Subdomain collection is an essential and very important part of information collection. Currently, there are many open source subdomain collection tools on the Internet, but there are always some problems as follows: :

* **Not powerful enough**, there are not enough interfaces for subdomain collection, and it cannot automatically collect batches of subdomains. There is no automatic subdomain parsing, verification, FUZZ, and information expansion functions.
* **Not friendly enough**, although the command line module is more convenient, but when there are many optional parameters and the operations to be implemented are complicated, using the command line mode is not friendly enough. If there is a front-end with good interaction and high operability, then use it The experience will be much better.
* **Lack of maintenance**, many tools have not been updated in several years, issues and PRs do not exist.
* **Efficiency issue**, it does not use multi-process, multi-thread and asynchronous coroutine technology, and the speed is slow.

In order to solve the above pain points, this project application was born. As its name suggests, I hope that OneForAll will be a powerful and comprehensive and fast subdomain collection ultimate artifact🔨 that combines the strengths of hundreds of schools.

Currently, OneForAll is still under development. There are definitely many problems and areas for improvement. You are welcome to submit [Issues](https://github.com/shmiylty/OneForAll/issues) and [PR](https:// github.com/shmilylty/OneForAll/pulls), if you use it, give it a little star✨. There is currently a QQ group dedicated to OneForAll communication and feedback👨‍👨‍👦‍👦::[**824414244**] (//shang.qq.com/wpa/qunwpa?idkey=125d3689b60445cdbb11e4ddff38036b7f6f2abbf4f7957df5dddba81aa90771) (Group verification: information collection).

## 👍Features

* **Powerful collection capability**, for detailed modules, please read [Collection Module Description](https://github.com/shmiylty/OneForAll/tree/master/docs/collection_modules.md).
   1. Use certificate transparency to collect subdomains (currently there are 6 modules: `censys_api`, `certspotter`, `crtsh`, `entrust`, `google`, `spyse_api`)
   2. Regular checks to collect subdomains (currently there are 4 modules: domain transfer vulnerability exploit `axfr`, check cross-domain policy file `cdx`, check HTTPS certificate `cert`, check content security policy `csp`, check robots file` robots`, check the sitemap file `sitemap`, use NSEC records to traverse the DNS domain `dnssec`, and modules such as NSEC3 records will be added later)
   3. Use web crawler files to collect subdomains (there are currently 2 modules: `archivecrawl`, `commoncrawl`, this module is still being debugged, and this module needs to be added and improved)
   4. Use DNS data set to collect subdomains (currently there are 24 modules: `bevigil_api`, `binaryedge_api`, `bufferover`, `cebaidu`, `chinaz`, `chinaz_api`, `circl_api`, `cloudflare`, `dnsdb_api `, `dnsdumpster`, `hackertarget`, `ip138`, `ipv4info_api`, `netcraft`, `passivedns_api`, `ptrarchive`, `qianxun`, `rapiddns`, `riddler`, `robtex`, `securitytrails_api`, `sitedossier`, `threatcrowd`, `wzpc`, `ximcx`)
   5. Use DNS queries to collect subdomains (currently there are 5 modules: collecting subdomains `srv` by enumerating common SRV records and making queries, and querying MX, NS, SOA, TXT records in the DNS records of the domain name to collect subdomains)
   6. Use the threat intelligence platform data collection subdomain (currently there are 6 modules: `alienvault`, `riskiq_api`, `threatbook_api`, `threatminer`, `virustotal`, `virustotal_api`. This module needs to be added and improved)
   7. Use search engines to discover subdomains (there are currently 18 modules: `ask`, `baidu`, `bing`, `bing_api`, `duckduckgo`, `exalead`, `fofa_api`, `gitee`, `github` , `github_api`, `google`, `google_api`, `shodan_api`, `so`, `sogou`, `ya
