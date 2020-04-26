# ORB_SLAM2-PythonBindings
A python wrapper for ORB_SLAM2, which can be found at [https://github.com/raulmur/ORB_SLAM2](https://github.com/raulmur/ORB_SLAM2).
This is designed to work with the base version of ORB_SLAM2, with a couple of minimal API changes to access the system output.
It has been tested on ubuntu 14.04 and 16.04 and built against Python3, although it does not rely on any python3 features.

这个版本从 [mmajewsk/ORB_SLAM2-PythonBindings](https://github.com/mmajewsk/ORB_SLAM2-PythonBindings) fork 而来，仅进行了微调以便安装

## Installation

### Prerequesities 前置需求

- modified versions of  ORBSLAM2 source code

  更改的 ORBSLAM2 源码

- ORBSLAM2 compiliation dependencies ([Pangolin](https://github.com/stevenlovegrove/Pangolin), [Eigen](http://eigen.tuxfamily.org/), [OpenCV3](http://opencv.org/))

  ORBSLAM2 的依赖库 ([Pangolin](https://github.com/stevenlovegrove/Pangolin), [Eigen](http://eigen.tuxfamily.org/), [OpenCV3](http://opencv.org/))

- Boost, c++ and python components (python36)

  Boost 的 Python 组件 (在CMakeLists中硬编码python版本为3.6，替换见下文)

  Boost 的 c++ 组件 用于提供 `libboost_serialization` 以保存地图

- Numpy development headers (to represent images in python, automatically converted to cv::Mat)

  Numpy (c++) 库

### Setup

#### ORBSLAM2 部分
~~First, we need an additional API method from ORBSLAM to extract completed trajectories.~~
~~Apply the patch file "orbslam-changes.diff" to the ORBSLAM2 source, which should create an additional method and add some installation instructions to the end of CMakeLists.txt.~~
~~Build orbslam as normal, and then run `make install`. This will install the ORBSLAM2 headers and .so to /usr/local~~
~~(if an alternative installation directory is desired, specify it to cmake using `-DCMAKE_INSTALL_PREFIX=/your/desired/location`).~~

直接克隆修改后的 ORBSLAM2 (从 **[Alkaid-Benetnash/ORB_SLAM2](https://github.com/Alkaid-Benetnash/ORB_SLAM2)** 微调而来)

```
git clone git@github.com:233a344a455/ORB_SLAM2.git
```

再运行脚本编译安装

```
cd ORB_SLAM2
chmod +x build.sh
./build.sh
```

#### Python 接口部分

Return to the ORBSLAM-Python source, build and install it by running
```
mkdir build
cd build
cmake ..
make
make install
```
This will install the .so file to /usr/local/lib/python3.6/dist-packages, such that it should 
If you have changed the install location of ORBSLAM2, you need to indicate where it is installed using ``-DORB_SLAM2_DIR=/your/desired/location``,
which should be the same as the install prefix above (and contain 'include' and 'lib' folders).

Verify your installation by typing
```
python3
>>> import orbslam2
```
And there should be no errors.

#### Examples

ORBSLAM2's examples have been re-implemented in python in the examples folder.
Run them with the same parameters as the ORBSLAM examples, i.e.:
```
python3 orbslam_mono_kitti.py [PATH_TO_ORBSLAM]/Vocabulary/ORBvoc.txt [PATH_TO_ORBSLAM]/Examples/Monocular/KITTI00-02.yaml [PATH_TO_KITTI]/sequences/00/
```

#### Alternative Python Versions 使用其他的python版本

At the moment, CMakeLists is hard-coded to use python 3.6. If you wish to use a different version, simply change the boost component used (python36) to the desired version (say, python-27), on line 38 of CMakeLists.txt.
You will also need to change the install location on line 73 of CMakeLists.txt to your desired dist/site packages directory.

## License
This code is licensed under the BSD Simplified license, although it requires and links to ORB_SLAM2, which is available under the GPLv3 license

It uses pyboostcvconverter (https://github.com/Algomorph/pyboostcvconverter) by Gregory Kramida under the MIT licence (see pyboostcvconverter-LICENSE).

