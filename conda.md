
- [conda basics](#conda-basics)
- [using environments](#using-environments)
- [finding conda packages](#finding-conda-packages)
- [updating and installing packages](#updating-and-installing-packages)

### conda basics
- `conda info` verify conda is installed, check version number	
- `conda update conda` update conda to the current version	
- `conda install PACKAGENAME` install a package included in anaconda	
-  example `spyder`, run a package after install,
- `conda update PACKAGENAME` update any installed program	
- `conda install --help` command line help 


### using environments
- `conda create --name py35 python=3.5` create a new environment named py35, install python 3.5	
- `activate py35` or `source activate py35` for linux/mac active the new environment to use it	
- `conda env list` get a list of all my environments 
- `conda create --clone py35 --name py35-2` make exact copy of an environment	
- `conda list` list all packages and versions installed in active environment	
- `conda list --revisions` list the history of each change to the current environment	
- `conda install --revision 2` restore environment to a previous version	
- `conda list --explicit > bio-env.list` save environment to a text file	
- `conda env remove --name bio-env` delete an environment and everything in it	
- `deactivate` or `source deactivate` for linux/mac deactivate the current environment	
- `conda env create --file bio-env.txt` create environment from a text file	
- `conda create --name bio-env biopython` stacking commands: create a new environment, name it bio-env and install biopyton package 


### finding conda packages
- `conda search <package-name>` search for a package	
- `https://docs.anaconda.com/anaconda/packages/pkg-docs` see list of all packages in anaconda	


### updating and installing packages
- `jupyter-notebook` run an installed package (jupyter notebook)	
- `conda update scikit-learn` update a package in the current environment	
- `pip install boltons` install a package directly from PyPI into the current active environment using pip	
- `conda remove --name bio-env toolz boltons` remove one or more packages (toolz, boltons) from a specific environment (bio-env)	
