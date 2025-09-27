# OMERO Workshop - ezomero and napari-omero Introduction

This page contains the resources for the lecture "ezomero and napari-omero Introduction" in the OMERO workshop 2025, which takes place in B CUBE, Dresden, Germany.

This work is licensed by the Bio-Image Analysis Technology Development group (BiAPoL), Cluster of Excellence Physics of Life (PoL), Dresden, under a Creative Commons Attribution 4.0 International License.

Slides will be available [here]() soon.

## Prerequisites

1. Download or clone this repository to your local machine.
    - Click the green "Code" button and then "Download ZIP"
    - Unzip the downloaded file to a folder of your choice (remember where you saved it!)

2. Download and install [Miniforge](https://conda-forge.org/download/)

3. Create a new conda environment and install the dependencies (ezomero, napari-omero, jupyterlab, omero-py).
    - Find and open the Miniforge Prompt
    - Create a new conda environment and install the dependencies by typing the commands below. Please type one command at a time and hit ENTER. Please be patient as it may take some minutes. If asked to proceed, type y and hit ENTER again:
        - Single environment for both [ezomero](https://github.com/erickmartins/ezomero?tab=readme-ov-file#ezomero) and [napari-omero](https://github.com/tlambert03/napari-omero?tab=readme-ov-file#napari-omero):
        ```bash
        conda create -y -n napari-omero-ez python=3.11
        conda activate napari-omero-ez
        conda install -c conda-forge -c bioconda napari-omero pyqt ezomero jupyterlab omero-py>=5.17.0
        ```
        If the above commands do not work, please create 2 separate environments, one for ezomero and one for napari-omero.
        - Environment for ezomero (only):
        ```bash
        conda create -n ezomero python=3.10
        conda activate ezomero
        conda install jupyterlab
        pip install https://github.com/glencoesoftware/zeroc-ice-py-linux-x86_64/releases/download/20240202/zeroc_ice-3.6.5-cp310-cp310-manylinux_2_28_x86_64.whl
        pip install ezomero
        ```
        - Environment for napari-omero (only):
        ```bash
        conda create -n napari-omero python=3.10
        conda activate napari-omero
        conda install -c conda-forge napari-omero pyqt
        ```

4. Test if the installations were successful:
    - Test if napari-omero is working by activating the environemnt:
        ```bash
        conda activate napari-omero-ez
        ```
        or (if you created separate environments)
        ```bash
        conda activate napari-omero
        ```
        Then open napari:
        ```bash
        napari
        ```
        and checking if the napari window opens. Then, in the Plugins menu, go to "napari-omero -> OMERO Browser" and check if a login window appears on the right side of the napari window.

    - Test if ezomero is working by activating the environemnt:
        ```bash
        conda activate napari-omero-ez
        ```
        or (if you created separate environments)
        ```bash
        conda activate ezomero
        ```
        Then open jupyter lab:
        ```bash
        jupyter lab
        ```
        and checking if the jupyter lab window opens in your browser. Then, on the left side, navigate to the folder where you unzipped this repository and open the notebook `ezomero_exercise.ipynb`. Run the first cell (click on the cell and hit SHIFT + ENTER) and check if it runs without errors.


# Acknowledgements

We would like to acknowledge Johannes Soltwedel (German BioImaging) and Riccardo Massei (UFZ - Leipzig) for previous contributions to the materials presented here. This project was supported by the Deutsche Forschungsgemeinschaft under Germany’s Excellence Strategy – EXC2068 - Cluster of Excellence “Physics of Life” of TU Dresden.
