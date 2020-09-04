# Fast_RNRR
This repository includes the source code of the paper "Quasi-Newton Solver for Robust Non-Rigid Registration", (CVPR2020), [https://arxiv.org/abs/2004.04322](https://arxiv.org/abs/2004.04322).

Authors: Yuxin Yao, [Bailin Deng](http://www.bdeng.me/), [Weiwei Xu](http://www.cad.zju.edu.cn/home/weiweixu/) and [Juyong Zhang](http://staff.ustc.edu.cn/~juyong/).

This code is protected under patent. It can be only used for research purposes. If you are interested in business purposes/for-profit use, please contact Juyong Zhang (the corresponding author, email: juyong@ustc.edu.cn).

## Dependencies
1. [OpenMesh](https://www.graphics.rwth-aachen.de/software/openmesh/)
2. [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)
3. [libigl](https://github.com/libigl/libigl)

## Compilation
The code is compiled using [CMake](https://cmake.org/) and tested on Ubuntu 16.04 (gcc5.4.0) and on Windows with Visual Studio 2015. An executable `Fast_RNRR` will be generated.

## Usage
The program is run with four input parameters:
```
$ Fast_RNRR <srcFile> <tarFile> <outPath> <landmarkFile>
```
1.`<srcFile>`: an input file storing the source mesh;

2.`<tarFile>`: an input file storing the target mesh or point cloud; 

3.`<outPath>`: an output file storing the path of registered source mesh; 

4.`<landmarkFile>`: an landmark file (nx2 matrix, first column includes the indexes in source file, second column includes the indexes in target file, each row is a pair correspondences separated by space).

`<landmarkFile>` can be ignored, our robust non-rigid registration method without landmarks will be used in this case.

### Notes

This code supports non-rigid registration from a triangle mesh to a mesh or a point cloud.

## Recently Updates (2020.9)

1. Simplify the code, just keep our method, delete the initialization operator of `SHOT` feature and `diffusion pruning`, you can also use [PCL](https://pointclouds.org/) to precompute initial correspondences if necessary. The old version move to the `src_cvpr` folder.
2. Change the calculation method of geodesic distance to locally using of [VTP method](https://github.com/YipengQin/VTP_source_code), in order to be more robust to unclosed mesh when constructing the sampling node graph.
3. Optional marking of points without correspondences, and exclusion of certain incorrect point pairs by distance and normal thresholds.

### Parameter choices
1. The weight parameters of `regularization term` and `rotation term` can be set in `paras.alpha` and `paras.beta` in `main.cpp` respectively. You can increase them to make the model more maintain the original characteristics, and decrease them to make deformed model closer to the target model. 
2. If you need to reject correspondences with a large difference between distance or normal when looking for the closest point, you can set the `paras.distance_threshold`  and `paras.normal_threshold` in `main.cpp`.


## Citation
Please cite the following papers if it helps your research:
```
@InProceedings{Yao_2020_CVPR,
    author = {Yao, Yuxin and Deng, Bailin and Xu, Weiwei and Zhang, Juyong},
    title = {Quasi-Newton Solver for Robust Non-Rigid Registration},
    booktitle = {IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month = {June},
    year = {2020}
}
```

## Acknowledgement
This work was supported by the National Natural Science Foundation of China (No. 61672481), and Youth Innovation Promotion Association CAS (No. 2018495).
