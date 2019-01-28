# Docking-The-inhibition-of-COX-2-by-CELEBREX

A Quick tutorial on the docking of a enzyme with a small molecule, though the use of the following software: 
1) ROSETTA-4 (Modelling software: https://www.rosettacommons.org/software)
2) Pyrosetta and PyrosettaTools (Graphical User Interface: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0066856)
3) PyMOL (a GUI and molecule visual aid: https://pymol.org/2/) 

and databases

-1) The Protein Data Bank archive (PDB: https://www.wwpdb.org/index)
-2) The Drugbank database (https://www.drugbank.ca/)

We will be covering the whole precess, from compilation to the analisys of the results.

**-----------------------------------------------------------------------------------------------------------------------------**

   **STEP-1: Compiling ROSETTA-4**
   
**-----------------------------------------------------------------------------------------------------------------------------**                                             
Ir order to run ROSETTA, you will need to compile it first. Go to Rosetta Commons website (https://www.rosettacommons.org/software) and apply for a free licence. You will get an e-mail with a link, a Username and a password. Once the download is finished, unpack the file by using the command:

                                   tar -xvzf rosetta[releasenumber].tar.gz
                                     
                                     
Once the .tar file finishes unpacking, you need to compile it.

1) Go  to Rosetta main dairectoy by: *cd rosetta/main/source


2) To compile Rosetta you need a C++ compiler. Rosetta developers typically use GCC or Clang. Rosetta uses SCons as a build system. While Scons is available as a separate download, the Rosetta download includes a version, which is the recommended version to use in compiling Rosetta.

3) Now you can build Rosetta using this general command line (make sure you are in the source folder)

                            ./scons.py -j <number_of_cores_to_use> mode=release bin

Where -j is the number of cores you wnat to use. This step may take a while, depending on the number of cores chosen.

**-----------------------------------------------------------------------------------------------------------------------------**

   **STEP-2: Compiling PyRosetta-4**
   
**-----------------------------------------------------------------------------------------------------------------------------**                                             



Note: Python 2.6 or better is required. Python 3 now works with the PyRosetta-4 version of PyRosetta.

In order to run PYROSETTA, you also need to compile it. Go to University of Washington website (https://els.comotion.uw.edu/) and apply for a free licence. You will get an e-mail with a link, a Username and a password. Once the download is finished, unpack the file by using the command:

                                  tar -vjxf PyRosetta-<version>.tar.bz2 
      
PyRosetta-4

    From the main PyRosetta directory, run python setup.py install

    Be aware that running PyRosetta is now different than for PyRosetta-3: See below.

    from rosetta import *
    from pyrosetta import *
    rosetta.init("-list -of -options")


