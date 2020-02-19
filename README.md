# pi_planarity_analyzer

pi planarity analyzer is a program which enables the stacking analysis of pi systems, by defining a normal vector on each pi system and performing different analyzations with these vectors, as directional average or angle to distance correlation or visual plots of all normal vectors on all pi systems within VMD (see examples for the TCL script).

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

If you have questions on how to run the program please feel free to contact me :)