# Graph pooling based on Graph U-Net

<img src="https://github.com/bknyaz/graph_nn/blob/master/figs/fig.png" height="192">

My attempt to reproduce graph classification results from recent papers [[1](https://openreview.net/forum?id=HJePRoAct7), [2](https://arxiv.org/abs/1811.01287)] using Graph U-Net. So far, my results using Graph U-Net are worse than the baseline (GCN).
I also compare to a recent work on Multigraph GCN (MGCN) [[4](https://arxiv.org/abs/1811.09595)].

This repository contains all necessary data for the PROTEINS dataset. It can be found [here](https://ls11-www.cs.tu-dortmund.de/staff/morris/graphkerneldatasets) along with similar datasets.

The baseline model is Graph Convolutional Network (GCN) [[3](https://arxiv.org/abs/1609.02907)].
The decoder part of Graph U-Net is not implemented yet in our code, i.e. the only difference with the baseline is using pooling based on dropping nodes between graph convolution layers.

Hyperparameters are taken from [[2](https://arxiv.org/abs/1811.01287)], but learning rate decay and dropout is also applied. The readout layer (last pooling layer over nodes) is also simplified to just ```max``` pooling over nodes.
All hyperparameters are the same for the baseline, Graph U-Net and Multigraph GCN (MGCN).

Implementation is very basic without much optimization, so that it is easier to debug and play around with the code.

```
python graph_unet.py --model gcn  # to run baseline GCN
python graph_unet.py --model unet  # to run Graph U-Net
python graph_unet.py --model mgcn  # to run Multigraph GCN
```

| Model                 | PROTEINS          
| --------------------- |:-------------:|
| GCN [[3](https://arxiv.org/abs/1609.02907)]                                   | 76.09 ± 0.69 |
| GCN [[3](https://arxiv.org/abs/1609.02907)] + *A<sup>2</sup>*                 | 75.76 ± 0.54 |
| GCN [[3](https://arxiv.org/abs/1609.02907)] + *A<sup>2</sup>* + *2I*          | 75.35 ± 0.57 |
| Graph U-Net [[1](https://openreview.net/forum?id=HJePRoAct7), [2](https://arxiv.org/abs/1811.01287)]                           | 72.95 ± 1.09 |
| Graph U-Net [[1](https://openreview.net/forum?id=HJePRoAct7), [2](https://arxiv.org/abs/1811.01287)] + *A<sup>2</sup>*         | 74.18 ± 0.92 |
| Graph U-Net [[1](https://openreview.net/forum?id=HJePRoAct7), [2](https://arxiv.org/abs/1811.01287)] + *A<sup>2</sup>* + *2I*  | 73.56 ± 0.64 |
| Multigraph GCN (MGCN) [[4](https://arxiv.org/abs/1811.09595)]  | 76.94 ± 0.54 |

# Requirements

The code is tested on Ubuntu 16.04 with pytorch 0.4.1 and Python 3.6, but should work in other environments with pytorch >= 0.4. 

The [python file](graph_unet.py) and [jupyter notebook file](graph_unet.ipynb) contain essentially the same code, the notebook file is kept for debugging purposes.

# References

[1] [Anonymous, Graph U-Net, submitted to ICLR 2019](https://openreview.net/forum?id=HJePRoAct7)

[2] [Cătălina Cangea, Petar Veličković, Nikola Jovanović, Thomas Kipf, Pietro Liò, Towards Sparse Hierarchical Graph Classifiers, NIPS Workshop on Relational Representation Learning, 2018](https://arxiv.org/abs/1811.01287)

[3] [Thomas N. Kipf, Max Welling, Semi-Supervised Classification with Graph Convolutional Networks, ICLR 2017](https://arxiv.org/abs/1609.02907)

[4] [Boris Knyazev, Xiao Lin, Mohamed R. Amer, Graham W. Taylor, Spectral Multigraph Networks for Discovering and Fusing Relationships in Molecules, NIPS Workshop on Machine Learning for Molecules and Materials, 2018](https://arxiv.org/abs/1811.09595)
