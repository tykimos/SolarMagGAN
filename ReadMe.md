
## Network architectures
---

Let Ck denote a Convolution-BatchNorm-ReLU layer with k filters. CDk denotes a a Convolution-BatchNormDropout-ReLU layer with a dropout rate of 50%. All convolutions are 4× 4 spatial filters applied with stride 2. Convolutions in the encoder, and in the discriminator, downsample by a factor of 2, whereas in the decoder they upsample by a factor of 2.

### Generator architectures
The encoder-decoder architecture consists of:
encoder:
C64-C128-C256-C512-C512-C512-C512-C512
decoder:
CD512-CD512-CD512-C512-C256-C128-C64

After the last layer in the decoder, a convolution is applied to map to the number of output channels (3 in general, except in colorization, where it is 2), followed by a Tanh function. As an exception to the above notation, BatchNorm
is not applied to the first C64 layer in the encoder.
All ReLUs in the encoder are leaky, with slope 0.2, while ReLUs in the decoder are not leaky.

The U-Net architecture is identical except with skip connections between each layer i in the encoder and layer n−i in the decoder, where n is the total number of layers. The skip connections concatenate activations from layer i to
layer n − i. This changes the number of channels in the decoder:
U-Net decoder:
CD512-CD1024-CD1024-C1024-C1024-C512-C256-C128

### Discriminator architectures
The 70 × 70 discriminator architecture is:
C64-C128-C256-C512
After the last layer, a convolution is applied to map to a 1
dimensional output, followed by a Sigmoid function. As an exception to the above notation, BatchNorm is not applied to the first C64 layer. All ReLUs are leaky, with slope 0.2. All other discriminators follow the same basic architecture, with depth varied to modify the receptive field size:

## Training details
---
All networks were trained from scratch. Weights were initialized from a Gaussian distribution with mean 0 and standard deviation 0.02.
Batch iteration : 200000
Batch size : 1
Optimizer : Adam optimizer
Learning rate : 2e-4
beta_1 : 0.5
beta_2 : 0.999
epsilon : 1e-07
decay : 0.0
amsgrad : False
lambda : 100
BatchNormalization
momentum : 0.9
epsilon : 1.01e-5
