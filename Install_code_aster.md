# How to install Code_Aster

Ref1: ([code_Aster official website](https://www.code-aster.org/spip.php?article272))

Ref2: ([A Blog by a Jananese](https://hitoricae.com/2020/05/16/installation-code_aster14-4-to-xubuntu20-04/))

1. Install prerequisites
``` shell
sudo apt-get install gcc g++ gfortran cmake python3 python3-dev python3-numpy tk tcl bison flex liblapack-dev libblas-dev libopenblas-dev libboost-python-dev libboost-numpy-dev zlib1g-dev nedit geany vim ddd

sudo apt-get install checkinstall openmpi-bin libx11-dev grace gettext libboost-all-dev swig
```

2. Download and install OpenBLAS 
   Official website for [OpenBLAS](https://www.openblas.net/)
   
   ```shell
   tar xfvz OpenBLAS-0.2.20.tar.gz
   cd OpenBLAS-0.2.20
   make NO_AFFINITY=1 USE_OPENMP=1
   make PREFIX=/opt/OpenBLAS install
   echo /opt/OpenBLAS/lib | sudo tee -a /etc/ld.so.conf.d/openblas.conf
   sudo ldconfig
   ```
   
3. Configure the Code_Aster install setting
   
   Change the compiler in file "setup.cfg", line 37:
   
   ```
   PREFER_COMPILER = 'GNU_without_MATH'
   MATHLIB='/opt/OpenBLAS/lib/libopenblas.a'
   ```
   Then Install Code_Aster:	
   
   ``` python3 setup.py install --prefix=/opt/aster144```
   
    After the build complete, to make host file for parallel calculation.
   
   ``` echo "$HOSTNAME cpu=$(cat /proc/cpuinfo | grep processor | wc -l)" > /opt/aster/etc/codeaster/mpi_hostfile```
   
4. 

