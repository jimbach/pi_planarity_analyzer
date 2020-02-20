# pi_planarity_analyzer

pi planarity analyzer is a program which enables the stacking analysis of pi systems, by defining a normal vector on each pi system and performing different analyzations with these vectors, as directional average or angle to distance correlation or visual plots of all normal vectors on all pi systems within VMD (see examples for the TCL script).

The python script can be called from command line by:



The atoms defining the pi system can be specified within the input .fcf file (see Handbuch (both english/german)) and the pictures for the definition of the atom numbers.

the basic structure of the .gro file needs to be in cluster structure, this means if you have a mixed system with more than 1 molecule type the molecules need to be sequenced within "clusters" in the .gro file, e.g. 3 donor molecules followed by 1 acceptor molecule and so on. The analysis can be applied for a gromos/gromacs .gro trajectory, where the time information needs to be stored in the header of the .gro file as:

MySystem  0.0
307840
    1THP1A   HC    1   3.066  15.865  16.869 -0.0760 -0.8612  3.8240
    1THP1A   CA    2   3.091  15.962  16.827 -0.0789  0.2241 -0.7041
    1THP1A    C    3   3.012  16.030  16.737 -0.5418  0.0754  0.4543
    1THP1A   HC    4   2.911  16.006  16.712  3.2132 -0.8468  3.0564
    1THP1A    C    5   3.069  16.152  16.702  0.0722  0.6128  0.9950
    1THP1A    C    6   3.196  16.170  16.754 -0.3342 -0.1039  0.1626
    1THP1A    S    7   3.239  16.045  16.867  0.5046  0.2593  0.1851
    1THP1A  CH2    8   2.986  16.254  16.622 -0.1224  0.4144  0.4403
    1THP1A  CH2    9   2.987  16.238  16.466 -0.7826 -0.4594 -0.6156
    ...
    

Where the "0.0" after MySystem denotes the time. If a single .gro file is analyzed a 0.0 dummy needs to be specified as the last entry in the header.

It is possible to perform multiple analyses by specifying keywords in the input control file (.fcf file)


This Script enables to calculate different quantaties for a .gro trajectory file. You can use the script out of the shell by:

analysis_per_frame input.gro input.fcf input.top starting_time ending_time

input.gro is the .gro trajectory, input.fcf a file which contains information which and how the calculations are done. Optional you can use a input.top, which is a topology-file, which is needed for center-of-mass calculations. You can also define start and ending times for which the calculations are done, note that in the current state you need a topology file to use start and ending times. you can use any dummy file for this. After specifying this you are good to go and can start the calculation. The output is appended onto the output files.

The Keywords are as follows (warning: the keywords in the handbuchdocumentation.pdf are deprecated, use the ones from README.md):

Vectors on a surface, where the vector is in the opposite direction as bending: NORMALVEC
Center of Masses, xyz-trajectory: COM_MOL
Correlation between vectors and distance: VEC_CORRELATION
See how planar a chain of C5 is: C5_PLANARITAET
Angle between C5-ring i -> i+1 and i+1 -> i+2: C5_P3HT_ANGLES
All keywords must be ended with END after definition of parameters.

EXAMPLES for .fcf files:

#------- COM EXAMPLE ------------

#format control file for analysis_per_frame
#calculates the center of mass for a molecule-type and writes
#it to xyz trajectory
#input: timestep, index of first atom in mol, atoms per mol, number of mol per cluster, atoms per cluster
#i.e. 1 386 118 3 740 :for 1 P3HT (386 atoms) followed by 3 DIPBI (each 118 atoms) (740 atoms per cluster)
#and so on every 1 timesteps (unit i.e. ps from .gro file)
COM_MOL
1 386 118 3 740
END


#------- VEC CORRELATION EXAMPLE ------------

#calculates the vector correlation for 2 vectors, which are defined by reference vectors
#input: timestep, id1, id2, id3, id4, id5, id6, atoms_in_clust, num_mol1_per_clust, atms_per_mol_1, startatom_mol_1, atms_to_skip_between_vec_calc, id_2_1, id_2_2, id_2_3, id_2_4, id_2_5, atms_to_skip_between_vec_calc, vectos_per_clust, atms_per_clust
# vectors are: id1 and id2, between them is the middle of the first molecule. id3 to id6 are the reference vectors to calculate the normal vector with respect to the center of the molecule.
#for the vectors see definition_of_normalvector and definition_of_normalvector_pisystem
# the id1 id2 .. id6 are the indices within the molecule, i.e. first atom in molecule = 1 see definition_of_normalvector_pisystem.png
# the id_2_1 id_2_2 .. id_2_5 are the indices within the molecule, i.e. first atom in molecule = 1 see definition_of_normalvector.png
# for 1 P3HT (386 atoms) followed by 3 DIPBI (each 118 atoms) (740 atoms per cluster)
VEC_CORRELATION
1 23 53 43 28 19 54 740 3 118 386 0 1 2 4 5 6 12 32 740
END



If you have questions on how to run the program please feel free to contact me :)