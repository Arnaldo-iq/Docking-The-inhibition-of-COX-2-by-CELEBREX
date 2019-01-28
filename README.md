# Docking-The-inhibition-of-COX-2-by-CELEBREX

A Quick tutorial on the docking of a enzyme with a small molecule, though the use of the following software: 
1) ROSETTA-4 (Modelling software: https://www.rosettacommons.org/software)
2) Pyrosetta and PyrosettaTools (Graphical User Interface: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0066856)
3) PyMOL (a GUI and molecule visual aid: https://pymol.org/2/) 

and databases

1) The Protein Data Bank archive (PDB: https://www.wwpdb.org/index)
2) The Drugbank database (https://www.drugbank.ca/)

We will be covering the whole precess, from compilation to the analisys of the results. Some of the information thatc an be found here can be found in the Rosetta Commons website, as the information made available there

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
      

 From the main PyRosetta directory, run python  by:
 
                                              ./setup.py install
                                       
 **-----------------------------------------------------------------------------------------------------------------------------**

   **STEP-3: Compiling PyrosettaTools**
   
**-----------------------------------------------------------------------------------------------------------------------------** 

You, again, must compile and install  PyrosettaTools, in ordeer to do that you must:

Copy the code from pyrosetta/SetPyRosettaEnvironment.sh to your .bashrc (linux) or .bash_profile (mac). Give the full path where it says PYROSETTA= Source this. Useful to add a shortcut to pyrosetta/ipython.py in your profile.

The GUI code exists both in the rosetta source code at main/source/src/python/bindings/app/pyrosetta_toolkit and in the PyRosetta binary distributions in app/pyrosetta_toolkit If you have sourced SetPyRosettaEnvironment.sh, an alias is created to launch the GUI using the pyrosetta_toolkit command.


**-----------------------------------------------------------------------------------------------------------------------------**

   **STEP-4: Downloading Pymol**
   
**-----------------------------------------------------------------------------------------------------------------------------** 

Pymol is rather mroe straightfoward than the previous packages, as it only requisres you to adquire a free licence from the Pymol website (https://pymol.org/2/) and run the script that loads its GUI:

                                                  ./pymol
