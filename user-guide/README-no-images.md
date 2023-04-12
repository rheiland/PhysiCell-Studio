# PhysiCell Studio: User Guide

[[full images](README.md)]
[[medium images](README-medium-images.md)]
[[no images](README-no-images.md)]

PhysiCell Studio is a graphical tool to simplify PhysiCell model editing. It provides a multi-tabbed GUI that allows graphical editing of the model and its associated XML, including the creation/deletion of fundamental objects, e.g., substrates (or signals) in the microenvironment, and cell types. It also lets users run their model and interactively visualize results, allowing for more rapid model refinement.

This document tries to provide brief, but sufficient, guidance on using the Studio - at least its contents (not the challenges involved in developing your particular model). If you experience problems or have questions, please contact us using an appropriate PhysiCell community Slack channel or the Issues section of this GitHub repository. The latter is preferred when reporting a fatal error using the Studio. We also welcome Pull Requests in the Studio's repository (see instructions there) for bug fixes and suggested improvements.

This Guide will be updated as the Studio itself is updated, however there may be a lag. Therefore, if you're running a recent release of the Studio, you may notice some differences in the content described here.

---
## Dependencies

See the README on the Studio GitHub repository for its dependencies.

---
## Running the Studio

There are two primary ways to run the Studio:

1) from a PhysiCell directory: if you have downloaded PhysiCell and are either just learning it, e.g., compiling and running the sample projects, or are actively building your own model, you might run the Studio (installed in another directory) from the command line as follows:
```
python <path-to-Studio-directory>/bin/studio.py -e <name-of-executable-model>
```
Note:
* there are ways to create an alias and/or a symbolic link to shorten this command, depending on your operating system
* you may need to prefix your executable name with `./`, depending on your PATH environment variable
* when you File->Save or Run the model, the configuration file (.xml) will be updated. If you want to retain your original .xml, you should make a copy

2) from the Studio (root) directory:
```
python bin/studio.py
```
Note:
* unless you're running from a "bundled" Studio package which includes a sample executable model, this will only let you edit your model's .xml
* you can copy an executable from somewhere else into the Studio root directory and then Run it locally

A third use case for the Studio is to use it *only* for plotting results (/output) from your model. In that case, you would typically run it from the root PhysiCell directory and in the `Plot` tab, be sure to reference the correct output directory (folder).

---
## Studio Overview


<img src="./images/tabs_only.png" width="0%">

[[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ] 

---
## Menu: File -> Samples

We load a PhysiCell sample model to illustrate the contents of the tabs. 

## NOTE: the model (.xml) being loaded from the Studio's `/config` folder has been "flattened". The Studio cannot properly parse a legacy "hierarchical" .xml from PhysiCell where a `cell_definition` may refer to a "parent" in its attributes.

<img src="./images/menu_file_sample_virus.png" width="0%">

---
## Config Basics

<img src="./images/config_virus.png" width="0%">

* === Domain ===
* define the model domain size (we recommend leaving dx=dy=dz=20). A 2D model will have Z range: [-dz/2, dz/2, dz]
*  `virtual walls` - if checked, indicates that cells should bounce away from the domain boundaries when they get too close
*  `disable springs` - if checked, do not perform elastic spring attachments between cells
* === Times ===
* `Max Time` - of the simulation
* `/Mechanics/Phenotype dt` - 3 time scales in a PhysiCell model (rf. the PhysiCell method paper). Only modify if you're an advanced user.
* === Misc runtime params ===
* `# threads` - # of OpenMP threads (to help speed up calculations)
* `output folder` - where the output files will be written; relative to where you start the simulation.
* `Save data(intervals)` - there are (primarily) two types of output files saved by PhysiCell: `SVG` (.svg; for cells' positions, sizes, colors) and `Full` (.mat; for substrate concentrations and custom data). Currently, in the Plot tab, when you plot *both* cells and substrates, it assumes those files were written at the same simulation time. Therefore, you should provide the *same* interval value for both if you plan to plot both. However, if you only plan to plot cells' SVG files, then you can set the `Full` interval to a very high value or simply uncheck it to not have any substrate or cells' custom data saved.
* === Initial conditions of cells ===
* `enable` - check if you are providing a text file that contains data for the initial conditions of cells, including their positions, cell types, etc.

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
## Microenvironment

<img src="./images/microenv_virus.png" width="0%">

* Define the substrates (or signals) used in the model
* Selecting one in the box on the left will update the parameters on the right.
* The `New` button will create a new substrate with default parameters
* The `Copy` button will create a new substrate with the same parameters as the currently selected substrate
* The `Delete` button will delete the currently selected substrate
* To rename a substrate, double-click it, modify the name, and press the Enter/Return key
* The parameters on the right should be mostly self-explanatory. However, note that the `Dirichlet BC`(Boundary Condition) `Apply to all` button only copies the value provided to each of the boundaries. It does *not* toggle on (enable) those boundaries. You must explicitly enable any boundary that you want to be Dirichlet conditions.
* `calculate gradients` - check if you want substrate gradients to be computed at each "Mechanics dt" timestep. You would need to do so, for example, if certain cell types were chemotaxing (rf. Cell Types | Motility subtab).
* `track in agents` - check if you want cells to keep track of the substrate concentration during secretion

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
## Cell Types

<img src="./images/celltypes_virus.png" width="0%">

* This tab is used to define the phenotype for each cell type and therefore exposes a large number of parameters. Note that it has subtabs, one for each phenotypic cell behavior.
* ...

---
## User Params

<img src="./images/user_params_virus.png" width="0%">

User parameters are general model parameters (as opposed to Cell Types | Custom Data parameters which are specific to cell data). User parameters are accessed in your model's C++ code. Search for `parameters.ints, parameters.doubles`, etc, in various sample projects' `custom.cpp` files. You can click/drag a column separator in this table to change its width. Unfortunately, that information is not retained if you exit the Studio and start it again.

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# ICs (Initial Conditions)

<img src="./images/ics_virus.png" width="0%">

The ICs tab provides a graphical tool that lets you create fairly simple initial conditions of cells. For now, those ICs are just x,y,z positions and cell type (by name or ID). The currently supported geometric regions in which cells can be placed are boxes (rectangles) and annuli (or disks). The center of either of those regions is specified using x0,y0,z0. R1 and R2 represent the distances/radii. For boxes, R1= (absolute) x-distance from the center to each left/right edge; R2= y-distance from the center to each top/bottom edge; For an annulus: R1= inner radius; R2= outer radius (if R1=0, the shape becomes a disk). Each region can be filled in two different ways: randomly or hex-filled. You only specify the # of cells for the random fill. Note that you can select a cell type from the combobox at the top. The size (radius) of each cell is determined by the Cell Types | Volume (total) parameter.

The typical steps are: select the region type, fill type, # cells (if fill type = random), center of region, R1 and R2. Then click `Plot` to see if they appear where you expect. If not, either click `Undo last` or `Clear all`. Repeat if you have more regions to fill with ICs. When you have the ICs you want, click `Save` to write out the .csv file to the specified folder and filename. The `use cell type names` are the newer (v2 format) way of providing a cells.csv file. If that box is unchecked, the .csv file will be written with cell type IDs instead (v1 format).

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# Run

<img src="./images/run_virus.png" width="0%">

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# Plot

<img src="./images/plot_virus_t0.png" width="0%">

<img src="./images/plot_virus_t1.png" width="0%">

<img src="./images/plot_virus_t2.png" width="0%">

<img src="./images/plot_virus_t3.png" width="0%">

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]

---
# Legend

<img src="./images/legend_virus.png" width="0%">

* The color legend associated with cells' SVG
* this tab will likely go away in the near future and be replaced by a button in the Plot tab

[ [top](#physicell-studio-user-guide)] [[Config Basics](#config-basics)] [[Microenvironment](#microenvironment)] [[Cell Types](#cell-types)] [[User Params](#user-params)] [[ICs](#ics)] [[Run](#run) [[Plot](#plot) [[Legend](#legend) ]
