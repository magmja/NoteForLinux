# How to install Code_Aster

Ref: ([code_Aster official website](https://www.code-aster.org/spip.php?article272))

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
3. Config the Code_Aster install setting
   ```
   cd aster-full-src-13.6.0
   sed -i "s:PREFER_COMPILER\ =\ 'GNU':PREFER_COMPILER\ =\'GNU_without_MATH'\nMATHLIB=\ '/opt/OpenBLAS/lib/libopenblas.a':g" setup.cfg
   ```  
   Then Install Code_Aster:
   ```
   python setup.py install --prefix=/opt/aster144
   ```

4. 