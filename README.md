# Colab化改造中 本家参照のこと。


# [Sketch Simplification](https://esslab.jp/~ess/research/sketch/)

![Example result](/example_fig01_eisaku.png?raw=true "Example result of the provided model.")
Example result of a sketch simplification. Image copyrighted by Eisaku Kubonouchi ([@EISAKUSAKU](https://twitter.com/eisakusaku)) and only non-commercial research usage is allowed.

## Overview

This code provides pre-trained models used in the research papers:

```
   "Learning to Simplify: Fully Convolutional Networks for Rough Sketch Cleanup"
   Edgar Simo-Serra*, Satoshi Iizuka*, Kazuma Sasaki, Hiroshi Ishikawa (* equal contribution)
   ACM Transactions on Graphics (SIGGRAPH), 2016
```

and

```
   "Mastering Sketching: Adversarial Augmentation for Structured Prediction"
   Edgar Simo-Serra*, Satoshi Iizuka*, Hiroshi Ishikawa (* equal contribution)
   ACM Transactions on Graphics (TOG), 2018
```

See our [project page](https://esslab.jp/~ess/research/sketch_master/) for more detailed information.

## Dependencies

- [PyTorch](http://pytorch.org/) (version 0.4.1)
  [torchvision](http://pytorch.org/docs/master/torchvision/)
- [pillow](http://pillow.readthedocs.io/en/latest/index.html)

All packages should be part of a standard PyTorch install. For information on how to install PyTorch please refer to the [torch website](http://pytorch.org/).

## Usage

Before the first usage, the models have to be downloaded with:

```
bash download_models.sh
```

Next test the models with:

```
python simplify.py
```

You should see a file called `out.png` created with the output of the model.

Application options can be seen with:

```
python simplify.py --help
```

## Pencil Drawing Generation

Using the same interface it is possible to perform pencil drawing generation. In this case, the input should be a clean line drawing and not a rough sketch, and the line drawings can be generated by:

```
python simplify.py --img test_line.png --out out_rough.png --model model_pencil2.t7
```

This will generate a rough version of `test_line.png` as `out_rough.png`. By changing the model it is possible to change the type of rough sketch being generated.

## Models

- `model_mse.t7`: Model trained using only MSE loss (SIGGRAPH 2016 model).
- `model_gan.t7`: Model trained with MSE and GAN loss using both supervised and unsupervised training data (TOG 2018 model).
- `model_pencil1.t7`: Model for pencil drawing generation based on artist 1 (dirty and faded pencil lines).
- `model_pencil2.t7`: Model for pencil drawing generation based on artist 2 (clearer overlaid pencil lines).

## Reproducing Paper Figures

For replicability we include code to replicate the figures in the paper. After downloading the models you can run it with:

```
./figs.sh
```

This will convert the input images in `figs/` and save the output in `out/`. We note that there are small differences with the results in the paper due to hardware differences and small differences in the torch/pytorch implementations. Furthermore, results are shown without the post-processing mentioned in the notes at the bottom of this document.

Please note that we do not have the copyright for all these images and in general only non-commercial research usage is permitted. In particular, `fig16_eisaku.png`, `fig06_eisaku_robo.png`, `fig06_eisaku_joshi.png`, and `fig01_eisaku.png` are copyright by Eisaku Kubonoichi ([@EISAKUSAKU](https://twitter.com/eisakusaku)) and only non-commercial research usage is allowed.
The images`fig14_pepper.png` and `fig06_pepper.png` are licensed by David Revoy ([www.davidrevoy.com](http://www.davidrevoy.com/)) under CC-by 4.0.

## Training

Please see the [training readme](train/TRAIN.md).

## Notes

- Models are in Torch7 format and loaded using the PyTorch legacy code.
- This was developed and tested on various machines from late 2015 to end of 2016.
- Provided models are under a non-commercial creative commons license.
- Post-processing is not performed. You can perform it manually with `convert out.png bmp:- | mkbitmap - -t 0.3 -o - | potrace --svg --group -t 15 -o - > out.svg`.

## Citing

If you use these models please cite:

```
@Article{SimoSerraSIGGRAPH2016,
   author    = {Edgar Simo-Serra and Satoshi Iizuka and Kazuma Sasaki and Hiroshi Ishikawa},
   title     = {{Learning to Simplify: Fully Convolutional Networks for Rough Sketch Cleanup}},
   journal   = "ACM Transactions on Graphics (SIGGRAPH)",
   year      = 2016,
   volume    = 35,
   number    = 4,
}
```

and

```
@Article{SimoSerraTOG2018,
   author    = {Edgar Simo-Serra and Satoshi Iizuka and Hiroshi Ishikawa},
   title     = {{Mastering Sketching: Adversarial Augmentation for Structured Prediction}},
   journal   = "ACM Transactions on Graphics (TOG)",
   year      = 2018,
   volume    = 37,
   number    = 1,
}
```

## Acknowledgements

This work was partially supported by JST CREST Grant Number JPMJCR14D1 and JST ACT-I Grant Numbers JPMJPR16UD and JPMJPR16U3.

## License

This sketch simplification code is  freely available for free non-commercial
use, and may be redistributed under these conditions. Please, see the [license](/LICENSE)
for further details.

