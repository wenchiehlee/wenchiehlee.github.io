---
title:  "Deep Learning Computing CI/CD Framework (II)"
date: 2020-08-22
categories: [DevOps]
image: "https://miro.medium.com/max/945/1*qehZ1KLTEO6y8tcCwlwWzQ.png"
visit: "http://dlc.barco.com"
toc: true
tags: 
author: wjlee
---

[![](https://rebrand.ly/dlc_png_url)](https://rebrand.ly/dlc_uml_url)

### Delete all non-running PODs
```sh
kubectl get pod --all-namespaces | \
awk '{if ($4 != "Running") \
system ("kubectl -n " $1 " delete pods " $2  " --grace-period=0 " " --force ")}'
```
 

## References
* [How To Install Kubernetes On Ubuntu 18.04](https://phoenixnap.com/kb/install-kubernetes-on-ubuntu)
* [How to Install and Configure Kubernetes (k8s) on Ubuntu 18.04 LTS](https://www.linuxtechi.com/install-configure-kubernetes-ubuntu-18-04-ubuntu-18-10/)
* [在 Kubernetes 上安装 Gitlab CI Runner](https://www.qikqiak.com/post/gitlab-runner-install-on-k8s/)
* [How To Monitor Kubernetes With Prometheus](https://phoenixnap.com/kb/prometheus-kubernetes-monitoring)
* [kubernetes101-introduction-tutorial](https://blog.techbridge.cc/2018/12/01/kubernetes101-introduction-tutorial/)
* [Kubernetes 基礎教學（一）原理介紹](https://medium.com/@C.W.Hu/kubernetes-basic-concept-tutorial-e033e3504ec0)
* [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
* [How To Access Kubernetes Dashboard Externally](https://www.thegeekdiary.com/how-to-access-kubernetes-dashboard-externally/)
* [Kubernetes 基礎教學（一）原理介紹](https://medium.com/@C.W.Hu/kubernetes-basic-concept-tutorial-e033e3504ec0)
* [Kubernetes 基礎教學（二）實作範例：Pod、Service、Deployment、Ingress](https://medium.com/@C.W.Hu/kubernetes-implement-ingress-deployment-tutorial-7431c5f96c3e)
* [Kubernetes 基礎教學（三）Helm 介紹與建立 Chart](https://medium.com/@C.W.Hu/kubernetes-helm-chart-tutorial-fbdad62a8b61)
* [My Favorite CLI Tools](https://switowski.com/blog/favorite-cli-tools?fbclid=IwAR3FU2WZaotaLyNuY0N3_6X0md3WkDKvkY2dpA9c_6luNBIZrGUL4QBShTY)
