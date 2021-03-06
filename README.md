# Text to Image Synthesis using Skip-thought Vectors

**The code for this model has not been tested because of time constraints. All the steps have been given below to train/test the model. Feel free to create a pull request if anyone is interested in testing this model.**

## Description
This is a PyTorch implementation of the paper Generative Adversarial Text-to-Image Synthesis [http://arxiv.org/abs/1605.05396] using skip thought vectors for caption embedding. This implementation is based on DCGAN. Below is the model architecture where blue bars represent skip thought vector for the captions.

[Figure]
Image Source : Paper

## Setup and Installments
  * Python==3.6.6
  * PyTorch==0.4.0
  * TorchVision==0.2.1
  * Theano

## Dataset
  * This model can be trained on the flowers dataset. Download flower dataset from here[] and save the images in Data folder as Data/flowers.
  * Now download the corresponding captions from here[]. After extracting, copy the text_c10 folder and paste it in Data folder as Data/text_c10.

## Skip-Thought Model
  * Download the pretrained models and vocabulary for skip thought vectors as per the instructions given below. Save the downloaded files in Data/skipthoughts.

  * Some of the files are quite large(>2GB). So make sure there is enough space available.

  * Run below code to download skip thought model and all other required files
  python download_skipthought.py


## Usage
  * Data Pre-processing :
  ```shell
  $ python data_loader.py
  ```

  * Training Arguments:
     ```shell
     dataset : Dataset used. Default = flowers
     batch_size : Batch Size. Default = 1
     num_epochs : NUmber of epochs to train. Default = 200
     img_size : Size of the image. Default = 64
     z_dim : Latent variable dimension. Default = 100
     text_embedding_dim : Embedding dim of caption. Default = 4800
     reduced_text_dim : Reduced embedding dim of caption. Default = 1024
     learning_rate : Learning Rate. Default = 0.0002
     beta1 : Hyperparameter of the Adam optimizer. Default = 0.5
     beta2 : Hyperparameter of the Adam optimizer. Default = 0.999
     l1_coeff : Coefficient for the L1 Loss. Default = 50
     resume_epoch : Resume epoch to resume training. Default = 1
     ```
  * Train the model by running below code
     ```shell
      $ python main.py
     ```
  * Testing model by giving custom input text
     ```shell
  	  $ python predict.py --text="Input caption to be used to generate the image"
     ```
  	The generated image will be save to text directory inside Data folder as Data/Testing 

## Model key-points

  * Skip Thought is an efficient model used for sentence embedding and is based on the concept of word
  embedding (word2vec or Glove). It returns a numpy array of dimension 4800 in which the first 2400
  dimensions is the uni-skip model and the last 2400 dimensions is the bi-skip model. We use the combine
  -skip vectors as experimentally, they perform the best.

  * Text2Image model is a Generarive Adversarial Network based model which is built on top of the DCGAN.
  It consists of a Discriminator network and a Generator network.

  * Discriminator network not only classifies the images generated by the generate as a fake image but also those real images which do not correspond to the correct caption. In short, fake examples are categorized by following :
  Fake Image + Correct Caption
  False Image(Real Image) + Incorrect Caption

  * Images are 64 x 64 in dimension

## Generated Images
Following are some of the images generated by this model
[A table of few 5-6 images along with their captions]

## TODO
Implementation of the same using an autoencoder for sentence embedding


## References
  * Generative Adversarial Text-to-Image Synthesis - http://arxiv.org/abs/1605.05396
  * Tensorflow implementation - https://github.com/paarthneekhara/text-to-image
  * Skip-Thought Model - https://github.com/ryankiros/skip-thoughts


## License
MIT
