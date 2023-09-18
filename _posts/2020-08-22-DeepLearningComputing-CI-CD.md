---
title:  "Deep Learning Computing CI/CD Framework"
metadate: "2020-08-22"
categories: [DevOps]
image: "https://miro.medium.com/max/945/1*qehZ1KLTEO6y8tcCwlwWzQ.png"
visit: "http://dlc.dlc.com"
toc: true
tags: [featured]
author: wjlee
---

[![](http://www.plantuml.com/plantuml/png/LT2nJiCm40RWtKznYAqBxS3UD5ag8H4fY0KOZlX8hCPtuNnMoTlZIa33PEdx_TkdsoT3jHZOHvpTZOqK2KmMrvq2pwWO8T5d9kwfKfNpqnZw4rDAi7FfxqfRtWXzc96jHUy33t2_YW_ozSkxxSgnDz7Ebea0pvGaqYfye87O7qGzwVNNhNCMh1Ig8rmcTfkNMr7aWTuAkSq6QebpDb9u3Ya8_wCg-o0NQT2mdDTkVRohco8hQX_h1CBGZQ86h_oU3JxoD46zz1CLQ6YUP8d4bjoUsFziyHi0)](http://www.plantuml.com/plantuml/uml/LT2nJiCm40RWtKznYAqBxS3UD5ag8H4fY0KOZlX8hCPtuNnMoTlZIa33PEdx_TkdsoT3jHZOHvpTZOqK2KmMrvq2pwWO8T5d9kwfKfNpqnZw4rDAi7FfxqfRtWXzc96jHUy33t2_YW_ozSkxxSgnDz7Ebea0pvGaqYfye87O7qGzwVNNhNCMh1Ig8rmcTfkNMr7aWTuAkSq6QebpDb9u3Ya8_wCg-o0NQT2mdDTkVRohco8hQX_h1CBGZQ86h_oU3JxoD46zz1CLQ6YUP8d4bjoUsFziyHi0)

### POCs on Small changes from Open Source

1. Non-GPL license Open source projects are good basements to add value as POC espcially on Deep Learning areas.

![](https://miro.medium.com/max/945/1*hcER5n2X-fmtykty3oojUg.png)

### POCs on Short but Full Cycle Deployments

1. Projects use git/yaml script to setup CI/CD pipeline and deployment flows.

1. Easy to trasnfer from localhost to server via gitlab-runner

![](https://i.imgur.com/w7otxUB.png)

![](https://www.openshift.com/hubfs/DRAFT%20Copy%20of%20Installing%20Runner%20Blog-4.png)

### Deployments based on Docker/K8s for Scalablity, Portablity

1. Docker/K8s based deployment for scaiblity, portablity

![](https://miro.medium.com/max/945/1*qehZ1KLTEO6y8tcCwlwWzQ.png)

### All POCs setups as a Ecosystem

### Live sites

#### Gitlab server

|Git Repo| Status | Progress  | Comments|
|--| ------ | ------ | -- |
| [![gitlab](https://img.shields.io/badge/project-gitlab-green)]() | [![status](https://gitlab.com/barco.co/gitlab/badges/master/pipeline.svg)](https://gitlab.com/barco.co/gitlab/pipelines) | [![progress](https://img.shields.io/badge/progress-beta-green)](https://tailab.dlc.com:9443) User=root <br> [![gitlab grafana](https://img.shields.io/badge/grafana_of_gitlab-beta-green)](https://tailab.dlc.com:9443/-/grafana)|


#### [Current runners](https://tailab.dlc.com:9443/admin/runners)

| Servers | [![Runner](https://img.shields.io/badge/Runner-gree?logo=gitlab)](https://tailab.dlc.com:9443/admin/runners)  | OS    |[![tag](https://img.shields.io/badge/Tag-blue?logo=Google-tag-Manager)](https://tailab.dlc.com:9443/admin/runners)| Monitoring|
|---------|---------|-------|---|--------------------|
| [![dlc.dlc.com](https://img.shields.io/badge/dlc.dlc.com-yellow?logo=nginx)](http://dlc.dlc.com)                   | dlc          | Ubuntu18.04  |dlc, ubuntu, GPU| [![Node](https://img.shields.io/badge/Node-green?logo=grafana)](https://dlc.dlc.com:3000/d/Xhz-2PMWz/linux?orgId=1) [![GPU](https://img.shields.io/badge/GPU-gray?logo=nVidia)](https://dlc.dlc.com:3000/d/whRCVvEWz/nvidia-gpu?orgId=1) |
| [![dlc1.dlc.com](https://img.shields.io/badge/dlc1.dlc.com-purple?logo=nginx)](http://dlc1.dlc.com)                   | dlc1          | Ubuntu18.04      |dlc1, ubuntu, GPU| [![Node](https://img.shields.io/badge/Node-green?logo=grafana)](https://dlc.dlc.com:3000/d/Xhz-2PMWz/linux?orgId=1) [![GPU](https://img.shields.io/badge/GPU-gray?logo=nVidia)](https://dlc.dlc.com:3000/d/whRCVvEWz/nvidia-gpu?orgId=1) |
| [![dlc2.dlc.com](https://img.shields.io/badge/dlc2.dlc.com-green?logo=nginx)](http://dlc2.dlc.com)                   | dlc2          | Ubuntu18.04      |dlc2, ubuntu| [![Node](https://img.shields.io/badge/Node-green?logo=grafana)](https://dlc.dlc.com:3000/d/Xhz-2PMWz/linux?orgId=1) |

### How to setup dlc/dlc1 to run a TensorFlow GPU project

#### with Gitlab runner

##### Step 1: Add project to Gitlab https://tailab.dlc.com:9443/deeplearningcomputing

##### Step 1.5: If your project is in https://git.dlc.com/

You will need to import your project for gitlab CI/CD only by add your project into https://tailab.dlc.com:9443/root/git-sync-mirror. After that, bitbucket code will be automatically syced to gitlab server.

##### Step 2: Enable dlc gitlab runner and setup CI/CD


##### Step 3: See the CI/CD results

#### with ssh or RDP + admin account

Step 1: Check with wj.lee@dlc.com and ask for admin account of dlc

Step 2: With ssh or RPD to login to dlc


### How to setup your runner- How to install gitlab-runner in your ubuntu

Step 1: 

```bash
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
```

Step 2: 

```bash
sudo chmod +x /usr/local/bin/gitlab-runner
```
Step 3: 

```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
```

Step 4: 

```bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```
Step 5.0: Check https://docs.gitlab.com/runner/register/index.html

```bash
sudo gitlab-runner register
```
and register interactively.

or 

Step 5.1:

First, by command line for docker gitlab-runner

```bash
sudo gitlab-runner register -n --url https://tailab.dlc.com:9443/ --registration-token YOUR-TOKEN --executor docker --description ${HOSTNAME}.dlc.com --tag-list "ubuntu, docker, ${HOSTNAME}" --run-untagged="true" --docker-image "docker:stable" --docker-privileged --tls-ca-file=/etc/gitlab-runner/certs/ssl.csr 
```


PS: YOUR-TOKEN can be obtained from [Gitlab Server](#gitlab-server), in top menu, Admin Area->Runners to get the registration token. If you have no idea how to get '/etc/gitlab-runner/certs/ssl.csr', please check step XX.

Second, by command line for shell gitlab-runner

```bash
sudo gitlab-runner register -n --url https://tailab.dlc.com:9443/ --registration-token YOUR-TOKEN --executor shell --description ${HOSTNAME}.dlc.com --tag-list "ubuntu, shell, ${HOSTNAME}" --run-untagged="true" --tls-ca-file=/etc/gitlab-runner/certs/ssl.csr
```
If you have no idea how to get '/etc/gitlab-runner/certs/ssl.csr', please check step XX.

Step 6: Allow passwordless sudo

execute 
```
sudo joe /etc/sudoers
```
, then check and edit/add one line as

```bash
gitlab-runner  ALL=(ALL) NOPASSWD: ALL
```

if no joe command, please install

```bash
sudo apt-get install joe
```

Step 6.1: Modify /etc/gitlab-runner/config.toml

```bash
sudo joe /etc/gitlab-runner/config.toml
```

and change concurrent from 1 to 40 or more.
Also, for shell runner, please also add 

```bash
environment = ["GIT_SSL_NO_VERIFY=true"]
```

Step 7: Install git-lsf

```bash
sudo apt-get -y install git-lfs
```

Step 8: Verify gitlab-runner
```bash
sudo gitlab-runner verify
```

Step 9: 

For ubuntu 20.04, please do this to prevent [Gitlab runner shell executor doesn't work on Ubuntu focal](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/26309)

```bash
sudo rm /home/gitlab-runner/.bash_logout
```

Step X: If you want to upgrade gitlab-runner

This is optional step. If you want to upgrae gitlab-runner to newest one. Please do the following commands

```bash
sudo systemctl stop gitlab-runner.service
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
sudo systemctl start gitlab-runner.service
sudo systemctl status gitlab-runner.service
```

Step XX:
If you met the problem like below or you have no idea how to get '/etc/gitlab-runner/certs/ssl.csr'
```bash 
ERROR: Registering runner... failed
runner=CtzAuyzs status=couldn't execute POST against https://gitlab.test.com.tw/api/v4/runners: 
Post https://gitlab.test.com.tw/api/v4/runners: x509: certificate signed by unknown authority
PANIC: Failed to register this runner. Perhaps you are having network problems 
```
then follow the steps below to get self-certification and note the filename is 'ssl.crt'

```bash
SERVER=SERVER=tailab.dlc.com
PORT=9443

CERTIFICATE=/etc/gitlab-runner/certs/ssl.crt

sudo mkdir -p $(dirname "$CERTIFICATE")

openssl s_client -connect ${SERVER}:${PORT} -showcerts </dev/null 2>/dev/null | sed -e '/-----BEGIN/,/-----END/!d' | sudo tee "$CERTIFICATE" >/dev/null
```
then you get '/etc/gitlab-runner/certs/ssl.crt' you need for gitlab-runner register.

## References
* [Even the Smallest Side Project Deserves its CI/CD Pipeline](https://medium.com/better-programming/even-the-smallest-side-project-deserves-its-ci-cd-pipeline-281f80f39fdf)
* [GitLab Auto DevOps 深入淺出，自動部署，連設定檔不用？！](https://5xruby.tw/posts/gitlab-auto-devops/)
* [Install Blackbox Exporter to Monitor Websites With Prometheus](https://blog.ruanbekker.com/blog/2019/05/17/install-blackbox-exporter-to-monitor-websites-with-prometheus/)
* [Adding Custom badges 📛 to Gitlab...](https://medium.com/@iffi33/adding-custom-badges-to-gitlab-a9af8e3f3569)
* [Dynamic badges using shields.io](https://medium.com/@vemarav/dynamic-badges-using-shields-io-5948dcb2a99d)
* [Dynamic Badges with Shields.io and Runkit](https://medium.com/@Tnodes/dynamic-badges-with-shields-io-and-runkit-9e80283f1b47)
* [Markdown code for lots of small badges 🎀 📌 (shields.io, forthebadge.com etc) 😎](https://github.com/Naereen/badges)
* [Continuous Delivery for Machine Learning- Automating the end-to-end lifecycle of Machine Learning applications](https://martinfowler.com/articles/cd4ml.html)
* [Welcome to The Hitchhiker’s Guide to PlantUML!](https://crashedmind.github.io/PlantUMLHitchhikersGuide/index.html)
* [使用 OPENSSL 產生 SSL 憑證需要的 KEY 與 CSR](https://ruilung-notes.blogspot.com/2016/11/openssl-ssl-key-csr.html)
* [OPENSSL常用語法彙整](https://www.sslbuyer.com/index.php?option=com_content&view=article&id=129:openssl-command-intro&catid=25&Itemid=2595)
* [[Linux] GitLab Runner 證書錯誤註冊失敗 (x509: certificate signed by unknown authority)](https://ggm-coding.blogspot.com/2019/08/gitlab-runner-x509-certificate-signed.html)
