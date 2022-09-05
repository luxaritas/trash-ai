---
title: 'Trash AI: A Web GUI for Serverless Computer Vision Analysis of Images of Trash'
tags:
  - tensorflow.js
  - IndexDB
  - Plastic Pollution
  - Trash
  - Litter
  - AI
  - Image Classification
  - Serverless
authors:
  - name: Win Cowger
    orcid: 0000-0001-9226-3104
    affiliation: 1 # (Multiple affiliations must be quoted)
  - name: Steven Hollingsworth
    corresponding: true # (This is how to denote the corresponding author)
    affiliation: 2
  - name: Day Fey
    affiliation: 2
  - name: Mary C Norris
    affiliation: 2
  - name: Walter Yu
    affiliation: 3
  - name: Kristiina Kerge
    affiliation: 4
  - name: Kris Haamer
    affiliation: 4
affiliations:
 - name: Moore Institute for Plastic Pollution Research, USA
   index: 1
 - name: Code for Sacramento, USA
   index: 2
 - name: California Department of Transportation, USA
   index: 3
 - nam: Let's Do It Foundation, Estonia
date: 1 September 2022
bibliography: paper.bib

---

# Summary

Although computer vision classification routines have been created for trash, they have not been accessible to most researchers due to the challenges in deploying the models. Trash AI is a web GUI (Graphical User Interface) for serverless computer vision classification of batch images with trash in them hosted at www.trashai.org. With a single batch upload and download, a user can automatically describe the types and quantities of trash in all of their images. 

# Statement of need

The trash in the environment is a widespread problem that is difficult to measure. Classical measurement techniques require surveyors with pen and paper to manually quantify every piece of trash at a site. This method is time-consuming. Scientists are actively trying to address this issue by using imaging to better understand the prevalence and distribution of trash in an efficient yet effective manner `[@Majchrowska:2022; @Proença:2020; @Moore:2020; @van Lieshout:2020; @WADE AI:2020; @Lynch:2018; @Wuu:2018; @Waterboards:2018]`. An app-based reporting of trash using cell phones, laptops, and other devices has been a valuable solution `[@Lynch:2018]`. Applications for AI in detecting trash currently include: images from bridges `[@van Lieshout:2020]`, drone imaging `[@Moore:2020]`, cameras on street sweepers `[@Waterboards:2018]`, and cell phone app based reporting of trash `[@Lynch:2018]`. Although there are many artificial intelligence algorithms developed for trash classification, none are readily accessible to the average data scientist. The primary limitation is that artificial intelligence (AI) algorithms are primarily run through programming languages (not graphic user interfaces), difficult to deploy without AI expertise, and often live on a server (which costs money to host). New developments in browser-side AI (e.g. tensorflow.js) and serverless architecture (e.g. AWS Lambda) have created the opportunity to have browser-side artificial intelligence in a web GUI alleviating both obstacles. We present Trash AI, an open source service for making computer vision available to anyone with a web browser and images of trash. 

# Example
 Video
 Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% }

# Method

## Workflow Overview
Trash AI is trained on the [TACO dataset](http://tacodataset.org/) using [YOLO 5](pytorch.org). Trash AI stores images in [IndexDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) to keep the data primarily browser side and uses [tensorflow.js](https://www.tensorflow.org/js) to keep analysis browser side too. When images are uploaded to the browser, Trash AI provides the prediction of the model as a graphical output. The raw data from the model and labeled images can be downloaded in a batch download to expedite analyses. Any data uploaded to the platform is automatically saved to an [S3 bucket](https://aws.amazon.com/s3/) which we can use to improve the model over time.

## AI Training
The AI model was developed starting with the TACO dataset which was available with a complimentary Jupyter Notebook on Kaggle (https://www.kaggle.com/datasets/kneroma/tacotrashdataset). An example notebook was referenced which used the default YOLO v5 model `[@Jocher:2020]` as the basic model to begin transfer learning. Next, transfer learning was completed using the entire TACO dataset to import the image classes and annotations in the YOLO v5 model.

## Limitations
From our experience, the accuracy of the model varies depending on the quality of the images and their context/background. Trash is a nuanced classification because the same object in different settings will not be considered trash (e.g. a drink bottle on someone's desk vs in the forest laying on the ground). This and other complexities to trash classification make a general trash AI a challenging (yet worthwhile) long term endeavor. The algorithm is primarily trained on single pieces of trash in the image with the trash laying on the ground and the model will likely excel for that use case currently.

# Availability
Trash AI is hosted on the web at www.trashai.org. The source code is [available on github](https://github.com/code4sac/trash-ai) with an [MIT license](https://mit-license.org/). The source code can be run offline on any machine that can install [Docker and Docker-compose](www.docker.com). [Documentation](https://github.com/code4sac/trash-ai#ai-for-litter-detection-web-application) is maintained by Code for Sacramento on Github and will be updated with each release. The image datasets shared to the tool are in an S3 Bucket that needs to be reviewed before being shared with others due to security and moderation concerns but can be acquired by [contacting the repo maintaniers](https://github.com/code4sac/trash-ai/graphs/contributors). 

# Future Goals
This workflow is likely to be highly useful for a wide variety of computer vision applications and we hope that people reuse the code for applications beyond trash detection. We aim to increase the labeling of images by creating a user interface that allows users to improve the annotations that the model is currently predicting by manually restructuring the bounding boxes and relabeling the classes. We aim to work in collaboration with the TACO development team to improve our workflow integration to get the data that people share to our S3 bucket into the [TACO training dataset](http://tacodataset.org/) and trained model. Future models will expand the annotations to include the Trash Taxonomy `[@Hapich:2022]` classes and add an option to choose between other models besides the current model.

# Acknowledgements
Code for Sacramento led the development of the software tool. The Moore Institute advised on priorities and led the drafting of this manuscript. Let's Do It Foundation assisted with original products leading up to trash AI in the development of WADE AI. We acknowledge the work of the Code for Sacramento team, part of code for America, without whom this project would not have been possible and acknowledge the input of the California Water Monitoring Council Trash Monitoring Workgroup. We acknowledge financial support from McPike Zima Charitable Foundation.

# References