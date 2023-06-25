
## Bottleneck Adapters
Introduces feed-forward layers in each layer of the Transformer model.
These are a down projection W_down and an up projection W_up with a non-linearity in between. The most important configuration is the bottel neck size. Configurations differ on where in the transformer block the adapter layers are place.
- [[Adapters - Houlsby 2019]] places a feed forward layer both after the self attention and after the MLP inside the Tranformer block
- Adapters - Pfeiffer 2020 places only on adapter per transformer block; after the MLP
![[Pasted image 20230625173630.png]]
## Prefix Tuning
Introduces new parameters in the multi-head attention block in each Transformer layer. It prepend two vectors on  the key and value vectors of the attention head inputs. The most important configuration is the size of these vectors. In the paper [[Prefix-Tuning - Li and Liang 2021]] the authors do not train the vectors directory. Rather they are obtained by a bottleneck MLP.
![[Pasted image 20230625173643.png]]
## Compactor
Similar to a bottleneck adapter but it uses as PHM layer instead of a linear one. The PHM layer constructs its matrix from two smaller matices. Therefore further reducing the number of trainable parameters. 
- see [[Compactor - Mahabadi 2021]]

## LoRA
stands for Low-Rank Adaptation. It injects trainable low-rank decompostion matrives into the layers of a pre-trained model. The low-dimensional rank of the decomposition, is the most important hyperparameter. While, in principle, this reparameterization can be applied to any weight matrix in a model, the original paper only adapts the attention weights of the Transformer self-attention sub-layer with LoRA.
- see [[LoRA - Hu 2021]]

## (IA)^3
stands for _Infused Adapter by Inhibiting and Amplifying Inner Activations_. 
(IA)^3 introduces trainable vectors lW into different components of a Transformer model, which perform element-wise rescaling of inner model activations. For any model layer expressed as a matrix multiplication of the form h=Wx, it therefore performs an element-wise multiplication with l_W, such that:

h=l_W⊙Wx

The implementation of (IA)^3, class, are derived from the implementation of LoRA, with a few main modifications. First, (IA)^3 uses multiplicative composition of weights instead of additive composition, as in LoRA. Second, the added weights are not further decomposed into low-rank matrices.
- see [[(IA)^3 - Liu 2022]]
