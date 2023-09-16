---
title:  "Tensorflow.js POC #8: Super Resolution with waifu2x (II)"
metadate: "2020-06-19"
categories: [ Tensorflow, "Pre-trained Model", Image to Image Transformer ]
image: "/assets/images/lena400x400-waifu2x_artwork.png"
visit: "https://wiki.barco.com/display/~WJLEE/Super+Resolution+of+Images"
layout: post
---

<body>
    <script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=" crossorigin="anonymous"></script>

    <script src="{{ site.url }}{{ site.baseurl }}/assets/plugins/jquery.event.move.js"></script>
    <script src="{{ site.url }}{{ site.baseurl }}/assets/plugins/jquery.twentytwenty.js"></script>
    <script>
      $(function()
      {

        $(".twentytwenty-container").eq(0).twentytwenty({default_offset_pct: 0.5,before_label: 'bicubic',after_label: 'waifu2x_artwork',click_to_move: true});
        $(".twentytwenty-container").eq(1).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x_artwork',click_to_move: true});
        $(".twentytwenty-container").eq(2).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_artwork_y',click_to_move: true});
        $(".twentytwenty-container").eq(3).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_photo',click_to_move: true});

        $(".twentytwenty-container").eq(4).twentytwenty({default_offset_pct: 0.5,before_label: 'bicubic',after_label: 'lanczos3',click_to_move: true});
        $(".twentytwenty-container").eq(5).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'lanczos3',click_to_move: true});
        $(".twentytwenty-container").eq(6).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_photo',click_to_move: true});
        $(".twentytwenty-container").eq(7).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_artwork_y',click_to_move: true});
        $(".twentytwenty-container").eq(8).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x_artwork',click_to_move: true});
        $(".twentytwenty-container").eq(9).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_artwork_y',click_to_move: true});
        $(".twentytwenty-container").eq(10).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x_photo',click_to_move: true});

      });
    </script>
</body>



| Git Repo                                                                                                                                         | Status                                                                                                                                                                | Progress                                                                                                                    | Comments                                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| [![waifu2x](https://img.shields.io/badge/waifu2x_tfjs-gray?logo=tensorflow)](https://git.barco.com/users/wjlee/repos/waifu2x-tfjs/browse) | [![status](https://tailab.barco.com:9443/deeplearningcomputing/waifu2x-tfjs/badges/master/pipeline.svg)](https://tailab.barco.com:9443/deeplearningcomputing/waifu2x-tfjs/pipelines) | [![progress](https://img.shields.io/badge/waifu2x_tfjs-POC-red)](http://dlc.barco.com:3002/)|tensorflow.js POC #8|


[![](https://rebrand.ly/dlc_png_url)](https://rebrand.ly/dlc_uml_url)


### avatar255x287

avatar255x287 is a 255x287 size PNG animation. We use it to identify the aliasing reduction of the SR.

waifu2x-photo = waifu2x-artwork_y = waifu2x-artwork > lanczos3 > bicubic

#### Quality comparison: bicubic < waifu2x_artwork
{% slider2020 %}
  ![bicubic]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-bicubic.png)
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-waifu2x_artwork.png)
{% endslider2020 %}

#### Quality comparison: lanczos3 < waifu2x_artwork
{% slider2020 %}
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-lanczos3.png)
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-waifu2x_artwork.png)
{% endslider2020 %}

#### Quality comparison: waifu2x_artwork = waifu2x_artwork_y

{% slider2020 %}
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-waifu2x_artwork.png)
  ![waifu2x_artwork_y]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-waifu2x_artwork_y.png)
{% endslider2020 %}

#### Quality comparison: waifu2x_artwork = waifu2x_photo

{% slider2020 %}
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-waifu2x_artwork.png)
  ![waifu2x_photo]({{ site.url }}{{ site.baseurl }}/assets/images/avatar255x287-waifu2x_photo.png)
{% endslider2020 %}

### lena400x400

lena400x400 is a 400x400 size JPG with natural human. We use it to identify the color richness and fine struture of the SR.

 waifu2x-artwork_y = waifu2x-artwork > waifu2x-photo > lanczos3 = bicubic

#### Quality comparison: bicubic = lanczos3

{% slider2020 %}
  ![bicubic]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-bicubic.png)
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-lanczos3.png)
{% endslider2020 %}

#### Quality comparison: waifu2x_artwork > lanczos3

{% slider2020 %}
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-waifu2x_artwork.png)
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-lanczos3.png)
{% endslider2020 %}

#### Quality comparison: waifu2x_artwork > waifu2x_photo

{% slider2020 %}
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-waifu2x_artwork.png)
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-waifu2x_photo.png)
{% endslider2020 %}

#### Quality comparison: waifu2x_artwork = waifu2x_artwork_y

{% slider2020 %}
  ![waifu2x_artwork]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-waifu2x_artwork.png)
  ![waifu2x_artwork_y]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-waifu2x_artwork_y.png)
{% endslider2020 %}

#### Quality comparison: lanczos3 < waifu2x_photo

{% slider2020 %}
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-lanczos3.png)
  ![waifu2x_photo]({{ site.url }}{{ site.baseurl }}/assets/images/lena400x400-waifu2x_photo.png)
{% endslider2020 %}

## Next step
* WenGL version of waifu2x.js



