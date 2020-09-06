# A note for learning Code_Aster

Author: Magnus Aske Mjåtveit


(ref: [Documentation15](https://www.code-aster.org/V2/doc/default/en/index.php?man=commande))


## Operator

---

## 1. DEBUT

The goal is to allocate the resources memory, disk and files. Concists of a set of orders starting with BEGINNING and ending in END.

`DEBUT(PAR_LOT =`: 

`YES`:

The supervisor analyzes `all` orders before asking the execution of it.


`NOT`/`NON`:

After having analyzed `one` order the supervisor requires his execution then passes to the analysis (and execution) of the following order (treatment orders by order).  


`IGNORE_ALARM =`:


Allows the user to remove the posting of certain alarms in order to more easily identify other alarms which could appear. During the execution of the order `END`, one systematically displays a summary table of the alarms emitted during the execution (and the number of occurrences). The alarms ignored by the user are proceeded by ‘*’ to distinguish (and they appear even if they were not emitted).

---

## 2. INCLUDE

Inserting a succession of orders which will be carried out almost such as they are written. Only the results of the orders are exported in the principal command set, not the other objects.


`INCLUDE(UNIT=`: 


Logical unit of the file to be included. It is essential to explicitly assign this number to a file within the the interface `astk`. 

---

## 3. LIRE_MAILLAGE

To create a grid/mesh by reading on a file. Product a structure of data of the type grid. 

Unit 20 by defaults. 


---

## 4. AFFE_MODELE

To define the modelled phenomenon (mechanical, thermal or acoustic) and the type of finite elements.

This operator allows to affect modelings on whole part of the grid, which defines:
* degrees of freedom on the nodes
* types of finite elements on the meshs
  
`AFFE`:


Defines the entities of the grid/mesh and the types of elements which will be affected for them. 

* GROUP_MA: For each occurrence, one give a modeling. Assignment with a list of groups of meshs. 

* MODELISATION: Type of interpolation and discretization. Obligatory for each occurrence of the keyword factor `AFFE`. Defines in an objective way the type of affected element in a kind of mesh. 

* PHENOMENE: Obligatory for each occurrence of the keyword factor `AFFE`. Modelled physical phenomenon.

Note: the keyword `PHENOMENON` must have the same value for all the occurrences of the keyword factor `AFFE`. 

---

## 5. AFFE_CARA_ELEM

To assign to elements of structure of the geometrical and material characteristics. The affected geometrical data are complementary to the data grid.

`CABLE`:

Type of element. Allows to assign a constant section to the elements of the type cables or cable-pulley.

`GROUP_MA = `, Assignment with all the elements of the groups of meshs specified. 

* N_INIT: Allows to define the initial tension in the cable. 


* SECTION: Allows to define the surface of the cross section of the cable.


* `MODELE = Mo`: Assignment with all the elements of the groups of meshs specified.


---

## 6. DEFI_MATERIAU

To define the behaviour or the parameters associated with tiredness, the damage, or the simplified methods.

* EC_SUR_E: Operation of elasticity. Report of the modules to compression and traction. If the module of compression is zero, the total linear system with displacements can become singular. 

* ELAS_F: Definition of the constant linear elastic characteristics or functions.  

* E = yg : Young's modulus
* NU = naked : Poisson's ratio
* RHO = rho : Density



---

## 7. AFFE_MATERIAU

To define the variables of order (temperature, space, hydration, drying, corrosion,...)

To assign materials to the geometrical zones of a grid or a model. Up to 26 metrials on the same mesh.

* GROUP_MA: Indicate the whole of the meshs which will be affected
* MATER: Name of the material which one wants to affect. 
* MODELE: If this argument is used, it is checked that the meshs affected in the order are part of the model as well.

---

## 8. AFFE_CHAR_MECA

The affected values do not depend on any parameter and are defined by actual values. 

`AFFE_CHAR_MECA_F`:

The affected values are function of one or more parameters as a whole {X, Y, Z}

* PESANTEUR: apply a field of gravity to the model
* GROUP_MA: who specifies the meshs to which the field applies (this possibility, which does not have a physical direction
* FORCE_NODALE: The loading is affected on the nodes
* FX, FY, FZ: Values of the components of the nodal forces of the nodal moments applied to the specified nodes. These nodal forces will come to be superimposed on the nodal forces resulting, possibly, other loadings. Into axisymmetric, the values correspond to a sector of a radian (to divide the real loading by 2 pi)
* MODELE: types of elements affected on the grid
* DDL_IMPO: usable to impose on nodes, one or more values of degree of freedom
* GROUP_NO: The kinematic conditions are imposed on the nodes given by this keyword
* LIAISON: Allows to embed nodes directly, i.e. to force to zero the degrees of freedom of translation and rotation. The other degrees of freedom are not modified.
* ENCASTRE: "built in" 


---

## 9. DEFI_LIST_REEL

To create a strictly increasing list of realities. The list can be given "in extenso" by the user, or, it can be formed from under lists defined in "constant step".

* DEBUT: It is the first reality of the list of realities which one wants to build.
* INTERVALLE:
* JUSQU_A = : it is the end of the interval which one will cut out a constant step.
* PAS = step of division interval
* LIST_INST : produce a structure of data
* PAS_MINI : specify the step of minimal time

---


## 10. DEFI_LIST_INST

To define the list of moments of calculation, like its management for the iterative algorithms of
resolution.

* DEFI_LIST: produce a structure of data
* LIST_LIST: moment of calculation based on concept defined in `DEFI_LIST_REEL` (9.)

---
## 11. IMPR_RESU(FORMAT `MED`)

To write the result of a calculation in a file with format MED. One describes the whole of the keywords of order IMPR_RESU concerning this format of exit only. 

One can write with the choice in a file with format MED:
- a grid
- fields with the nodes
- fields with the elements.

* FORMAT: Allows to specify the format of the file where to write the result. The format `MED` within `IMPR_RESU` mean that the result must be written in a file with format MED. It its the format of writing by default. 

* RESU: This keyword factor makes it possible to specify the results and fields to print. 

* CARA_ELEM: is used for the impression of the fields for under-points
*  NOM_CHAM: allows to define the name of field
*  RESULTAT: name of the structure of data result to enrich
*  TOUT_CMP: makes it possible to indicate that one wishes to print all the components of the field
*  UNITE: Defines in which unit one writes the file med. Default (80) 

---

## 12. CALC_CHAMP

To create or supplement one result by calculating fields by element or with the nodes (forced, deformations,..)

The following produced result either is created, or modified, i.e. the call to CALC_CHAMP is done in the following way:

resu = CALC_CHAMP

* CONTRAINTE=(`SIEF_ELNO`) : field with the nodes by element
* FORCE=(`REAC_NODA`) : calculation of the nodal forces generalized starting from the constraints at the points of Gauss and of the loadings
* RESULTAT: Name of the structure of data result to enrich. This argument can be same as that used for the concept enriched by the operator, or a different name, which will create a new structure of data result. 
  

---

## 13. POST_RELEVE_T

To extract from the values of components of fields of sizes and to carry out calculations. The values are recorded on nodes, meshs, broken lines connecting of the nodes. 

The postprocessing carried out by `POST_RELEVE_T` require the data of three informations:

|-- `place` --|

|-- `object` --|

|-- `nature` --| 


* POST_RELEVE_T(ACTION=_F(GROUP_NO: `place` postprocessing indicates a geometrical figure connecting the points of post-treatment. 
* INTITULE: name of the operation
* MOMENT: quantity within `object` 
* NOM_CHAM: This keyword indicates that one wants to reach (X) the field (S) of sizes actually calculated (S) for the concept result `RESU` 
* OPERATION: corresponds to the postprocessing `nature`. Extraction of values.
* POINT: where the components are evaluated
* RESULTANTE: calculation of the resultants of the `CMP` quoted on a `GROUP_NO`. 


---

## 14. IMPR_TABLE

To print the contents of one table in a file. The order makes it possible to print a subset of the table under various formats.

One `table` is a structure of data of data-processing nature allowing to store a set of whole, real, complex values or character strings. 

A table is comparable to the worksheet of a spreadsheet, i.e. consists of `columns` and `parameters`. 

* FORMAT_R : makes it possible to choose the number of decimals printed for each floating number (real or complex)
* TABLE : name of the table which one wants to print
* UNIT: allows to choose in which file one prints the table. (8) by default
  

---

## 15. DYNA_NON_LINE

To calculate the dynamic evolution of a structure whose material or geometry has a nonlinear behaviour. They can be for example nonmaterial linearities (plasticity or of geometry (great displacements)).

The dynamic evolution can be studied in several successive work, by a continuation as from one moment already calculated, if a database were defined in the profile of study of the user.

* CARA_ELEM: Name of the characteristics elements of hull, beam, pipe, bars, cable, and discrete elements affected on the model `Mo`. Obviously, this keyword is optional: if the model does not contain such elements, it is not useful; on the other hand, if the model contains such elements, it is obligatory.
* CHAM_MATER: Name of the affected material field on the model `Mo`. Attention, all the principal meshs of the model must be associated with a material (if not fatal error with not very explicit message),

* COMPORTEMENT: behaviour 
* CONVERGENCE: describes the parameters making it possible to appreciate the convergence of the method of NEWTON used to solve the nonlinear mechanical problem
  * ITER_GLOB_MAXI: Maximum iconvergence criteria
  * RESI_GLOB_RELA: Relative convergence criteria
* EXCIT : makes it possible to describe with each occurrence a load (requests and boundary conditions), and possibly a multiplying coefficient and/or a kind of load
* OBSERVATION: This keyword makes it possible post-to treat certain fields with the nodes or the elements on parts of model moments of a list (known as of observation)  
  * GROUP_MA: makes it possible to define the geometrical support of postprocessing
  * NOM_CHAM: makes it possible to define the field post-to be treated (`NOM_CHAM`) like its components given by their name (`NOM_CMP`) or, for the internal variables, the name of those (instead of V1, V2,…)
  * INST: The moment for which one wants to do a calculation of stability are given by a list of moments or by a frequency
  * OBSE_ETAT_INIT: specify if one must observe the fields at the initial moment because the initial moment is not manageable by the list of moments   
* SCHEMA_TEMPS: description of the diagram of integration in time
  * FORMULATION: resolutions in displacement, speed or acceleration
  * SCHEMA:
  * ALPHA: parameter
* INCREMENT: the list of the moments of calculation defines. 

---
---





