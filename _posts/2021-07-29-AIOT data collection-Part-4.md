---
title:  "AIOT data collection- Part 4- Alert"
metadate: "2021-07-29 21:40:10"
categories: ["BigData"]
image: "https://newrelic.com/sites/default/files/wp_blog_inline_files/telegraf1.png"
visit:
tags: [featured]
featured: true
author: wjlee
---

# Overview

# Alert with Grafana/InfluxDB

The basic pipeline of grafana/prometheus/alertmanager/influxDB

[![](https://liquidreply.net/wp-content/uploads/2021/07/architecture.png)](https://liquidreply.net/howto-send-your-alerts-to-microsoft-teams)

The complete block diagram 

[![](https://www.plantuml.com/plantuml/png/ZPHTJ_is5CRl_IcE-h-hbBwqW50r0Hsm2GbGD-2gwyLfV9fQE7PcEspLkky-noLAdEMYDv3aFB_Zn-UbTzQXSMKkcVqKga23EGZboEmm9VY70Mmn_SoCBXM_rr8RE92K-gyge0qdS_ge3QgCsB-CCIUS97XzNi7hu--m4WL9eGXsNlLXoS0lHBpA2U-OPK9bZ3Nd3VRE5OlncCjqDjgYIVKerVdYOZQPZYqf9tB_Pm1eWHGlj0Ud_VH5YxwUN4yYPjRFnCXLXCpxaNcBcKycquYvw6TY97Ps2JyoGwIwfFMe8ypjA1UfqLRlN9LWBCVf7fKY6MMvWX-6k6-5fCn_0qaxnux3OTKFvujE1bReeU7m2ESK_5Z1pxWbcLZ7XOwvRgc3-adjPFdtmyznowDZ-wiUwDNZwWr-AyaSOgA_w07vrU0E5SANi5ZA2EklUw3Ugvh2VQXXa9zLx2CZnK-rPIoLkkH-KTRBl932bPmsOGquEjoYzGrCqLfKtE0Wx5CZ_4CzvOKsZan0KktV52a7Wwe0bNhz-5Mz_rcLOWD9QxJEoM8Bl3-4DBxpOTsy9acQrLdNJIrzLrkH6Lk_Q4uIFWgETUBcGdLpMmwb3iaPMp-WtMyr6kxzDeRd7MlVxV8PFB8oEYUtfz8ckGsLt_oK9Ekb9EDUK5M95_2gdTY959tGYaMnIjkaw4hR8U_ePlrzz8RLJ-4pDCQdFjIyHDUux5pZfHuG29CK2XAU8khAK-tvy2RwkhS04HxxUnjCHlEmEFtl3Cbev6LnznRVk_HkK2YXCdWZPpkOfw9fE0iAbbgpLJD1PBj35EJTGvQbqsFmdInHmb8fxRosJX2B8UcvsSaVXC__Et3KjNUArEec578teno9QrEyTXNh_AMQQV7KWx25n4D7DRg9vl3qAn-EQAvxUzk5cc7jI7jtnXi9izVTW3jIlCpbVm00)](http://www.plantuml.com/plantuml/uml/ZPHTJ_is5CRl_IcE-h-hbBwqW50r0Hsm2GbGD-2gwyLfV9fQE7PcEspLkky-noLAdEMYDv3aFB_Zn-UbTzQXSMKkcVqKga23EGZboEmm9VY70Mmn_SoCBXM_rr8RE92K-gyge0qdS_ge3QgCsB-CCIUS97XzNi7hu--m4WL9eGXsNlLXoS0lHBpA2U-OPK9bZ3Nd3VRE5OlncCjqDjgYIVKerVdYOZQPZYqf9tB_Pm1eWHGlj0Ud_VH5YxwUN4yYPjRFnCXLXCpxaNcBcKycquYvw6TY97Ps2JyoGwIwfFMe8ypjA1UfqLRlN9LWBCVf7fKY6MMvWX-6k6-5fCn_0qaxnux3OTKFvujE1bReeU7m2ESK_5Z1pxWbcLZ7XOwvRgc3-adjPFdtmyznowDZ-wiUwDNZwWr-AyaSOgA_w07vrU0E5SANi5ZA2EklUw3Ugvh2VQXXa9zLx2CZnK-rPIoLkkH-KTRBl932bPmsOGquEjoYzGrCqLfKtE0Wx5CZ_4CzvOKsZan0KktV52a7Wwe0bNhz-5Mz_rcLOWD9QxJEoM8Bl3-4DBxpOTsy9acQrLdNJIrzLrkH6Lk_Q4uIFWgETUBcGdLpMmwb3iaPMp-WtMyr6kxzDeRd7MlVxV8PFB8oEYUtfz8ckGsLt_oK9Ekb9EDUK5M95_2gdTY959tGYaMnIjkaw4hR8U_ePlrzz8RLJ-4pDCQdFjIyHDUux5pZfHuG29CK2XAU8khAK-tvy2RwkhS04HxxUnjCHlEmEFtl3Cbev6LnznRVk_HkK2YXCdWZPpkOfw9fE0iAbbgpLJD1PBj35EJTGvQbqsFmdInHmb8fxRosJX2B8UcvsSaVXC__Et3KjNUArEec578teno9QrEyTXNh_AMQQV7KWx25n4D7DRg9vl3qAn-EQAvxUzk5cc7jI7jtnXi9izVTW3jIlCpbVm00)

## Alert Event Trigger
Related to alert event system, there are two questions, what events will trigger the alert (so called **alert event trigger**) and when context (so called **alert event context**) will show to user when alert.

## Alert Event Context

Here is an example of grafana chart that iframe embedded a grafana chart showing the accumlated number of ClickShare user cohort.

### ClickShare User Cohort Newest Count

[![live demo](https://img.shields.io/badge/live_demo-green?logo=grafana)](https://dlc.barco.com:3000/d/pLMAu/user-cohort?orgId=1)

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
  <iframe src="https://dlc.barco.com:3000/d-solo/pLMAu/user-cohort?orgId=1&now-30d&to=now&panelId=2" width="1024px" height="768px" frameborder="0"></iframe>
<!-- Google embed ends -->
</div>

### ClickShare User Cohort 30d Monitoring

[![live demo](https://img.shields.io/badge/live_demo-green?logo=grafana)](https://dlc.barco.com:3000/d/pLMAu/user-cohort?orgId=1)

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
  <iframe src="https://tailab1.barco.com:3000/d-solo/pLMAu/user-cohort?orgId=1&from=now-30d&to=now&panelId=4" width="1024px" height="768px" frameborder="0"></iframe>
<!-- Google embed ends -->
</div>

### ClickShare Rating in Feedback 30d Monitoring

[![live demo](https://img.shields.io/badge/live_demo-green?logo=grafana)](https://dlc.barco.com:3000/d/sCo107Gnz/user-feedback)

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
<iframe src="https://dlc.barco.com:3000/d-solo/sCo107Gnz/user-feedback?orgId=1&from=now-30d&to=now&panelId=6" width="1024px" height="768px" frameborder="0"></iframe>
<!-- Google embed ends -->
</div>

### ClickShare Total Feedback 30d Monitoring

[![live demo](https://img.shields.io/badge/live_demo-green?logo=grafana)](https://dlc.barco.com:3000/d/sCo107Gnz/user-feedback)

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
<iframe src="https://dlc.barco.com:3000/d-solo/sCo107Gnz/user-feedback?orgId=1&from=now-30d&to=now&panelId=2" width="1024px" height="768px" frameborder="0"></iframe>
<!-- Google embed ends -->
</div>



# Refrences


