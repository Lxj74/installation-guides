# Install PCL

We use the Point Coud Library (PCL) for 2D/3D image and point cloud processing. Official download page: [link](http://pointclouds.org/)

- First install [OpenNI2 & NiTE2](install-openni-nite.md) for Xtion Pro Live support.

## Install PCL 1.7.2-1+trusty6 with VTK 5.8.0-14.1ubuntu3 (Ubuntu 14.04)

For Trusty and similar versions, we need to add the jochen-sprickerhof PPA [[ref](https://launchpad.net/~v-launchpad-jochen-sprickerhof-de/+archive/ubuntu/pcl)], while VTK is available directly as part of `universe` [[ref](http://packages.ubuntu.com/source/trusty/vtk)].

```bash
sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
sudo apt update
sudo apt install libpcl-all libpcl-all-dev
sudo apt install libopenni-sensor-primesense0 # no pcl-tools here; and libopenni-sensor-pointclouds0 cannot be installed simultaneously.
```

## Install PCL 1.7.2-3~utopic1 with VTK (Ubuntu 14.10)

For Utopic and similar versions, we need to add the jochen-sprickerhof PPA [[ref](https://launchpad.net/~v-launchpad-jochen-sprickerhof-de/+archive/ubuntu/pcl)].

```bash
sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
sudo apt update
sudo apt install libpcl-dev
sudo apt install pcl-tools # no sensor here, but libopenni-sensor-primesense0 may be found elsewhere
```

## Install PCL 1.7.2-14build1 with VTK 6.2.0+dfsg1-10build1 (Ubuntu 16.04)

PCL is available directly as part of `universe` in modern Ubuntu distros [[ref](https://launchpad.net/ubuntu/+source/pcl)].

```bash
sudo apt install libpcl-dev  # depends: libvtk6-dev
```

Developers may find obscure `No rule to make target '/usr/lib/x86_64-linux-gnu/libproj.so'` errors in their PCL-dependent applications, this is due to a known bug. Workaround ([SO answer](https://stackoverflow.com/a/40034779)):

```bash
sudo apt install libproj-dev
```

Besides, remove a superfluous `vtkproj4` item from the list of PCL libraries in your CMake code:

```cmake
find_package(PCL 1.7) # you probably have this around somewhere

# add these lines afterwards
if(DEFINED PCL_LIBRARIES)
    list(REMOVE_ITEM PCL_LIBRARIES "vtkproj4")
endif()
```

See also [PointCloudLibrary/pcl#2406](https://github.com/PointCloudLibrary/pcl/issues/2406#issuecomment-428101801) (linker error in case new point types are added).

## Install PCL (From source)

Link: [install from source](http://pointclouds.org/documentation/tutorials/compiling_pcl_posix.php).

## Install PCL (For any distro with CUDA for KinFu)

No official ppa, install CUDA, then [install from source](http://pointclouds.org/documentation/tutorials/compiling_pcl_posix.php) setting additional flags to get `pcl_kinfu_largeScale`, `pcl_kinfu_largeScale_mesh_output`, `pcl_kinfu_largeScale_texture_output`.

See additional info [here](https://david-estevez.gitbooks.io/install-guides/content/01_pcl_cuda.html).
