---
tags:
  - definitions
  - glossary
custom-width: .nan
---
# Machine Learning
Machine learning is a branch of artificial intelligence that involves the development of algorithms and statistical models that enable computers to learn from and make predictions or decisions based on data. It focuses on building systems that can automatically improve and adapt their performance over time without being explicitly programmed.
# Bring Your Own Data (BYOD)
BYOD is a feature that allows users to bring in their own custom labeled datasets to [[LEIP Design]] to create a model in a few steps. Users can import their dataset, choose or create a model of their liking, and begin the training process.

The easiest method of BYOD is by choosing a recipe from our [[#Golden Recipes]]. Once a model is chosen/created and trained, users can begin to use [[LEIP Optimize]] to optimize and target their deployment hardware.
# Golden Recipes
Golden Recipes, found in [[LEIP Design]], are [[#Recipe|recipes]] that have been curated by us through hundreds of thousands of inferences worth of experiments on different model parameter variations **AND** target hardware. These Golden Recipes are known for good performance, whether they excel in power efficiency, inference speed, low memory footprint, model size, or a combination of these traits.

The GRDB Explorer can be accessed by visiting this [link](https://gtc.latentai.io/).
# Recipe
A recipe is a set of configurations encompassing both model and hardware settings that are ready-to-execute across LEIP. Recipes can be created through out [[Recipe Designer]], which is found in [[LEIP Design]]. The end result of a recipe is a compiled model that is ready to be deployed with our [[Latent Runtime Engine (LRE)]], found in [[LEIP Deploy]].
# Quantization
Quantization in machine learning is a technique used to reduce the precision of the numbers that represent the model parameters, such as weights and activations. The goal of quantization is to decrease the computational and memory requirements of a model, making it more efficient and faster, especially for deployment on resource-constrained devices like mobile phones or embedded systems.
# Calibration
In the context of quantization, calibration refers to the process of determining the appropriate scaling factors and ranges for quantizing the model’s weights and activations. This process is crucial to maintaining the model's accuracy after quantization.