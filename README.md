# Docking-The-inhibition-of-COX-2-by-CELEBREX

A Quick tutorial on the docking of a enzyme with a small molecule, though the use of the following software: 
1) ROSETTA-4 (Modelling software: https://www.rosettacommons.org/software)
2) Pyrosetta and PyrosettaTools (Graphical User Interface: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0066856)
3) PyMOL (a GUI and molecule visual aid: https://pymol.org/2/) 
4) OpenBabel (https://sourceforge.net/projects/openbabel/).

and databases

1) The Protein Data Bank archive (PDB: https://www.rcsb.org)
2) The Drugbank database (https://www.drugbank.ca/)

We will be covering the whole precess, from compilation to the analisys of the results. Some of the information that can be found here can be found in the Rosetta Commons website, as the information made available there

**-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-1: Compiling ROSETTA-4
   
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

   ## STEP-2: Compiling PyRosetta-4
   
**-----------------------------------------------------------------------------------------------------------------------------**                                             



Note: Python 2.6 or better is required. Python 3 now works with the PyRosetta-4 version of PyRosetta.

In order to run PYROSETTA, you also need to compile it. Go to University of Washington website (https://els.comotion.uw.edu/) and apply for a free licence. You will get an e-mail with a link, a Username and a password. Once the download is finished, unpack the file by using the command:

                                    tar -vjxf PyRosetta-<version>.tar.bz2 
      

 From the main PyRosetta directory, run python  by:
 
                                              ./setup.py install
                                       
 **-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-3: Compiling PyrosettaTools
   
**-----------------------------------------------------------------------------------------------------------------------------** 

You, again, must compile and install  PyrosettaTools, in ordeer to do that you must:

Copy the code from pyrosetta/SetPyRosettaEnvironment.sh to your .bashrc (linux) or .bash_profile (mac). Give the full path where it says **PYROSETTA= Source** this. Useful to add a shortcut to pyrosetta/ipython.py in your profile.

The GUI code exists both in the rosetta source code at main/source/src/python/bindings/app/pyrosetta_toolkit and in the PyRosetta binary distributions in app/pyrosetta_toolkit If you have sourced SetPyRosettaEnvironment.sh, an alias is created to launch the GUI using the pyrosetta_toolkit command.


**-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-4: Downloading PyMOL
   
**-----------------------------------------------------------------------------------------------------------------------------** 

Pymol is rather mrore straightfoward than the previous packages, as it only requires you to adquire a free licence from the Pymol website (https://pymol.org/2/) and run the script that loads its GUI:

                                                  ./pymol
                                                  
The GUI is rather easy to user and intuitive. It looks like the picture below:                                                  
                                                  
![pymol](https://user-images.githubusercontent.com/39299850/51978247-9b83d480-2481-11e9-955f-99533e1ae137.png)


**-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-5- Downloading the PDB file and cleaning the molecule
   
**-----------------------------------------------------------------------------------------------------------------------------** 

Next, go to the Protein Data Bank archive (PDB: https://www.wwpdb.org/index) and download the Prostaglandin-endoperoxide synthase 2 PDB file. Load Pymol and open the COX-2 PDB file. It may come with a other molecules attached to it, (like water or inhibitors), so remove them by either deleting them manually. You might want to run the **clean_pdb.py** script that will allow you to strip the PDB of information other than the desired protein coordinates.
Our unrelaxed, cleaned COX-2 molecule is shown below:

![yes](https://user-images.githubusercontent.com/39299850/52065664-e92a3b00-256e-11e9-84c1-7eb1991c9f0c.png)


**-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-6- Preparing the receptor: Scoring, relaxing, scoring...
   
**-----------------------------------------------------------------------------------------------------------------------------** 

OK, now the enzyme is ready to be dealt with. First, we are going to run the **scoring function** from Rosetta to get an idea of how refined the structure we got is. Bear in mind that a refined structure of this size must have a score in the thousands (negative). We run the score calculation by:
                                     
    ~HOME/rosetta_src_2018.33.60351_bundle/main/source/bin/score_jd2.default.linuxgccrelease -s 1cx2v2.pdb -out:suffix _crystal_v2
    
  where:
- [x] _1cx2v2.pdb_, is your input file, the molecular coordinates.
- [x] _crystal_v2_ is the extension of the output file
- [x] _core_jd2.default.linuxgccrelease_ is the module of Rosetta that calculates the scores

You see right aways that the score is largely positive **(13562.228)** (_score_crystal.sc_ output file), pointing out to the conclusion that the structure needs  _"relaxing"_  from its original bound structure. You can do that by running  Rosetta's **relax** function, by using the following command:

    ~HOME/rosetta_src_2018.33.60351_bundle/main/source/bin/relax.default.linuxgccrelease -s 1cx2v2.pdb -out:suffix _relax
    
  An output file in the PDB format is going to be generated with the new more stable atomic coordinates for the enzyme (**1cx2v2_relax_0001.pdb**). A new score file is also going to be generated for that new "relaxed" geometry. The new relaxed score we obtain is **-5348.366** indicating a  much more stable configuration.
  
  **-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-7- Preparing the ligand: Adding hydrogens, generating confomers and .params file
   
**-----------------------------------------------------------------------------------------------------------------------------** 

Ligands can be found available on either The Protein Data Bank archive (PDB: https://www.rcsb.org) orThe Drugbank database (https://www.drugbank.ca/). Celebrex (4-5-(4-Methylphenyl)-3-(trifluoromethyl)pyrazol-1-yl benzenesulfonamide	C17H14F3N3O2S, https://en.wikipedia.org/wiki/Celecoxib), usually can be found in a *.sdf* format without any hydrogen atoms. In order to make it readable by Rosetta, you need, first, to add the hydorgen atoms. To do that, run Babel with the following command:

                                     babel -h celebrex.sdf celebrex_withH.sdf
                                    
 After the  hydrogen atoms are added, run the _molfile_to_params.py_ script, from the ~HOME/rosetta/main/source/scripts/python/public/ directory, with the command:
 
                ~HOME/rosetta/main/source/scripts/python/public/molfile_to_params.py/celebrex_withH.sdf
                
 The results is two confomers of celebrex in the _.pdb_ format (LG_0001.pdb and LG_0002.pdb) and the required .params file (LG.params).
 
 

**-----------------------------------------------------------------------------------------------------------------------------**

   ## STEP-8-Docking time!
   
**-----------------------------------------------------------------------------------------------------------------------------** 
    
 Now we are really close to the docking itself! Append the most stable confomer of the ligand (LG_0001.pdb and LG_0002.pdb) to the end of the .pdb file of the COX-2 enzyme. Remove aeverything else from this new pdb file, that we are going to call _1cx2new.pdb_. After appending the ligand coordinates to  the enzyme, move the two molecules togheter using pymol, placing the ligand near the enzyme alosteric site.
 Now, you can run ROSETTA's docking protocol, that will basiscally generate random translations and rotations through a Monte-Carlo algorithim, deciding to keep the perturbation or undo-it based on the energy score of this new configuration. To run the protocol you should used the command:

    ~HOME/rosetta/main/source/bin/docking_protocol.linuxgccrelease -s 1cx2new.pdb  -nstruct 1 -partners A_B -dock_pert 3 20 -spin -randomize1 -randomize2 -out:suffix _global_dock
    
where:
- [x] _-nstruct 1_, Number of times to process each input PDB
- [x] _-partners A_B_, Defines docking partners by ChainID
- [x] _-dock_pert 3 20_, Do a small perturbation with partner two
- [x] _-spin_, Spin a second docking partner around axes from center of mass of partner1 to partner2
- [x] _-randomize1 -randomize2_ Randomize the first and second docking partner.
- [x] _scoresdocking_protocol.linuxgccrelease_ Is the Rosetta's docking protocol

After executing the command, the docking starts. It takes a while and you are going to get some information on your terminal:

![image2](https://user-images.githubusercontent.com/39299850/52406465-ac59c900-2ac5-11e9-960b-967da991fe5b.png)


