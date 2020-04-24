# Causal Modeling with Variational Autoencoder
This project aims to train an variational autoencoder using Deepmind's dSprites dataset.

## Introduction
The objective of this project is to detect whether there's a deep causal relationship between the 6 ground truth independent factors that aggregately determine a dSprite image. 

## Dataset
dSprites is a dataset of sprites, which are 2D shapes procedurally generated from 6 ground truth independent "factors." These factors are color, shape, scale, rotation, x and y positions of a sprite.

All possible combinations of these variables are present exactly once, generating N = 737280 total images.

## What is Variational AutoEncoder

![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/VAE.png)

## Optimization:
* The code is made compatible for GPU for faster processing.
* The learned weights are saved to avoid training frequently to enhance development efficiency.

## Results
* Given an intervention, we were successfully able to recreate images with the other independent factors.

## Applications
* Our code can be used to perform image manipulation. For example, altering the monalisa portrait to change her expression to laughing, sad or angry.


