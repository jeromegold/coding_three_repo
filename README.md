# Coding Three Project - Influencer GAN

https://github.com/jeromegold/coding_three_repo

**Overview**

The aim of the project was to use machine learning tools to generate an instagram image of an Instagram influencer and assess whether this generated image is
close to visually realistic and potentially could be used for advertiisng/marketing purposes.

**Overall Result**

The attempt/hypothesis failed. The reasons will be discussed further.

**References**

A reference list is porivded at the end of the doucment and the Jupyter notebooks are referenced accordingly.

**Video Location**

https://youtu.be/Kn7cMbV5Upo
-----------------------------------------------------------------------------------------------------

**Introduction:**

The image generator DALL-E has been in the news lately ("From Trump Nevermind babies to deep fakes: DALL-E and the ethics of AI art", The Guardian 18.6.2022). Opinions tend to vary regarding the use cases and benefit of DALL-E to society. However, it is generally agreed that the images are impressive ("Give this AI a few words of description and it produces a stunning image – but is it art?", The Conversation, 10.6.2022).

I wondered whether image generation could be used for advertising/marketing purposes.

The aim of this project was to test this idea in the form of a generated Instagram influencer.

**Background**

Image generation is one area that has benefitted from improved techniques in machine learning. Relatively recently, in 2014, the seminal paper "Generative Adversarial Nets" was published by Goodfellow et al.

Since the first description of a Generative Adversarial Network (GAN), the use of GANs has increased. Websites such as https://this-person-does-not-exist.com/en demonstrate what can be achieved with image generation.

One area that extensively uses images is advertising and marketing. And Instagram is a platform used by influencers to generate income.  

A question I asked was whether generative techniques can be used to generate Instagram images similar to those posted by influencers.

**Method**

*Scraping images from instagram*

I investigated a few ways to scrape for Instagram images. There are python packages available such as insta-scrape (https://pypi.org/project/insta-scrape/) and instagram-scraper (https://pypi.org/project/instagram-scraper/).

The issue I found with these packages is that they are built by third parties and while useful, they are somewhat limited - eg might be good at extracting text but not as useful at extracting images. There are also limitations on the Instagram API re: how many images can be returned from one call. It might be as few as 12.

Rather than use an API I settled on webscraping using code modified from a web post (see reference 3 below). This used Selenium in the background. This was quite uncomplicated. The idea was to search for image files from within the html and these were downloaded.

When scraping, the main issue involved is the way Instagram loads images onto a website. Even if a user has 3000 images in their feed, Instagram only loads approximately 20 rows x 3 images. Therefore on each call only approximately 60 - 70 images are downloaded.

This could probably be automated to scroll through the entire feed but I performed this manually and downloaded a little over 1000 Instagram images of influencers.

I haven't posted the images to the Github repo but are available if necessary and can email them through.

*Custom Dataset*

My dataset consisted of 1000 Istagram images of influencers.

*Selecting a generative method*

The Keras site (https://keras.io/examples/) contains a number of GANs useful for various generative tasks. There is CycleGan, PixelCNN, and DeepDream among others.

There are other options as well to generate images such as Autoencoders.

**DCGAN**
I initially settled on using some code from Keras - DCGAN to Generate Face Images (https://keras.io/examples/generative/dcgan_overriding_train_step/). This was authored by fchollet and modified last in 2021.

Due to poor image generation, which will be discussed later, some research led me to StyleGan-ADA. In 2020 NVIDIA developed a GAN that could be trained on very few images - approximately 5000 images could get a reasonable result compared to the 50,000 - 100,000 required for other GANs.

**StyleGAN-ADA**
The implementation for StyleGAN used pytorch. Keras provides a code example for Jupyter notebooks.
https://keras.io/examples/generative/gan_ada/. I wasn't able to implement this, primarily because the loading of my custom dataset wouldn't work fully with the model. The model would start to train but then would fail at the end of the first epoch. The implentation provided by Keras used a dataset from Tensorflow and used the tfds.load call to download the images from Tensorflow.

**StyleGAN for faces**

I attempted to use StyleGAN for faces (https://keras.io/examples/generative/stylegan/) but also ran into some difficulties with model training.

**Results and Discussion**

As mentioned the images generated by DCGAN after 120 epochs were poor and didn't come close to resembling any of the Instagram images in the dataset. The primary reason I suspect is the size of the dataset. The GAN requires tens of thousands of images.

**Conclusion**

In summary, I see image generation being used increasingly frequently and this will impact advertising and marketing
and other industries as well. My attempt to generate an Instagram influencer image did not succeed but I learnt about various GANs and their limitations during the process.

Most of all I have learnt data preprocessing can be a stumbling block.

References:

1. StyleGan-ADA implementation https://keras.io/examples/generative/gan_ada/
2. DCGAN implementationw https://keras.io/examples/generative/dcgan_overriding_train_step/ authored by fchollet
3. Webscraping Instagram using Selenium https://towardsdev.com/web-scrapping-instagram-with-python-selenium-11229e1b075
4. Instagram
5. AI in Media lecture notes UAL
6. Goodfellow, I, et al. Generative Adversarial Nets https://arxiv.org/pdf/1406.2661.pdf
7. StyleGan for faces implementation https://keras.io/examples/generative/stylegan/
