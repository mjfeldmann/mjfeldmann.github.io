---
layout: post
title:  "Hello World!"
date:   2020-02-17 17:49:00
categories: blog
permalink: /posts/ubbensReview/
---
Hello dear reader,

I am thinkin about adopting a paper review style format for this blog. This may extend to albums as I expand the old list of things that I am currently listening to and currently reading, see <a href="mjfeldmann.github.io">the homepage</a>. Also, I should mention that my style will likely be a bit "from the hip."

That being stated, I am going to start with Ubbens et al (2020) Latent Space Phenotyping: Automatic Image-Based Phenotyping for Treatment Studies. 

I was able to talk about this work with Jordan Ubbens (@jordanubbens) at Phenome2019 after his presentation on this work, because he replied to a Twitter message. I slipped into his DMs so-to-speak. IFF you are attending Phenome2020, I highly recommend the digital phenotyping workshop that Jordan is speaking at.

Anyways, I find this work fascinating because it is closely related to several projects that I am working on regarding fruit shape. Furthermore, there has recently been more references to "latent space phenotypes" (LSP) and as far as I can tell, that stems from this paper. At least it is the reference that Joseph Gage and I have used for this phrase. However, it is exactly the same as the "Cryptotype" coined by Dr. Daniel Chitwood. "We propose the term cryptotype to describe latent, multivariate phenotypes that maximize the separation of a priori classes" (Chitwood & Topp 2015).

What is a LSP? In this manuscript, Ubbens defined LSPs as "a broad family of techniques known as latent variable models. ... LSP instead constructs a latent representation that best discriminates between image sequences of control and treated samples of a plant population and then measures differences among individuals within the latent space to quantify ...the effect of the treatment. The key characteristic of LSP in comparison to existing image-based phenotyping methods is that the phenotype estimated using an image analysis pipeline is replaced with an abstract learned concept... inferred automatically from the image data using deep learning techniques." 

What this means is that LSPs don't have the same type of direct interpretation as height or width and thus they are challenging to describe outside of the context of the sample and it's relationship to all other samples. So, an LSP is any number or set of numbers that can be extracted from an image through any set of techniques. One interpretation of an image that clear makes the most sense in image-based phenotyping is that the image is simply a matrix of numbers, and we want describe the relationship between the values in that matrix. This is not a new interpretation, but reaching it really helped me recognize the huge value in getting high quality images with as little noise as possible as LSPs are first and foremost going to describe the most salient aspects of that image (e.g., those aspects that explain the most variance)

This is why I enjoy this paper so much. The authors use longitudinal Trt-ctrl experiments and encode a reduced space using a encode-decoder CNN. This type of network effectively projects a matrix so a much smaller parameter space and then attempts to decode that reduced space to reconstruct the original image. The goal is to minimize a loss function while maintaining accuracy in the decoding network (you want your encoding to represent your image uniquely) and using an appropriate number of neurons in your encoded representation. It doesn't help to drop from 10,000 to 1,000 parameters, but 10,000 to 10 actually become actionable and tractable.

However, the authors took a very interesting approach which allowed them to potentially maintain quite a few parameters in their encoded layer. The approach they took was to estimate the geodesic distance from starting point to end point in their longitudinal data for both treated plants and control plants. The geodesic distance is a good choice because it is forced to follow defined path through points (with 6 time points, there would be 5 paths) and each of 6 nodes would have some linear distance in multidimensional space to the subsequent node. The geodesic distance is then the sum of all of the relevant path lengths and is a single value. Brilliant.
