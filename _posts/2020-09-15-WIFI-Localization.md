---
title:  "Pytorch POC #6: WIFI Indoor Positioning"
date: 2020-09-15
categories: [ Tensorflow, "Fine-Tune Model", "WIFI Indoor Positioning", "Supervised Learning","BigData", "IOT"]
author: wjlee
image: "https://ja-si.com/wp-content/uploads/2017/05/Indoor-Location-Tracking.jpg"
visit: "http://dlc.barco.com:3234"
---

## Project Map of DLC 

[![](https://rebrand.ly/dlc_png_url)](https://rebrand.ly/dlc_uml_url)

## Overview

This is still a very early stage of POC. With a pre-defined datasets, with many WIFI APP signal strengths data try to prdict the real location of the indoor room. 

This might be the first POC try to define our input and output data formats.

Also, this POC also be a high level connector of several different components together since it will leaverage multi factor information to conclude a precise indoor locationing. 

[![](https://www.dvginteractive.com/wp-content/uploads/2019/08/indoors_IPS-768x436.png)](https://www.dvginteractive.com/arcgis-indoors-enable-indoor-positioning-and-a-common-operating-picture/)

[![](https://www.dvginteractive.com/wp-content/uploads/2019/08/indoors_assets.png)](https://www.dvginteractive.com/arcgis-indoors-enable-indoor-positioning-and-a-common-operating-picture/)

When it comes to localization within buildings, a distinction can be made between **client-based** (**Active tracking**) and **server-based positioning** ( **Passive tracking** + **Active tracking** as optional). **Client-based localization** enables determining the position directly on the end user's device (e. g. smartphone). In the case of **server-based localization**, positioning takes place on a server.

[![](https://www.infsoft.com/portals/0/Images/solutions/basics/quick-start/Infographic-indoor-positioning-client-and-server-based-847.jpg)](https://www.infsoft.com/solutions/basics/quick-start-indoor-positioning)

## Technologies for Client-Based Indoor Positioning 

Client-Based Indoor Positioning Compared: Wi-Fi vs. BLE vs. UWB vs. RFID vs. Ultrasound

[![](https://www.infsoft.com/Portals/0/Images/blog/2021/technologies-server-based-positioning.jpg)](https://www.infsoft.com/blog/technologies-for-server-based-indoor-positioning-compared)

| Technology | Accuracy               | Range |
|------------|------------------------|-------|
| WIFI       | <15m                   | <150m |
| BLE 4      | <8m                    | <75m  |
| BLE 5.1    | <1m                    | <75m  |
| UWB        | <30cm                  | <150m |
| RFID       | Present detection only | <1m   |

## Technologies for Server-Based Indoor Positioning 

Server-Based Indoor Positioning Compared: Wi-Fi vs. BLE vs. UWB vs. RFID vs. Ultrasound

[![](https://www.infsoft.com/Portals/0/Images/blog/2021/technologies-server-based-positioning.jpg)](https://www.infsoft.com/blog/technologies-for-server-based-indoor-positioning-compared)

| Technology     | Accuracy               | Range           |
|----------------|------------------------|-----------------|
| WIFI           | <15m                   | <150m           |
| BLE 4          | <8m                    | <75m            |
| BLE 5.1        | <1m                    | <75m            |
| UWB            | <30cm                  | <150m           |
| RFID           | Present detection only | <1m             |
| **Ultrasound** | **<4m**                | **<8m or Wall** |

| Indoor Positioning Technology          | Comments                                                                 |
|----------------------------------------|--------------------------------------------------------------------------|
| Client-Based                           | No server setup. Use existing framework. but, low precision              |
| Server-Based (Passive tracking only)   | Server only. 3-5 sec delay. Not realtime application                     |
| Server-Based (Passive+Active tracking) | Need sever+client to get hybrid info for realtime & stable location info |

## Deeper insights of Client-Based Indoor Positioning 

[![](https://media.springernature.com/full/springer-static/image/art%3A10.1186%2Fs13673-020-00222-0/MediaObjects/13673_2020_222_Fig7_HTML.png?as=webp)](https://hcis-journal.springeropen.com/articles/10.1186/s13673-020-00222-0/figures/7)


## Indoor Positioning Use Cases

Many different [use cases](https://www.infsoft.com/use-cases/articlepage).

## POC using find3

| Git Repo                                                                                                           | Status                                                                                                                                                                                               | Progress                                                                                                         | Comments                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| [![find3](https://img.shields.io/badge/project-find3-green)](https://git.barco.com/users/wjlee/repos/find3/browse) | [![status](https://tailab.barco.com:9443/deeplearningcomputing/finetunemodels/find3/badges/master/pipeline.svg)](https://tailab.barco.com:9443/deeplearningcomputing/finetunemodels/find3/pipelines) | [![progress](https://img.shields.io/badge/POC-red?logo=docker)](http://dlc1.barco.com:8005/view/dashboard/barco) | Family=barco <br>[API:Devices by Loc (w 1 mins)](http://dlc1.barco.com:8005/api/v1/by_location/barco?history=1&num_scanners=1&randomized=0) |

Get info of device='dlc2.barco.com' & family='barco' from find3 server 

```bash
curl -s -L -XGET "http://dlc1.barco.com:8005/api/v1/location_basic/barco/dlc2.barco.com"
```
Get WIFI/BT SSID, BSSID, RSSID of the location and device

```bash
curl -XGET http://dlc1.barco.com:8005/api/v1/location/barco/dlc2.barco.com
```

Get all devices within 1 minsfrom family='barco' from find3 server and output it as a table

```bash
curl -s -L -XGET "http://dlc1.barco.com:8005/api/v1/by_location/barco?history=1&num_scanners=1" | jq -s '.[] | .locations | .[] |.devices' | jsoncsv -A  | mkexcel | csvcut  -d , -C 5  |csvlook --snifflimit 0  | sudo tee output.txt
```
Update GPS info of location 'Aris Cube' (device=dlc2.barco.com)

```bash
curl -s -L -XPOST "http://dlc1.barco.com:8005/api/v1/gps" -H "Content-Type:application/json" --data-binary '{"f":"Barco","l":"Aris Cube","gps":{"lat":25.01290,"lon":121.46701,"alt":0}}'
```
Delete family=barco data (Dangersous operation!!! Warning!!!)

```bash
 curl -s -L -XDELETE "http://dlc1.barco.com:8005/api/v1/database/barco"
```
### Block diagram of find3

[![](https://www.plantuml.com/plantuml/png/bLB1Rjf04BtlLup83San1BMAE4I1fgcuLAuKJjI7mJkOLTQprkwQD2hyUzS6GMmiHRrOyflttkgzcKVdqVggqCAzAYxHOW6AFTaDPWH_1S0QizVScehbDwEDXNVIshpL0sCbsIDeB79EuY24yCfhWWLB4_34EEMLOSKv9AeahPY4k3mms7fVJkDOwcnykqQRcTlC5DFxqUXBl5Fq5ajqsxL1A-DcEW1qG2nB4pp6S9DR8kxtQzdTVurRqZkuiIIxGdUbd8n6evPm0ZUd0eIcFA2WQUF5VZZSA9OJUBQ6VGqdoAI7mptyPy9zxRNWZQx-FCrXwSZ2Cv6ijz3sx4tPg7zOt20Zx9J3IlUhMWdtWbWUumWX0beQ9lOmc2y7uGPMJRGeqofo6JAJJSMA2on_iwSW2y-buj1MpbXQesIiacr0-btkqkCM3Ytbpta_UzpBRcYDuEdSuonPfD7vICJgnORooARHGuSaMhDP0CBdcjRr3eINLcw97jVe20QdnHqZVDyHUz0cpyb-D4aXYYwNs0bqMbvj85Qddrhm01U3yKUtSSjk4kpw5bORdCDE8K7dr8wWGHJdlNrtDBFCVoAv-qmYBiK5PhkWwI-gxFlLOLtHjiPvne94f-3RXtDTKrYM4Zr1Gt3YaLXMXVu7)](http://www.plantuml.com/plantuml/uml/bLB1Rjf04BtlLup83San1BMAE4I1fgcuLAuKJjI7mJkOLTQprkwQD2hyUzS6GMmiHRrOyflttkgzcKVdqVggqCAzAYxHOW6AFTaDPWH_1S0QizVScehbDwEDXNVIshpL0sCbsIDeB79EuY24yCfhWWLB4_34EEMLOSKv9AeahPY4k3mms7fVJkDOwcnykqQRcTlC5DFxqUXBl5Fq5ajqsxL1A-DcEW1qG2nB4pp6S9DR8kxtQzdTVurRqZkuiIIxGdUbd8n6evPm0ZUd0eIcFA2WQUF5VZZSA9OJUBQ6VGqdoAI7mptyPy9zxRNWZQx-FCrXwSZ2Cv6ijz3sx4tPg7zOt20Zx9J3IlUhMWdtWbWUumWX0beQ9lOmc2y7uGPMJRGeqofo6JAJJSMA2on_iwSW2y-buj1MpbXQesIiacr0-btkqkCM3Ytbpta_UzpBRcYDuEdSuonPfD7vICJgnORooARHGuSaMhDP0CBdcjRr3eINLcw97jVe20QdnHqZVDyHUz0cpyb-D4aXYYwNs0bqMbvj85Qddrhm01U3yKUtSSjk4kpw5bORdCDE8K7dr8wWGHJdlNrtDBFCVoAv-qmYBiK5PhkWwI-gxFlLOLtHjiPvne94f-3RXtDTKrYM4Zr1Gt3YaLXMXVu7)


| Signal strength (dBm) | Expected Quality                                                                                     |
|-----------------------|------------------------------------------------------------------------------------------------------|
| -90                   | Chances of connecting are very low at this level                                                     |
| -80                   | Unreliable signal strength                                                                           |
| -67                   | Reliable signal strength– the edge of what Cisco considers to be adequate to support Voice over WLAN |
| -55                   | Anything down to this level can be considered excellent signal strength.                             |
| -30                   | Maximum signal strength, you are probably standing right next to the access point.                   |

### A snapshot of find3 active RSSI & its BSSID, SSID on 2020/08/31 nearby dlc2.barco.com


| Rssi | Freq      | Type     | Algo | Rate | BSSID                  | SSID                       |
|------|-----------|----------|------|------|------------------------|----------------------------|
| -50  | 2.412 GHz | 802.11n  | 6    | 12   | E8  D0  FC  BF  18  0D | ClickShare-Mobile-CX20     |
| -52  | 5.825 GHz | 802.11ac | 7    | 8    | 04  D4  C4  D3  42  84 | ASUS_Automation_5G         |
| -72  | 5.825 GHz | 802.11ac | 7    | 8    | E4  AA  EA  58  43  93 | CX-50-DEMO-RICHEN          |
| -50  | 2.457 GHz | 802.11n  | 7    | 12   | B0  7F  B9  82  03  04 | NETGEAR25                  |
| -66  | 2.437 GHz |          | 7    | 7    | F0  1D  2D  5D  A9  C0 | Barco                      |
| -58  | 5.24 GHz  | 802.11n  | 6    | 8    | 28  24  FF  69  5B  B7 | TestRoom_CSE800_mac (5GHz) |
| -55  | 2.437 GHz |          | 7    | 7    | F0  1D  2D  5B  54  61 | Barco Guest                |
| -61  | 5.24 GHz  | 802.11ac | 1    | 8    | 3C  91  80  84  95  07 | ClickShare-HW-UniSee       |
| -71  | 5.24 GHz  | 802.11ac | 7    | 8    | E4  AA  EA  35  04  65 | ClickShare-1863551994      |
| -55  | 2.437 GHz | 802.11n  | 7    | 12   | BE  42  4F  CB  C3  44 | TestRoom-EAP-WinServer     |
| -46  | 5.785 GHz |          | 6    | 8    | 7C  10  C9  61  97  84 | TAI-QA-ASUSROG-6E_5G       |
| -49  | 5.18 GHz  | 802.11ac | 7    | 8    | 10  63  C8  97  03  9F | TAI_MR08                   |
| -58  | 5.785 GHz | 802.11ac | 7    | 8    | BC  CF  4F  CB  C3  43 | TestRoom-EAP               |
| -63  | 5.18 GHz  | 802.11ac | 6    | 8    | 3C  91  80  84  9C  5D | ClickShare-1862300001      |
| -59  | 5.3 GHz   |          | 7    | 6    | F0  1D  2D  5A  D5  6F | Barco                      |
| -57  | 2.412 GHz | 802.11n  | 7    | 12   | D4  6E  0E  41  61  EA | keroro24                   |
| -60  | 5.32 GHz  |          | 9    | 6    | F0  1D  2D  5B  54  6E | Barco Guest                |
| -68  | 5.58 GHz  |          | 7    | 6    | F0  1D  2D  5A  D9  8D | BarcoIoT                   |
| -55  | 5.18 GHz  | 802.11ac | 7    | 8    | 3C  91  80  84  9C  5F | TAI_MR09                   |
| -59  | 5.745 GHz | 802.11ac | 7    | 8    | E4  AA  EA  74  46  FF | ClickShare-Mobile-CX50     |
| -53  | 2.412 GHz |          | 7    | 7    | F0  1D  2D  5A  D5  62 | BarcoIoT                   |
| -69  | 5.805 GHz | 802.11ac | 6    | 8    | D4  6E  0E  41  61  E9 | keroro5                    |
| -62  | 5.24 GHz  | 802.11ac | 7    | 8    | F8  A2  D6  6E  09  CF | TestRoom_CSE200P_mac       |
| -58  | 5.785 GHz | 802.11ac | 7    | 8    | BE  43  4F  CB  C3  45 | TestRoom-EAP-WinServer     |
| -73  | 5.68 GHz  |          | 7    | 6    | F0  1D  2D  5C  27  CF |                            |
| -39  | 2.447 GHz | 802.11n  | 7    | 12   | 2C  FD  A1  CD  32  38 | ASUS                       |
| -69  | 5.765 GHz | 802.11ac | 7    | 8    | 70  2E  D9  42  F4  76 | MAXHUB-6BF                 |
| -56  | 5.745 GHz | 802.11ac | 7    | 8    | E4  AA  EA  35  21  3F | SClickShare-1863551600     |
| -58  | 5.785 GHz | 802.11ac | 7    | 8    | BE  43  4F  CB  C3  44 | TestRoom-PSK2              |
| -62  | 2.412 GHz | 802.11n  | 7    | 12   | E8  D0  FC  BF  13  5F | ClickShare-1862300251      |
| -59  | 5.18 GHz  | 802.11ac | 7    | 8    | E4  AA  EA  74  2C  D3 | ClickShare-1863553421      |
| -60  | 2.452 GHz | 802.11n  | 7    | 12   | 04  D4  C4  35  69  E8 | ASUS_SQA_JessicaHsu_2.4G   |
| -59  | 5.18 GHz  | 802.11ac | 7    | 8    | 3C  91  80  84  95  D3 | ClickShare-MR12            |
| -69  | 2.412 GHz |          | 1    | 7    | F0  1D  2D  5A  D9  82 | BarcoIoT                   |
| -61  | 2.412 GHz | 802.11n  | 7    | 12   | BC  30  7E  F1  1D  9B | ClickShare Audi-1          |
| -61  | 5.18 GHz  | 802.11ac | 7    | 8    | 3C  91  80  84  97  59 | ClickShare-1862300078      |
| -60  | 5.32 GHz  |          | 7    | 6    | F0  1D  2D  5B  54  6F |                            |
| -78  | 2.437 GHz | 802.11n  | 7    | 8    | 02  21  6A  F8  2F  AF | DIRECT-ZWTAICLT24036msZe   |
| -62  | 5.24 GHz  | 802.11ac | 1    | 8    | 02  12  5F  17  67  2F | WiCS-2100-72E              |
| -59  | 2.462 GHz | 802.11n  | 7    | 12   | 00  D0  41  DC  13  C8 | myvita                     |
| -55  | 5.18 GHz  | 802.11ac | 7    | 8    | 3C  91  80  84  9F  25 | ClickShare-0716174986      |
| -71  | 5.18 GHz  | 802.11ac | 7    | 8    | 10  63  C8  A7  9E  23 | TAI_MR04                   |
| -86  | 5.18 GHz  | 802.11ac | 1    | 8    | 10  63  C8  96  FF  87 | TAI_MR01                   |
| -28  | 2.427 GHz | 802.11n  | 1    | 12   | 7A  DA  88  B2  74  EC |                            |
| -66  | 2.422 GHz | 802.11n  | 7    | 12   | BC  30  7E  DD  3D  FE | WiPG-1000-78C              |
| -56  | 5.18 GHz  | 802.11ac | 7    | 8    | F8  A2  D6  8D  BF  8F | ClickShare-1863550102      |
| -59  | 5.3 GHz   |          | 7    | 6    | F0  1D  2D  5A  D5  6D | BarcoIoT                   |
| -73  | 5.24 GHz  | 802.11n  | 7    | 8    | D8  61  62  8B  1D  EF | TAI-MR06-Pingtung          |
| -52  | 5.18 GHz  | 802.11ac | 7    | 8    | 12  63  C8  14  92  3B | DIRECT-BM                  |
| -83  | 5.68 GHz  |          | 7    | 6    | F0  1D  2D  5A  CC  AE | Barco Guest                |
| -81  | 5.26 GHz  |          | 7    | 6    | F0  1D  2D  5D  B2  AF |                            |
| -68  | 2.437 GHz | 802.11n  | 7    | 12   | BC  EE  7B  7D  46  C0 |                            |
| -81  | 5.745 GHz | 802.11ac | 7    | 8    | 02  12  5F  17  68  8C | WiCS-2100-88B              |
| -68  | 5.58 GHz  |          | 7    | 6    | F0  1D  2D  5A  D9  8E | Barco Guest                |
| -55  | 2.437 GHz | 802.11n  | 1    | 12   | BE  42  4F  CB  C3  43 | TestRoom-PSK2              |
| -77  | 5.745 GHz | 802.11ac | 7    | 8    | 02  12  5F  17  66  66 | WiCS-2100-665              |
| -52  | 5.18 GHz  | 802.11n  | 7    | 8    | 28  24  FF  4D  1B  FD | ClickShare-1872075087      |
| -82  | 5.2 GHz   | 802.11n  | 1    | 8    | BC  30  7E  D9  C3  F4 | ClickShare-8000000049      |
| -72  | 5.18 GHz  | 802.11ac | 7    | 8    | E4  AA  EA  74  26  59 | CX-50_Service              |
| -71  | 5.18 GHz  | 802.11ac | 7    | 8    | E8  D0  FC  BF  15  D1 | Agile 01                   |
| -58  | 5.18 GHz  | 802.11ac | 7    | 8    | 3C  91  80  84  95  B3 | ClickShare-1862300131      |
| -48  | 5.745 GHz | 802.11ac | 7    | 8    | 2C  FD  A1  CD  32  3C | ASUS_5G                    |
| -47  | 5.18 GHz  | 802.11ac | 6    | 8    | E4  AA  EA  58  45  8B | ClickShare-1863552495      |
| -84  | 5.22 GHz  | 802.11ac | 7    | 8    | 3C  91  80  84  98  13 | TAI_MR03                   |
| -69  | 5.18 GHz  | 802.11n  | 7    | 8    | B8  B7  F1  01  B0  2D | ClickShare-1873124000      |
| -45  | 2.412 GHz | 802.11n  | 1    | 12   | C8  60  00  AC  FB  30 | ASUS-FA                    |
| -64  | 2.462 GHz |          | 1    | 7    | F0  1D  2D  5C  27  C0 |                            |
| -68  | 5.58 GHz  |          | 7    | 6    | F0  1D  2D  5A  D9  8F | Barco                      |
| -54  | 2.412 GHz |          | 7    | 7    | F0  1D  2D  5A  D5  61 | Barco Guest                |
| -64  | 5.745 GHz | 802.11ac | 7    | 8    | 02  12  5F  17  67  F2 | WiCS-2100-LIN              |
| -53  | 5.2 GHz   | 802.11ac | 9    | 8    | 04  D4  C4  35  69  EC | ASUS_SQA_JessicaHsu_5G     |
| -64  | 2.462 GHz |          | 7    | 7    | F0  1D  2D  5C  27  C2 | BarcoIoT                   |
| -59  | 5.18 GHz  | 802.11ac | 7    | 8    | F8  A2  D6  8D  BF  5D | ClickShare-1863550098      |
| -81  | 5.745 GHz | 802.11ac | 7    | 8    | 02  12  5F  30  00  AC | WiCS-2100-0AB              |
| -53  | 2.462 GHz | 802.11n  | 7    | 12   | 00  4E  35  1A  C8  60 | TAI-ClickShare-WPA2-DFS    |
| -73  | 5.68 GHz  |          | 9    | 6    | F0  1D  2D  5C  27  CD | BarcoIoT                   |
| -59  | 5.18 GHz  | 802.11ac | 7    | 8    | F8  A2  D6  8D  CB  39 | ClickShare-1863550140      |
| -75  | 5.22 GHz  | 802.11n  | 7    | 8    | 28  24  FF  5B  05  05 | CSE-200-demo               |
| -61  | 5.18 GHz  | 802.11ac | 7    | 8    | 10  63  C8  BF  B1  81 | ClickShare-1862337967      |
| -80  | 5.26 GHz  |          | 7    | 6    | F0  1D  2D  5D  B2  AE | Barco Guest                |
| -53  | 5.18 GHz  | 802.11ac | 1    | 8    | A0  40  A0  82  49  0E | QA-test-5G                 |
| -51  | 2.412 GHz | 802.11n  | 7    | 12   | 10  63  C8  96  F7  F3 | ClickShare-T20             |
| -60  | 5.32 GHz  |          | 7    | 6    | F0  1D  2D  5B  54  6D | BarcoIoT                   |
| -43  | 5.22 GHz  |          | 7    | 8    | 6C  CD  D6  F5  9D  69 | HW_WIFI6E_5G               |
| -52  | 2.462 GHz | 802.11n  | 7    | 12   | 18  31  BF  C5  D1  38 | SQA_Balloon_24G            |
| -82  | 5.68 GHz  |          | 7    | 6    | F0  1D  2D  5A  CC  AF | Barco                      |
| -84  | 5.745 GHz | 802.11ac | 7    | 8    | 02  12  5F  30  06  4F | WiCS-2100-64E              |
| -45  | 2.437 GHz |          | 7    | 12   | 7C  10  C9  61  97  80 | TAI-QA-ASUSROG-6E_2.4G     |
| -58  | 5.18 GHz  | 802.11ac | 7    | 8    | E4  AA  EA  58  43  81 | ClickShare-1863552454      |
| -75  | 5.5 GHz   |          | 7    | 6    | F0  1D  2D  5D  A9  CD | BarcoIoT                   |
| -75  | 5.18 GHz  | 802.11ac | 7    | 8    | D8  F3  BC  54  4B  89 | ClickShare-1862375851      |
| -43  | 2.472 GHz |          | 7    | 12   | 08  36  C9  2F  78  F5 | TAI-QA-NetGear-2.4G        |
| -63  | 2.412 GHz | 802.11n  | 7    | 12   | 3C  91  80  84  9C  91 | ClickShare-1862300102      |
| -68  | 2.412 GHz |          | 6    | 7    | F0  1D  2D  5A  D9  80 | Barco                      |
| -66  | 2.437 GHz |          | 7    | 7    | F0  1D  2D  5D  A9  C2 | BarcoIoT                   |
| -63  | 5.5 GHz   | 802.11ac | 7    | 8    | 00  4E  35  1A  C8  70 | TAI-ClickShare-WPA2-DFS    |


### Live demo of find3 passive RSSI of dlc2.barco.com

[![live demo](https://img.shields.io/badge/live_demo-green?logo=grafana)](https://dlc.barco.com:3000/d/1nU7bPnnz/indoor-position?orgId=1)

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by MS -->
<iframe src="https://dlc.barco.com:3000/d-solo/1nU7bPnnz/indoor-position?orgId=1&from=now-10m&to=now&panelId=2" width="1024px" height="768px" frameborder="0"></iframe>
<!-- MS embed ends -->
</div>

## PPT

Can't see the following page? Please login to [MS office](https://login.microsoftonline.com/aeb84c91-6270-4446-ada5-d71ceba1d535/login) first.

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by MS -->
<iframe src="https://barcozone-my.sharepoint.com/personal/wj_lee_barco_com/_layouts/15/Doc.aspx?sourcedoc={50905eb0-8897-4ef0-92d7-d5f91be448b8}&amp;action=embedview&amp;wdAr=1.7777777777777777" width="1024px" height="768px" frameborder="0">This is an embedded <a target="_blank" href="https://office.com">Microsoft Office</a> presentation, powered by <a target="_blank" href="https://office.com/webapps">Office</a>.</iframe>
<!-- MS embed ends -->
</div>


## References
* [基于WiFi指纹的室内定位 (autoencoder)](https://duhuazhen.github.io/2017/01/03/wifi_locate/)
* [移動設備究竟是怎樣僅僅使用Wi-Fi 來定位的?](https://www.zhihu.com/question/20355764)
* [Wifi indoor positioning using Arduino and Machine Learning in 4 steps](https://eloquentarduino.github.io/2019/12/wifi-indoor-positioning-on-arduino/)
* [Fingerprinting Acoustic Localization Indoor Based on Cluster Analysis and Iterative Interpolation](https://www.researchgate.net/publication/328553362_Fingerprinting_Acoustic_Localization_Indoor_Based_on_Cluster_Analysis_and_Iterative_Interpolation)
* [Learning the Localization Function: Machine Learning Approach to Fingerprinting Localization](https://www.researchgate.net/publication/323957009_Learning_the_Localization_Function_Machine_Learning_Approach_to_Fingerprinting_Localization#pf24)
* [WiDeep: WiFi-based Accurate and Robust Indoor Localization System using Deep Learning](http://sig-iss.work/percom2019/papers/p232-abbas.pdf)
* [UJIndoorLoc dataset download](https://archive.ics.uci.edu/ml/datasets/ujiindoorloc) [![nextcloud](https://img.shields.io/badge/UJIndoorLoc_wifi_dataset-blue?logo=nextcloud)](http://dlc.barco.com:9980/apps/files/?dir=/Datasets/WIFI/UJIndoorLoc&fileid=217)
* [Wi-Fi- based Indoor Positioning System Using Smartphones](https://www.talentica.com/assets/white-papers/wifi-indoor-positioning-using-smartphones.pdf)
* [[MQTT] Mosquitto Docker 架設與設定詳細過程](https://weirenxue.github.io/2021/07/01/mqtt_mosquitto_docker/)
* [如何在家中任何地方檢查 Wi-Fi 信號強度](https://www.techadvisor.com/how-to/network-wifi/check-wi-fi-signal-strength-3803538/)
* [iABACUS: A Wi-Fi-Based Automatic Bus Passenger counting System](https://res.mdpi.com/d_attachment/energies/energies-13-01446/article_deploy/energies-13-01446-v2.pdf)
* [WIFI monitor mode- wiki](https://en.wikipedia.org/wiki/Monitor_mode)
* [WIFI Promiscuous mode- wifi](https://en.wikipedia.org/wiki/Promiscuous_mode)
* [wireshark](https://www.wireshark.org)
* [Wireshark- Analyzing Wireless Packet Captures](https://documentation.meraki.com/General_Administration/Tools_and_Troubleshooting/Analyzing_Wireless_Packet_Captures)
* [Scapy- Packet crafting for Python2 and Python3](https://scapy.net/)

