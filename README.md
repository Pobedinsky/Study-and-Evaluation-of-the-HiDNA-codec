# HiDNA Codec briefly explained

## Overview

The HiDNA codec is a sophisticated software system designed to compress images and store them in DNA sequences. Developed by the I3S laboratory in partnership with Pearcode Company for the JPEG DNA call of proposal, HiDNA leverages advanced neural network techniques to achieve high compression rates and efficient storage. The codec supports the encoding of images into DNA formats like FASTA and the reverse process of decoding these sequences back into images.

## Key Features

- **Neural Implicit Representation**: Utilizes an MLP (Multilayer Perceptron) to overfit and reconstruct the image based on latent spaces.
- **Autoregressive Model**: Estimates the distribution of quantized latent spaces to enhance entropy encoding.
- **Entropy Encoding**: Removes redundancy and optimizes the bit rate for storage efficiency.

## Architecture

### Components

1. **Synthesis Model - $f_\theta$** :
   - Based on COIN (Compression with Implicit Neural Representations) technology with modifications ([link to paper](https://arxiv.org/pdf/2103.03123)).
   - Hierarchical organization of latent spaces by resolution levels.
   - Quantization of 8x8 blocks with added uniform noise.
   - Back-propagation based on Mean Squared Error (MSE) to update latent spaces.
   - Upsampling of latent spaces using bicubic interpolation.

2. **Autoregressive Model - $f_{\psi}$** :
   - Predicts the distribution of the quantized latent space.
   - Integral for entropy encoding processes.

3. **Entropy Encoding**:
   - Quantized latent spaces are processed to remove redundancy and optimize storage.

### Step-by-Step Process

1. **Training Phase**:
   - Latent spaces are divided into 8x8 blocks and quantized.
   - Uniform noise is added before feeding into the synthesis module.
   - Distortions are calculated, and latent spaces are updated via back-propagation.
   - Autoregressive model is refined concurrently.

2. **Encoding**:
   - Images are encoded into small DNA sequences stored in a FASTA file.
   - The FASTA format represents nucleotide sequences using letters A, T, C, and G.

3. **Decoding**:
   - The header (GIO), autoregressive model parameters (ARMO), and synthesis model parameters (SynthO) are decoded sequentially.
   - Latent spaces are reconstructed to regenerate the original image.

## Data Serialization

The HiDNA codec organizes data into four types of oligos:
- **Global Information (GIO)**: Contains general info such as variable sizes and model parameters.
- **Autoregressive Model Parameters (ARMO)**: Stores parameters for the autoregressive model.
- **Synthesis Model Parameters (SynthO)**: Stores parameters for the synthesis model.
- **Latent Space (DO)**: Contains the quantized latent space data.

## Cost Function

The HiDNA codec employs a cost function to balance distortion and bit rate:

$J(\lambda)(ŷ) = D + \lambda R(ŷ)$
- $D$ : Distortion
- $R(ŷ)$: Rate of the quantized latent space
- $\lambda$: Weighting factor to balance distortion and rate

## Conclusion

The HiDNA codec is a cutting-edge solution for DNA-based image storage, offering a novel approach to digital data storage with high efficiency and robustness. By combining neural network models with DNA encoding techniques, HiDNA provides a powerful tool for managing the growing demands of digital data storage.

### References

- COIN: Compression with Implicit Neural Representations. [Link to paper](https://arxiv.org/pdf/2103.03123)
