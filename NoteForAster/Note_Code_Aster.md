# A note for learning Code_Aster

## Operator


1. DEBUT

The goal is to allocate the resources memory, dic and files. Concists of a set of orders starting with BEGINNING and ending in END.


2. INCLUDE

Inserting a succession of orders which will be carried out almost such as they are written. Only the results of the orders are exported in the principal command set, not the other objects.

3. LIRE_MAILLAGE

To create a grid by reading on a file. Product a structure of data of the type grid. 

4. AFFE_MODELE

To define the modelled phenomenon (mechanical, thermal or acoustic) and the type of finite elements.

This operator allows to affect modelings on whole part of the grid, which defines:
* degrees of freedom on the nodes
* types of finite elements on the meshs


5. AFFE_CARA_ELEM

To assign to elements of structure of the geometrical and material characteristics. The affected geometrical data are complementary to the data grid.

6. DEFI_MATERIAU

To define the behaviour or the parameters associated with tiredness, the damage, or the simplified methods.

7. AFFE_MATERIAU

To assign materials to the geometrical zones of a grid or a model. Up to 26 metrials on the same mesh.

8. AFFE_CHAR_MECA

The affected values do not depend on any parameter and are defined by actual values. 

9. DEFI_LIST_REEL

To create a strictly increasing list of realities. The list can be given "in extenso" by the user, or, it can be formed from under lists defined in "constant step".

10. IMPR_RESU(FORMAT `MED`)

To write the result of a calculation in a file with format MED. One describes the whole of the keywords of order IMPR_RESU concerning this format of exit only. 

11. CALC_CHAMP

To create or supplement one result by calculating fields by element or with the nodes (forced, deformations,..)

The following produced result either is created, or modified, i.e. the call to CALC_CHAMP is done in the following way:

resu = CALC_CHAMP

12. POST_RELEVE_T

To extract from the values of components of fields of sizes and to carry out calculations. The values are recorded on nodes, meshs, broken lines connecting of the nodes. 

13. IMPR_TABLE

To print the contents of one table in a file. The order makes it possible to print a subset of the table under various formats.

14. DYNA_NON_LINE

To calculate the dynamic evolution of a structure whose material or geometry has a nonlinear behaviour. They can be for example nonmaterial linearities (plasticity or of geometry (great displacements)).

The dynamic evolution can be studied in several successive work, by a continuation as from one moment already calculated, if a database were defined in the profile of study of the user.





