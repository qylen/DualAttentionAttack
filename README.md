# DualAttentionAttack

This [paper](https://arxiv.org/abs/2103.01050) is accepted by CVPR'2021(Oral).

This paper proposed a dual attention supression attack approach, which exploits both the modle attention and human attention. Specifically, we distract the model attention to obtain a better attack ability, and moreover, we evade the human attention to help improving the naturalness.

#### Framework

<img src="media/framework.png" width="80%">

## Running

### before running

you need:

- dataset
  + The dataset can be generated by CARLA, which is a 3D virtual simulated environment and  a commonly used open-source simulator for autonomous driving research. Specifically, you can select different conditional parementers to dicide the angles, distances, and so on.
  + The dataset we generated can be accessed in [baidu pan](https://pan.baidu.com/s/1m2dACufqcRb-uL2JYGZxkA) (dual) and [Google Drive](https://drive.google.com/drive/folders/1vspvRxnZ3shOV4kM5ELcO9-xztapBThS?usp=sharing).
  + unzip the masks.zip and phy_attack.zip in the `src/data`.
- 3d object `.obj`  and texture file `.mtl` (eg. `src/audi_et_te.obj` and `src/audi_et_te.mtl`)
- face id list `.txt` which need to be trained (eg. `src/all_faces.txt`)
- seed content texture and edge mask texture
- Requirements:
  - pytorch: 1.4.0
  - neural_render: 1.1.3

### training

```shell
python train.py --datapath=[path to dataset] --content=[path to seed content] --canny=[path to edge mask]
```

results will be stored in `src/logs/`, include:

- output images
- `loss.txt`
- `texture.npy`  the trained texture file

### testing

```shell
python test.py --texture=[path to texture]
```

results will be stored in `src/acc.txt`

while the requirement is:
-python:3.6.2
-pytorch:1.4
-neural_render: which is in the src/neural_renderer, don't install the version in the pip git or original git. In the train.py ,add this code:
-sys.path.append(".../src/neural_renderer")
-chainer:6.7.0
-my cuda version is 10.1,so I install the cudatoolkit 10.1
-cupy:6.7.0(cupy-cuda101=6.7.0)
-numpy:1.14.0
