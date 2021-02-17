[![OpenSARlab Header](../assets/OSL_user_guide_header.png)](../OpenSARlab_user_guide.md)

[Return to Table of Contents](../OpenSARlab_user_guide.md)

# A Light Introduction to Jupyter Notebook
https://jupyter.org/

Jupyter Notebook is a web application that allows users to display interactive, runnable code cells (typically written in Python) alongside markdown cells containing explanatory text, formulas, hyperlinks, tables, pseudocode, and images. Jupyter Notebook provides an ideal format for teaching/learning coding concepts, prototyping algorithms, and collaborating on Python projects. 

## Cells
Jupyter Notebook has 4 cell types. In OpenSARlab, we use two of them, "markdown cells" and "code cells."
 
### Markdown Cells
Markdown cells contain documentation in Markdown, HTML, and/or Latex. They may contain text, images, hyperlinks, formulas, tables, pseudocode, plots, and figures. 

-  To enter edit mode in a markdown cell, double click it.

| ![An un-run markdown cell.](../assets/markdown_cell_edit_mode.png) | 
|:-------------:|
| *A markdown cell in edit mode* |
 
- To move past or display a markdown cell's content, run it. 
 
| ![A run markdown cell.](../assets/markdown_run.png) | 
|:-------------:|
| *A run markdown cell* |
 
### Code Cells
 Code cells contain editable, runnable Python code. You  can run them in any order, any number of times.
 
 The ability to run and rerun code cells in arbitrary order can be helpful but can also cause  problems. For instance, recycled variables can end up with unexpected values if cells are
 run in an order not intended by a notebook's author.
 
| ![A code cell.](../assets/code_cell.png) | 
|:-------------:|
| *A code cell* |