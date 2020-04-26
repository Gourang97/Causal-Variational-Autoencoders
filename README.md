# Causal Modeling on Variational Autoencoder

## Authors 

[Farhanur Rahim Ansari](https://www.linkedin.com/in/farhanurrahimansari/), [Gourang Patel](https://www.linkedin.com/in/gourang-patel/), [Sarang Pande](https://www.linkedin.com/in/srngpande/), [Vidhey Oza](https://www.linkedin.com/in/vidheyoza/)

## Abstract

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium, sapiente ad eaque? Rerum distinctio, ratione aperiam! Quae, quaerat nihil illum tempora, nulla nemo, quidem doloribus sed fugit culpa saepe. Qui!

[See video abstract]()

## Theory 

### Variational Autoencoder

- Overview
![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/VAE.png)

- Flow
![Variational Autoencoder](https://github.com/Gourang97/CausalML_VAE/blob/master/fig/vae_2.jpg)

* Dimensionality reduction is the process of reducing the number of features that describe some data either by selecting only a subset of the initial features or by combining them into a reduced number new features. Hence they can be seen as an encoding problem too. 
* Autoencoders are neural network architectures composed of an encoder and a decoder and trained to reconstruct the input during the encoding-decoding process of the model. As a result, the encoder learns to reduce dimensionality without losing important information about the input. 

### Training & Optimization

The training has being done on Google Colab Platform on GPU resource.
The dataset was divied into the train and test data in the data Once the CVAE class functions are set up we can execute the train and evaluate fucntion. The optimum learning rate used is 1.0e-3 and num of epochs are kept to be 10. The optimizer used here is "ADAM", as it works best with the stochastic dataset, which is here in our case. We observe from the elbo plot that the training losses with the given learning rate changes minimally after the 10 epochs. We also find the test loss after every 5 epochs i.e the TEST_EPOCH_FREQUECY is set to 5, so as to make sure that the model is not overfitting or underfitting our dataset.

Once the training is completed we are also saving the trained model weights so as to ensure the resusability of our results. The results observed our significant to implement the interventions and conditioning as we observed that the Average Training Loss after 10 epochs are 16.1449 and the Average Test loss After 5 epochs are 23.3984.

Training and Loss Plot:
<br/>
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/training_model_loader.PNG" width="360" height="300">
&nbsp;
<img src="https://github.com/Gourang97/CausalML_VAE/blob/master/fig/elbo_plot_train.png" width="360" height="300">

* The code is made compatible for GPU for faster processing.
* The learned weights are saved to avoid training frequently to enhance development efficiency.

## How to explore this project

Navigate to [this page] to see our project directory. 

### Prerequisite libraries

```
matplotlib
numpy
tqdm
seaborn
torch
torchvision
pyro-ppl
pydrive
```

### How to run our code

[This](https://github.com/Gourang97/CausalML_VAE/blob/master/causal_vae_dsprites_Farhan.ipynb) is the main Jupyter notebook that contains the full implementation of Causal VAE with counterfactuals. 

The first section mainly deals with the setup of VAE as a supervised model. It loads the data from the [dSprites repository](https://github.com/deepmind/dsprites-dataset). For error-free working, ensure that you specify the correct path after cloning the repo into the `data` directory. The model is then trained and tested to verify its correct training. An alternative to manual training is to run the `Load weights` cell. 

The second section has the construction of the Structural Causal Model (SCM). To make sure the model was developed properly before performing causal operations, we run 2 sanity checks: generating single image and reconstructing it using sampling, and checking if the decoder is able to generate the image if the latents are changed. 

Then we move on to perform three causal operations: conditioning, interventions and counterfactual reasoning. 

## Sample Results 

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
