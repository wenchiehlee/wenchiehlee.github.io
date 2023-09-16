---
title:  "Tensorflow.js POC #8: Super Resolution with waifu2x"
metadate: "2020-06-19"
categories: [ Tensorflow, "Pre-trained Model", Image to Image Transformer ]
image: "/assets/images/avatar255x287-waifu2x_artwork.png"
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

        $(".twentytwenty-container").eq(0).twentytwenty({default_offset_pct: 0.5,before_label: 'bicubic',after_label: 'waifu2x',click_to_move: true});
        $(".twentytwenty-container").eq(1).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x',click_to_move: true});
        $(".twentytwenty-container").eq(2).twentytwenty({default_offset_pct: 0.5,before_label: 'SRGAN',after_label: 'waifu2x-NCNN',click_to_move: true});
        $(".twentytwenty-container").eq(3).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x',after_label: 'waifu2x-NCNN',click_to_move: true});
        $(".twentytwenty-container").eq(4).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x',after_label: 'SRMD-NCNN',click_to_move: true});
        $(".twentytwenty-container").eq(5).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x',after_label: 'Anime4K',click_to_move: true});
        $(".twentytwenty-container").eq(6).twentytwenty({default_offset_pct: 0.5,before_label: 'bicubic',after_label: 'Anime4K',click_to_move: true});

        $(".twentytwenty-container").eq(7).twentytwenty({default_offset_pct: 0.5,before_label: 'bicubic',after_label: 'waifu2x_artwork',click_to_move: true});
        $(".twentytwenty-container").eq(8).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x_artwork',click_to_move: true});
        $(".twentytwenty-container").eq(9).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_artwork_y',click_to_move: true});
        $(".twentytwenty-container").eq(10).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_photo',click_to_move: true});

        $(".twentytwenty-container").eq(11).twentytwenty({default_offset_pct: 0.5,before_label: 'bicubic',after_label: 'lanczos3',click_to_move: true});
        $(".twentytwenty-container").eq(12).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'lanczos3',click_to_move: true});
        $(".twentytwenty-container").eq(13).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_photo',click_to_move: true});
        $(".twentytwenty-container").eq(14).twentytwenty({default_offset_pct: 0.5,before_label: 'waifu2x_artwork',after_label: 'waifu2x_artwork_y',click_to_move: true});
        $(".twentytwenty-container").eq(15).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x_photo',click_to_move: true});
      });
    </script>
</body>



| Git Repo                                                                                                                                         | Status                                                                                                                                                                | Progress                                                                                                                    | Comments                                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| [![waifu2x](https://img.shields.io/badge/waifu2x_tfjs-gray?logo=tensorflow)](https://git.barco.com/users/wjlee/repos/waifu2x-tfjs/browse) | [![status](https://tailab.barco.com:9443/deeplearningcomputing/waifu2x-tfjs/badges/master/pipeline.svg)](https://tailab.barco.com:9443/deeplearningcomputing/waifu2x-tfjs/pipelines) | [![progress](https://img.shields.io/badge/waifu2x_tfjs-POC-red)](http://dlc.barco.com:3002/)|tensorflow.js POC #8|

[![](https://rebrand.ly/dlc_png_url)](https://rebrand.ly/dlc_uml_url)

## Overview
Super Resolution of images are important for video quality. Common SR like bicubic or lanczos3, now embedded in GPU as default SR. But, in 4K display or larger display, common SR is not enough, SR with Deep learning provide significant improvements on differnt target images. 

Super resolution of images highly depends the properties of the image, like animation, line draw, or a full color complex nature images will have different results on different algorithms. Here we benchmark several traditional SR algorithm of bicubic, lanczos3, (Bell, and ....) from [imageenlarger](https://www.imageenlarger.com/) and do a comparison with a DL SR on line draw or animation style image. 

Now we provide A/B Test on the different target images to verify the results of deep learning and normal images.

## A/B test on waifu2x-NCNN vs. waifu2x vs. lanczos3 vs. bicubic vs. SRGAN

### 1096x632_PPT_image

1096x632_PPT_image is a 1096x632 size PNG with words and graph PPT. We use it to identify the clearance of the SR.

SRMD-NCNN = waifu2x-NCNN = waifu2x > lanczos3 > bicubic > Anime4K > SRGAN (bicubic is most GPU interpolation algorithm. So lanczos3 and waifu2x show better results to normal GPU). SRGAN, Anime4K: SR result is GG..

#### Quality comparison: bicubic < waifu2x
{% slider2020 %}
  ![bicubic]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image-bicubic.png)
  ![waifu2x]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_waifu2x_art_noise1_scale_tta_1.png)
{% endslider2020 %}

#### Quality comparison: lanczos3 < waifu2x
{% slider2020 %}
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image-lanczos3.png)
  ![waifu2x]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_waifu2x_art_noise1_scale_tta_1.png)
{% endslider2020 %}

#### Quality comparison: SRGAN < waifu2x. 
SRGAN is GG

{% slider2020 %}
  ![SRGAN]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image-SRGAN.png)
  ![waifu2x-NCNN]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_Waifu2x-NCNN-Vulkan.png)
{% endslider2020 %}

#### Quality comparison: waifu2x = waifu2x-NCNN

{% slider2020 %}
  ![waifu2x]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_waifu2x_art_noise1_scale_tta_1.png)
  ![waifu2x-NCNN]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_Waifu2x-NCNN-Vulkan.png)
{% endslider2020 %}

#### Quality comparison: waifu2x = SRMD-NCNN

{% slider2020 %}
  ![waifu2x]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_waifu2x_art_noise1_scale_tta_1.png)
  ![SRMD-NCNN]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_SRMD-NCNN-Vulkan.png)
{% endslider2020 %}


#### Quality comparison: waifu2x > Anime4K

{% slider2020 %}
  ![waifu2x]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_waifu2x_art_noise1_scale_tta_1.png)
  ![Anime4K]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_Anime4K.png)
{% endslider2020 %}

#### Quality comparison: bicubic > Anime4K

{% slider2020 %}
  ![bicubic]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image-bicubic.png)
  ![Anime4K]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_Anime4K.png)
{% endslider2020 %}


### Part II
Check [Part II]({{ site.url }}{{ site.baseurl }}/SuperResolution-with-waifu2x-II/)

## Next step
* WenGL version of waifu2x.js
* Speedup of waifu2x

## References
* [waifu2x tensorflow c++ repo](https://git.barco.com/users/wjlee/repos/waifu2x-tfjs/browse)
* [waifu2x tensorflow.js repo](https://git.barco.com/users/wjlee/repos/waifu2x/browse)


## Jekyll image comparison slider
In this page, [twentytwenty image compare slider](https://github.com/zurb/twentytwenty) is used to enable image comparison slider.

To enable it in your post, please add the following code into your markdown documents


``` js
{% slider2020 %}
  ![lanczos3]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image-lanczos3.png)
  ![Waifu2x]({{ site.url }}{{ site.baseurl }}/assets/images/1096x632_PPT_image_Waifu2x-NCNN-Vulkan.png)
{% endslider2020 %}
```

After above, you can have first version of image compariosn slider. But, if you want to change the label of the images. you will need to find default_with_image_slider.html and modify the code as below in the beginning of the .md file

``` js
<body>
    <script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=" crossorigin="anonymous"></script>

    <script src="{{ site.url }}{{ site.baseurl }}/assets/plugins/jquery.event.move.js"></script>
    <script src="{{ site.url }}{{ site.baseurl }}/assets/plugins/jquery.twentytwenty.js"></script>
    <script>
      $(function()
      {

        $(".twentytwenty-container").eq(0).twentytwenty({default_offset_pct: 0.5,before_label: 'lanczos3',after_label: 'waifu2x-NCNN',click_to_move: true});
      });
    </script>
</body>
```

You also can check the code of this site in [gitbucket](https://git.barco.com/users/wjlee/repos/dlcv2.barco.com/browse) and search for all 'twentytwenty'