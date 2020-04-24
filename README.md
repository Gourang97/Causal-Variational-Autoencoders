# Causal Modeling with Variational Autoencoder
This project aims to train an variational autoencoder using Deepmind's dSprites dataset.

## Introduction
The objective of this project is to detect whether there's a deep causal relationship between the 6 ground truth independent factors that aggregately determine a dSprite image. 

## Dataset
dSprites is a dataset of sprites, which are 2D shapes procedurally generated from 6 ground truth independent "factors." These factors are color, shape, scale, rotation, x and y positions of a sprite.

All possible combinations of these variables are present exactly once, generating N = 737280 total images.

Factors and their values:

* Shape: 3 values {square, ellipse, heart} ![Shape](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Sha_1.png?v=4&s=50) ![Shape](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Sha_2.png)
* Scale: 6 values linearly spaced in (0.5, 1)
* Orientation: 40 values in (0, 2 π )
* Position X: 32 values in (0, 1)
* Position Y: 32 values in (0, 1)

Further, the objective of any generative model is essentially to capture underlying data generative factors, the disentangled representation would mean a single latent unit being sensitive to variations in single generative factors

## What is Variational AutoEncoder

- Overview
![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/VAE.png)

- Flow
![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/vae_2.jpg)

* Dimensionality reduction is the process of reducing the number of features that describe some data (either by selecting only a subset of the initial features or by combining them into a reduced number new features) and, so, can be seen as an encoding process
* Autoencoders are neural networks architectures composed of both an encoder and a decoder that create a bottleneck to go through for data and that are trained to lose a minimal quantity of information during the encoding-decoding process

## Optimization:
* The code is made compatible for GPU for faster processing.
* The learned weights are saved to avoid training frequently to enhance development efficiency.

## Results
* ### Variational Autoencoder
  * #### Reconstruction
    * Achieved good accuracy using VAE
    * <image>
  * #### Reconstruction with manual change in latent factors
    * Original image with manual change in shape (Image1)
    * <image>
    * Original image with manual change in orientation to Image1 (Image2)
    * <image>
* ### Structural Causal Model(SCM)
  * #### Reconstruction
  * #### Conditioning
  * #### Intervention
  * #### Counterfactual
    * Original image with image it would have been had shape been heart
    ![Counterfactual shape](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/counterfactual_shape.png)

## Applications
* Generating fake human faces. 
* Producing purely synthetic music.


