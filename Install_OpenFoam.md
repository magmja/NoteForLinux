# How to install Code_Aster

(ref: )

## OpenFoam v2006

- Source the bashrc, eg. if installed under the `~/OpenFOAM` directory

```
source ~/OpenFOAM/OpenFOAM-v2006/etc/bashrc
```

- Test the system readiness (optional, not supported for cross-compilation)

```shell
foamSystemCheck
```

- Compile OpenFOAM

```shell
./Allwmake -s -l
./Allwmake -j -s -q -l
```

- Post-compilation steps

- Open a new shell and source the OpenFOAM environment to see all changes (refer to top of page).
- Validate the build (not supported for cross-compilation) by running

```
foamInstallationTest
```

- Create the user `run` directory:

```
mkdir -p $FOAM_RUN
```

- Test the installation with a simple tutorial:

```
run
cp -r $FOAM_TUTORIALS/incompressible/simpleFoam/pitzDaily ./
cd pitzDaily
blockMesh
simpleFoam
```

## OpenFoam7

1. Add source:

   ```shell
   sudo sh -c "wget -O - https://dl.openfoam.org/gpg.key | apt-key add -"
   sudo add-apt-repository http://dl.openfoam.org/ubuntu
   ```

2. update 

   ```shell
   sudo apt-get update
   ```

3. Install

   ```shell
   sudo apt-get -y install openfoam7
   ```

4. User Configuration

   add the following to the end of  the file "~/.bashrc"

   ```alias of7="source /opt/openfoam7/etc/bashrc"```

Finish!