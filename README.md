# FashionBlend: Diffusion Model

The project is based on a Diffusion Model which will create realistic images of a model wearing selected clothing. Users will input both the model image and the desired attire, and the system will combine them to produce an accurate depiction of the model in the chosen outfit.

## Variational Autoencoder (VAE)

The input clothes image goes through a Variational Autoencoder (VAE), which encodes the image into a lower-dimensional latent space while preserving its essential features. This latent representation captures the overall structure and content of the input clothes image.
Architecture of VAE(https://drive.google.com/file/d/1Zh90lKFvUY_Xfuhk1CkiWu8gKJI-p9w9/view?usp=sharing)
## CLIP

CLIP is a powerful model developed by OpenAI that learns joint representations of images and text. It can map images and their corresponding textual descriptions into a shared embedding space.

## U-Net Architecture

The latent vector from the VAE (representing the input clothes image) and the vector embedding from CLIP (representing the target model image) are then combined and passed as input to a U-Net architecture, which is well-suited for diffusion models. The U-Net's encoder-decoder structure, with skip connections and multi-scale processing, allows it to effectively map the high-dimensional data (images) to the latent space and reconstruct them coherently.

## Diffusion Model

Within the U-Net, the diffusion model's reverse process is conditioned on both the VAE's latent vector (capturing the clothes content) and the CLIP's vector embedding (describing the target model visual characteristics). The CLIP embedding and the latent vector are combined with time step information and fed into the diffusion model.

## Classifier-Free Guidance

The diffusion model then predicts the noise that needs to be removed at each time step, guiding the denoising process towards generating an image that aligns with both the latent vector (preserving the overall structure and content of the clothes) and the model image embedding (incorporating the desired visual characteristics of the target model).

This denoising process is facilitated by Classifier-Free Guidance, which involves training a single network as a mix of a conditioned and an unconditioned model. During training, the model randomly decides whether to use the conditioning information (model image embedding) or not. This way, the network learns to operate in both conditioned and unconditioned modes, effectively becoming a hybrid model.
Architecture of CFG(https://drive.google.com/file/d/1Eg9aig5cyoLLEDslb25gfjyC3CqF6Ynd/view?usp=sharing)
## Output

After the iterative denoising process, the final denoised latent vector is passed through the decoder part of the VAE, which reconstructs the output image from the latent representation. This output image should reflect the clothes from the input clothes image, fitted onto the target model represented by the model image input, combining the visual characteristics of both inputs.
Architecture(https://drive.google.com/file/d/1p0aP9DNbPFAIj55SjSKvq9IhYpeGAkQZ/view?usp=sharing)
