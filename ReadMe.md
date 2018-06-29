
## Network architectures

### Generator architectures

The generator is consist of the encoder-decoder architecture:

encoder:

1. Conv2D(filers = 64, strides = 2), LeakyReLu(slope = 0.2)
2. Conv2D(filers = 128, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
3. Conv2D(filers = 256, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
4. Conv2D(filers = 512, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
5. Conv2D(filers = 512, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
6. Conv2D(filers = 512, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
7. Conv2D(filers = 512, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
8. Conv2D(filers = 512, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
9. Conv2D(filers = 512, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
10. Conv2D(filers = 512, strides = 2), ReLu

decoder:

1. Conv2DTranspose(filter = 512, strides = 2), BatchNorm, Dropout(rate = 0.5), ReLU
2. Conv2DTranspose(filter = 512, strides = 2), BatchNorm, Dropout(rate = 0.5), ReLU
3. Conv2DTranspose(filter = 512, strides = 2), BatchNorm, Dropout(rate = 0.5), ReLU
4. Conv2DTranspose(filter = 512, strides = 2), BatchNorm, ReLU
5. Conv2DTranspose(filter = 512, strides = 2), BatchNorm, ReLU
6. Conv2DTranspose(filter = 512, strides = 2), BatchNorm, ReLU
7. Conv2DTranspose(filter = 256, strides = 2), BatchNorm, ReLU
8. Conv2DTranspose(filter = 128, strides = 2), BatchNorm, ReLU
9. Conv2DTranspose(filter = 64, strides = 2), BatchNorm, ReLU
10. Conv2DTranspose(filter = 1, strides = 2), Tanh

Also, the generator has skip-connections between layers of the encoder and layers of the decoder like the U-Net architecture. 

skip-connection:

* encoder 1st layer - decoder 10th layer
* encoder 2nd layer - decoder 9th layer
* encoder 3rd layer - decoder 8th layer
* encoder 4th layer - decoder 7th layer
* encoder 5th layer - decoder 6th layer
* encoder 6th layer - decoder 5th layer
* encoder 7th layer - decoder 4th layer
* encoder 8th layer - decoder 3rd layer
* encoder 9th layer - decoder 2nd layer

### Discriminator architectures

The discriminator architecture is described in the following notation:
* Conv2D(filers = 64, strides = 2), LeakyReLu(slope = 0.2)
* Conv2D(filers = 128, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
* Conv2D(filers = 256, strides = 2), BatchNorm, LeakyReLu(slope = 0.2)
* Conv2D(filers = 512, strides = 1), BatchNorm, LeakyReLu(slope = 0.2)
* Conv2D(filers = 1, strides = 1), Sigmoid

The receptive field size used in our discriminator is 126 x 126.

## Hyperparameter

#### Loss
* Lamba : 100

#### Batch

* Batch iteration : 200000
* Batch size : 1

#### Optimizer 
* Optimizer : Adam solver
* Learning rate : 0.0002
* momentum beta 1 parameter : 0.5
* momentum beta 2 parameter : 0.999
