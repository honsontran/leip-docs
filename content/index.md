---
title: Welcome to LEIP
tags:
  - home
custom-width: .nan
---
> [!TIP] Tip
> Reading this page entirely from top to bottom is recommended. 

Hello! Welcome to the [[Latent AI Edge Inference Platform (LEIP)]].

This home page will serve to help you intuitively understand how to navigate and leverage [[What is LEIP?|LEIP]] to rapidly create highly performant AI models.

If you would like to schedule an evaluation of [[What is LEIP?|LEIP]], please contact us at support@latentai.com
# Before You Begin...
To keep things simple, [[LEIP]] is broken down into 3 products. You can use each of these products based on what tools you need to deploy your Machine Learning (ML) model.

1. [[Design]]
	* Easily create and train an ML model by [[Glossary#Bring Your Own Data (BYOD)|Bringing Your Own Data (BYOD)]]. This can be done by selecting from our curated [[Golden Recipes]], or create a recipe through [[Recipe Designer]].
2. [[Optimize]]
	* Easily apply software and hardware optimizations to your model for a chosen hardware deployment. No specific hardware optimization knowledge is needed.
	* Users can take advantage of [[LEIP Optimize]] whether they created a model from [[LEIP Design]], or if they have created one outside of [[LEIP]] (this path is also known as [[Bring Your Own Model (BYOM)]]).
3. [[Deploy]]
	* Install our [[Latent Runtime Engine (LRE)]] to manage and run your models created from [[LEIP Optimize]].
	* Utilize [[LRE Services]] to enable your model to report metrics and enhance security.
# Getting Started: Identifying Your Path
There are 2 paths to enter into [[What is LEIP?|LEIP]]. Your path will depend on which [[What is LEIP?|LEIP]] Products you will use to create your AI solution. The steps for each path are listed in order below.

If you're more of a visual person, [click this graph]() to see a high level overview of the paths.
## [[Glossary#Bring Your Own Data (BYOD)|Bring Your Own Data (BYOD)]]
1. Pre-requisites
	* A labeled dataset in [[COCO]] or [[PASCAL VOC]] format.
	* Don't know how to create a labeled dataset? Click [[here]].
3. [[Design]]
	* Create and train a model here, with the end result being a trained (and traced PyTorch) model.
4. [[Optimize]]
	* Use the trained model from [[Design]] in the optimization phase to [[Glossary#Quantization|quantize]] and target deployment hardware of your choosing.
5. [[Deploy]]
	* Install our [[Latent Runtime Engine (LRE)]] to manage and run your models created from [[LEIP Optimize]].
## [[Bring Your Own Model (BYOM)]]
1. Pre-requisites
	* A trained model from a popular ML framework (e.g., TensorFlow, Keras, PyTorch, etc.).
2. [[Optimize]]
	* Use your trained model in the optimization phase to [[Glossary#Quantization|quantize]] and target deployment hardware of your choosing.
3. [[Deploy]]
	* Install our [[Latent Runtime Engine (LRE)]] to manage and run your models created from [[LEIP Optimize]].
# Installing LEIP SDK & LRE

> [!NOTE]  Note
> The LEIP SDK consists of [[Optimize]] and [[Deploy]]. This is installed on your _development_ machine.
> 
> For deployment, you will install the [[Latent Runtime Engine (LRE)|LRE]] on your _deployment hardware_. The [[Latent Runtime Engine (LRE)|LRE]] is responsible for running the optimized model created from the SDK.

Once you've identified your [[What is LEIP?|LEIP]] path, check to see if you have all the prerequisites to run [[What is LEIP?|LEIP]] by visiting [[Installing Prerequisites]].

Once you have satisfied all prerequisites, refer to [[Installing LEIP SDK]].

After installation, you can browse and use our [[#Tutorials|tutorials]] below.

Once you have a model you're ready to deploy with, you can reference [[Installing LRE]] to install the runtime and deploy your model on your target hardware.
# Tutorials
Tutorials will be labeled with #BYOM or #BYOD depending on which path you choose.
* [[Getting Started with BYOD to Deployment]]
