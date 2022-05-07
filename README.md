# A-brief-introduction-to-autoencoders

# ***AutoEncoders***
AutoEncoder is an ***unsupervised Artificial Neural Network*** that attempts to encode the data by compressing it into a lower dimension (*bottleneck layer*), and than decoding the data to reconstruct the original input.

In AutoEncoders is important that the number of input must be equal to the numner of output.
![encoder-decoder](https://user-images.githubusercontent.com/72698188/167250361-97c07bfb-0497-4824-888f-282429aa4227.png)

- ***Encoder***: function $e$ that compresses the input into a *latent-space* representation. $e(x)$
- ***Decoder***: function $d$ that reconstruct the input from the *latent-space* representation. $d(e(x))$


Dimensionality reduction can then be interpreted as data compression where the encoder compress the data (from the initial space to the *encoded space*, also called *latent space*) whereas the decoder decompress them.

## ***Dimensionality reduction***

Dimensionality reduction is the process of reducing the number of features that describe some data. This reduction is done either by selection (only some existing features are conserved) or by extraction (a reduced number of new features are created based on the old features) and can be useful in many situations that require low dimensional data (data visualisation, data storage, heavy computation…)

So we are looking for the pair of encoder/decoder that keeps the ***maximum of information when encoding*** and, so, has the ***minimum of reconstruction error when decoding***.

Dimensionality reduction with no reconstruction loss often comes with a price: the lack of interpretable and exploitable structures in the latent space (***lack of regularity***). Second, most of the time the final purpose of dimensionality reduction is not to only reduce the number of dimensions of the data but to reduce this number of dimensions **while keeping the major part of the data structure information in the reduced representations**. For these two reasons, the dimension of the latent space and the “depth” of autoencoders (that define degree and quality of compression) have to be carefully controlled and adjusted depending on the final purpose of the dimensionality reduction.

![reducint dimentionality](https://user-images.githubusercontent.com/72698188/167250386-8ccc5424-bf45-4e85-8a99-e516c8b4c370.png)

## **Variational Autoencoders VAE**
Up to now, we have discussed dimensionality reduction problem and introduce autoencoders that are encoder-decoder architectures that can be trained by gradient descent.


### ***Limitations of autoencoders for content generation***
Once the autoencoder has been trained, we have both an encoder and a decoder but still no real way to produce any new content. We could be tempted to think that, if the latent space is regular enough (well “organized” by the encoder during the training process), we could take a point randomly from that latent space and decode it to get a new content.

However, the regularity of the latent space for autoencoders is a difficult point that depends on the ***lack of regularity***. The high degree of freedom of the autoencoder that makes possible to encode and decode with no information loss (despite the low dimensionality of the latent space) leads to a ***severe overfitting***.

***The autoencoder is solely trained to encode and decode with as few loss as possible, no matter how the latent space is organised.***


###***Definition of variational autoencoders***
One possible solution to obtain such regularity is to introduce explicit regularisation during the training process. ***A variational autoencoder can be defined as being an autoencoder whose training is regularised to avoid overfitting and ensure that the latent space has good properties that enable generative process.***

Just as a standard autoencoder, a variational autoencoder is an architecture composed of both an encoder and a decoder and that is trained to minimise the reconstruction error between the encoded-decoded. However, in order to introduce some regularisation of the latent space, we proceed to a slight modification of the encoding-decoding process: ***instead of encoding an input as a single point, we encode it as a distribution over the latent space.***

![VAE](https://user-images.githubusercontent.com/72698188/167250403-2a32b139-8b1e-4644-81ca-4d816773f02f.png)

In practice, the encoded distributions are chosen to be normal so that the encoder can be trained to return the mean and the covariance matrix that describe these Gaussians. The reason why an input is encoded as a Gaussian distribution with some variance instead of a single point is that it makes possible to express very naturally the latent space regularisation.



The loss function that is minimised when training a ***VAE*** is composed of a “*reconstruction term*” (on the final layer), that tends to make the encoding-decoding scheme as performant as possible, and a “*regularisation term*” (on the latent layer), that tends to regularise the organisation of the latent space. That regularisation term is expressed as the ***Kulback-Leibler divergence*** between the returned distribution and a standard Gaussian.

![Immagine 2022-05-07 122955](https://user-images.githubusercontent.com/72698188/167250507-f302449c-674a-45cb-93c2-1ef31ecca126.png)


![VAE schema](https://user-images.githubusercontent.com/72698188/167250434-be35cf3f-394f-4e6d-a03d-dc9a1149577d.png)

# ***References***

[`Semantic Hashing,Ruslan Salakhutdinov, Geoffrey Hinton`](http://www.utstat.toronto.edu/~rsalakhu/papers/semantic_final.pdf)

[`Intro to Autoencoders in TensorFlow`](https://www.tensorflow.org/tutorials/generative/autoencoder)

[`Understanding Variational Autoencoders (VAEs)`](https://towardsdatascience.com/understanding-variational-autoencoders-vaes-f70510919f73)



