# Causal Modeling with Variational Autoencoder
This project aims to train an variational autoencoder using Deepmind's dSprites dataset.

## Introduction
The objective of this project is to detect whether there's a deep causal relationship between the 6 ground truth independent factors that aggregately determine a dSprite image. 

## Dataset
dSprites is a dataset of sprites, which are 2D shapes procedurally generated from 6 ground truth independent "factors." These factors are color, shape, scale, rotation, x and y positions of a sprite.

All possible combinations of these variables are present exactly once, generating N = 737280 total images.

Factors and their values:

* Shape: 3 values {square, ellipse, heart} <br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Sha_1.png" width="120" height="120"><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Sha_2.png" width="120" height="120">
* Scale: 6 values linearly spaced in (0.5, 1) <br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Sca_1.png" width="120" height="120"><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Sca_2.png" width="120" height="120">
* Orientation: 40 values in (0, 2 π )<br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Or_1.png" width="120" height="120"><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Or_2.png" width="120" height="120">
* Position X: 32 values in (0, 1)<br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Pos_X_1.png" width="120" height="120"><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Pox_X_2.png" width="120" height="120">
* Position Y: 32 values in (0, 1)<br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Pos_Y_1.png" width="120" height="120"><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/Pos_Y_2.png" width="120" height="120">

Further, the objective of any generative model is essentially to capture underlying data generative factors, the disentangled representation would mean a single latent unit being sensitive to variations in single generative factors

## What is Variational AutoEncoder

- Overview
![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/VAE.png)

- Flow
![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/vae_2.jpg)

* Dimensionality reduction is the process of reducing the number of features that describe some data (either by selecting only a subset of the initial features or by combining them into a reduced number new features) and, so, can be seen as an encoding process
* Autoencoders are neural networks architectures composed of both an encoder and a decoder that create a bottleneck to go through for data and that are trained to lose a minimal quantity of information during the encoding-decoding processthe Model

## Training the Model
The training has being done on Google Colab Platform on GPU resource.
The dataset was divied into the train and test data in the data_loaders fucntion. And the train and test data can be called using the generator functions whenever required. Once the CVAE class functions are set up we can execute the train and evaluate fucntion. The optimum learning rate used is 1.0e-3 and num of epochs are kept to be 10. The optimizer used here is "ADAM", as it works best with the stochastic dataset, which is here in our case. We observe from the elbo plot that the training losses with the given learning rate changes minimally after the 10 epochs. We also find the test loss after every 5 epochs i.e the TEST_EPOCH_FREQUECY is set to 5, so as to make sure that the model is not overfitting or underfitting our dataset.

Once the training is completed we are also saving the trained model weights so as to ensure the resusability of our results. The results observed our significant to implement the interventions and conditioning as we observed that the Average Training Loss after 10 epochs are 16.1449 and the Average Test loss After 5 epochs are 23.3984.

Training and Elbow Plot:
<br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/training_model_loader.PNG" width="120" height="120">
<br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/elbo_plot_train.png" width="120" height="120">

## Optimization:
* The code is made compatible for GPU for faster processing.
* The learned weights are saved to avoid training frequently to enhance development efficiency.

## Results
* ### Variational Autoencoder
  * #### Reconstruction
    * Reconstructed Image using VAE 
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/original_reconstruction.png" width="400" height="200">
  * #### Reconstruction with manual change in latent factors
    * Original image with manual change in shape (Image1)
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/change_shape.png" width="400" height="200">
    * Original image with manual change in orientation to Image1 (Image2)
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/change_orientation.png" width="400" height="200">
* ### Structural Causal Model(SCM)
  * #### Reconstruction
    * Reconstructed image using SCM
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/scm_reconstruction.png" width="400" height="200">
  * #### Conditioning
    * Original image Conditioned on scale = 6
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/scm_conditioned.png" width="400" height="200">
  * #### Intervention
    * Original image intervened on PositionX = 32 and PositionY = 32
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/scm_intervene.png" width="400" height="200">
  * #### Counterfactual
    * Original image with image it would have been had shape = 3 (Heart)
    <br/><img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/counterfactual_shape.png" width="400" height="200">

## Applications
* Generating fake human faces. 
* Producing purely synthetic music.


