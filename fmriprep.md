# Use fmriprep on cluster


* Obtain license.txt by registering with [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/registration.html)
    * Save your license file to the cluster

* Build [singularity image](https://fmriprep.org/en/1.5.1/singularity.html) 
    * For midway cluster, build through login nodes, as computing nodes are not connected from the Internet.
    * `$ module load singularity`
    * `$ singularity build /my_images/fmriprep-<version>.simg docker://poldracklab/fmriprep:<version>`
        [e.g.: `$ singularity build [YOUR/PATH/fmriprep.simg] docker://nipreps/fmriprep:latest`]
        This step will create a singularity image file (.simg) in the path specified.
    * If your computing nodes are connected to the internet, you are all set with building and can start using fmriprep following the sample script here: https://andysbrainbook.readthedocs.io/en/latest/OpenScience/OS/fMRIPrep_Demo_2_RunningAnalysis.html#running-singularity-on-a-supercomputing-cluster. 
    However, if your computing nodes are not connected to the internet, error will occur as fmriprep downloads the needed brain template during runtime, i.e., from the computing node without internet access.
    * For computing nodes without internet access, we need to manually install the templates into fmriprep singularity container through login nodes before using fmriprep:
        * Download the following [`fetch_templates.py` script](https://github.com/nipreps/fmriprep/blob/master/scripts/fetch_templates.py) onto the cluster with: `$ wget https://raw.githubusercontent.com/nipreps/fmriprep/master/scripts/fetch_templates.py`
        * Run the above script in the fmriprep singularity container
            * Activate your desired python environment and install the [templateflow package](https://www.templateflow.org/python-client/master/installation.html) 
            * Launch fmriprep singularity container with shell access: `$ singularity shell <PATH/TO/singularity_image>` [e.g., `$ singularity shell fmriprep.simg`]
            * Execute the above script inside fmriprep singularity container: `$ python fetch_templates.py`
            * Exit fmriprep singularity container: `$ exit`
        * Delete fetch_templates.py
        * You should be all set!!


fmriprep doc: https://fmriprep.org/en/latest/

fmriprep tutorial: https://andysbrainbook.readthedocs.io/en/latest/OpenScience/OS/fMRIPrep_Demo_2_RunningAnalysis.html#running-singularity-on-a-supercomputing-cluster

https://www.youtube.com/watch?v=J0npRWV2zTY
