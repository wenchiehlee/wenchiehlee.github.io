---
title:  "Pre-trained Model, and What is Next Steps"
date: 2020-07-10
categories: ["Pre-trained Model"]
image: "/assets/images/DLC-mindmap.png"
author: wjlee
---

[![](https://rebrand.ly/dlc_png_url)](https://rebrand.ly/dlc_uml_url)

## Pre-trained Model

**Pre-trained model** for deep learning is the easiest entry point for an application developers to start the deep learning. With the pre-trained model as a blackbox, the application developers can focus on the problem he want to resolve with the pre-trained model and do the first integration and see the result of the integration resolve the target problem or not and how far it is to the perfect goal. If the goal become nearer, then a fine-tuning of pre-trained model or even a from-scratch pre-trained model can be addressed as a solution for the final integration.

There are several pre-trained models based on different programming langnauges and platforms.

### Tensorflow.js Pre-trained Models

* [Pre-trained model mirror from google](https://npm.taobao.org/mirrors/tfjs-models/savedmodel/)
* [npm tensorflow pre-train model](https://www.npmjs.com/search?q=%40tensorflow-models&ranking=popularity)

### IBM MAX Pre-trained Models

* [Pre-trained model from IBM](https://developer.ibm.com/technologies/artificial-intelligence/models)

### nVidia Pre-trained Models

* [NVIDIA Deep Learning Examples for Tensor Cores](https://github.com/NVIDIA/DeepLearningExamples)

### Pytorch Pre-trained Models

## Fine-tune Models

Once the pre-trained model gives some promise on the solution to the problem. A deeper and better solution can be addressed by fine-tuning the model. We call it as fine-tuning model of pre-trained model.

There are several strategies of fine-tuning the models from much training efforts to less ones.

![](https://miro.medium.com/proxy/1*9t7Po_ZFsT5_lZj445c-Lw.png)

Another view for different dataset size for fine-tining models.

![](https://miro.medium.com/max/688/1*PZjljzgxvFQkSU17js7-hQ.png)

## MLOps

Main idea of whole ML pipeline. 

![](https://miro.medium.com/max/1050/0*DMSY_Od9MvuJpkjO.png)

Basic idea of MLOps pipeline.

![](https://radiant.digital/wp-content/uploads/2021/02/MLOps_1-860x1024.jpg)

## References
* [Pre-Trained Machine Learning Models vs Models Trained from Scratch](https://heartbeat.fritz.ai/pre-trained-machine-learning-models-vs-models-trained-from-scratch-63e079ed648f#f3f6)
* [Why Not Training Model From Scratch ?](https://medium.com/@sagarsonwane230797/transfer-learning-from-pre-trained-model-for-image-facial-recognition-8b0c2038d5f0)
* [給ML Engineer的MLOps簡述: 持續開發機器學習Service的高效理念](https://medium.com/%E8%BB%9F%E9%AB%94%E4%B9%8B%E5%BF%83/%E7%B5%A6ml-engineer%E7%9A%84mlops%E7%B0%A1%E8%BF%B0-%E6%8C%81%E7%BA%8C%E9%96%8B%E7%99%BC%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92service%E7%9A%84%E9%AB%98%E6%95%88%E7%90%86%E5%BF%B5-8bd552876299)
* [The Fundamentals Of MLOps – The Enabler Of Quality Outcomes In Production Environments](https://radiant.digital/the-fundamentals-of-mlops-the-enabler-of-quality-outcomes-in-production-environments/)
* [AI’s Biggest Struggle Yet — No Streamlined MLOps as a Service](https://ai.plainenglish.io/ai-biggest-struggle-yet-no-streamlined-mlops-as-a-service-a4e4b42422ae)