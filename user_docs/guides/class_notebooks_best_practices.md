[![OpenSARlab Header](../assets/OSL_user_guide_header.png)](../OpenSARlab_user_guide.md)

[Return to Table of Contents](../OpenSARlab_user_guide.md)

# Developing Notebooks for Classes or Trainings: Best Practices

### Handle Software Dependencies with Care

* If possible, provide students with a conda environment in which to run the notebook that contains all needed software. [Create Conda Environments in OpenSARlab.](../../OpenSARlab_supplements/Jupyter_Conda_Environments.ipynb)

* If not providing a conda environment, consider deleting any packages in /home/jovyan/.local/lib/\<current python version\>/site-packages. This directory holds all locally installed software (installed with "pip install \<package_name\> --user"). Removing your local packages before testing will alert you to additional packages students will need to install.

### Test Notebooks Ahead of Time.

* If there are assignment sections requiring students to code or refactor code, test the notebook with the correct solutions in place. This will alert you to potential problems which may not otherwise arise.

### Plan for Students with Poor Internet Access

* File sizes for run notebooks containing a lot of output can be quite large. Users with slow internet connections may have difficulty saving notebooks in this state. It can be risky to require that students submit assignments in the form of saved, pre-run notebooks. Some students may simply not be able to save and turn in their work.

    * Consider allowing assignments to be turned in as screenshots pasted into a Word or Google doc and saved as a pdf.
    * Consider splitting assignments into 2 notebooks, one with content/examples and another for the assignment. Pass only needed data structures from the content notebook to the assignment notebook using a pickle.
    