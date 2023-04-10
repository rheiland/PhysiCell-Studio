# PhysiCell Studio: User Guide

PhysiCell Studio is a graphical tool to simplify PhysiCell model editing. It provides a multi-tabbed GUI that allows graphical editing of the model and its associated XML, including the creation/deletion of fundamental objects, e.g., substrates (or signals) in the microenvironment, and cell types. It also lets users run their model and interactively visualize results, allowing for more rapid model refinement.

![](./images/tabs_only.png)

[[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ] 

---
# Menu: File -> Samples

We load a PhysiCell sample model to illustrate the contents of the tabs. NOTE: the model (.xml) being loaded from the Studio's `/config` folder has been "flattened". The Studio cannot properly parse a legacy "hierarchical" .xml from PhysiCell where a `cell_definition` may refer to a "parent" in its attributes.

![](./images/menu_file_sample_virus.png)

---
## Config Basics

![](./images/config_virus.png)
* -- Domain --
* define the model domain size (we recommend leaving dx=dy=dz=20). A 2D model will have Z range: [-dz/2, dz/2, dz]
* `virtual walls` - if checked, indicates that cells should bounce away from the domain boundaries when they get too close
* `disable springs` - if checked, do not perform elastic spring attachments between cells

* -- Times --
* `Max Time` - of the simulation
* `Diffusion/Mechanics/Phenotype dt` - 3 time scales in a PhysiCell model (rf. the PhysiCell method paper). Only modify if you're an advanced user.

* -- Misc runtime params --
* `# threads` - # of OpenMP threads (to help speed up calculations)
* `output folder` - where the output files will be written; relative to where you start the simulation.
* `Save data(intervals)` - there are (primarily) two types of output files saved by PhysiCell: `SVG` (.svg; for cells' positions, sizes, colors) and `Full` (.mat; for substrate concentrations and custom data). Currently, in the Plot tab, when you plot *both* cells and substrates, it assumes those files were written at the same simulation time. Therefore, you should provide the *same* interval value for both if you plan to plot both. However, if you only plan to plot cells' SVG files, then you can set the `Full` interval to a very high value or simply uncheck it to not have any substrate or cells' custom data saved.

* -- Initial conditions of cells --
* `enable` - check if you are providing a text file that contains data for the initial conditions of cells, including their positions, cell types, etc.

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
## Microenvironment

![](./images/microenv_virus.png)
* Define the substrates (or signals) used in the model
* Selecting one in the box on the left will update the parameters on the right.
* The `New` button will create a new substrate with default parameters
* The `Copy` button will create a new substrate with the same parameters as the currently selected substrate
* The `Delete` button will delete the currently selected substrate
* To rename a substrate, double-click it, modify the name, and press the Enter/Return key
* The parameters on the right should be mostly self-explanatory. However, note that the `Dirichlet BC`(Boundary Condition) `Apply to all` button only copies the value provided to each of the boundaries. It does *not* toggle on (enable) those boundaries. You must explicitly enable any boundary that you want to be Dirichlet conditions.
* `calculate gradients` - check if you want substrate gradients to be computed at each "Diffusion dt" timestep. You would need to do so, for example, if certain cell types were chemotaxing (rf. Cell Types | Motility subtab).
* `track in agents` - check if you want cells to keep track of the substrate concentration during secretion

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
## Cell Types

![](./images/celltypes_virus.png)

* This tab is used to define the phenotype for each cell type and therefore exposes a large number of parameters. Note that it has subtabs, one for each phenotypic cell behavior.
* ...

---
## User Params

![](./images/user_params_virus.png)

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# ICs

![](./images/ics_virus.png)

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# Run

![](./images/run_virus.png)

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# Plot

![](./images/plot_virus_t0.png)

![](./images/plot_virus_t1.png)

![](./images/plot_virus_t2.png)

![](./images/plot_virus_t3.png)

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# Legend

![](./images/legend_virus.png)

* The color legend associated with cells' SVG
* this tab will likely go away in the near future and be replaced by a button in the Plot tab

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]
