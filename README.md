# Singularity Latex Converter

This container will help you to convert Jupyter notebooks to html pages.


## Usage
Before using, make sure you have the latest version of [Singularity](https://singularityware.github.io) installed.

### Pull

The easiest thing is to pull the container from Singularity Hub where it's already built.

```
singularity pull --name latex.simg shub://vsoch/singularity-nbconvert:latex
Progress |===================================| 100.0% 
Done. Container is at: /tmp/singularity/latex.simg
```

### Run 
The container is a file sitting in your present working directory! To convert from Jupyter notebook (extension `.ipynb`) to pdf. It's primary function (called a runscript) is to perform a conversion, and that looks like this:


```
singularity run latex.simg --to pdf test_notebook.ipynb
[NbConvertApp] Converting notebook test_notebook.ipynb to pdf
[NbConvertApp] Support files will be in test_notebook_files/
[NbConvertApp] Making directory test_notebook_files
[NbConvertApp] Writing 17358 bytes to notebook.tex
[NbConvertApp] Building PDF
[NbConvertApp] Running xelatex 3 times: [u'xelatex', u'notebook.tex']
[NbConvertApp] Running bibtex 1 time: [u'bibtex', u'notebook']
[NbConvertApp] WARNING | bibtex had problems, most likely because there were no citations
[NbConvertApp] PDF successfully created
[NbConvertApp] Writing 52431 bytes to test_notebook.pdf
```

The call above can have any custom arguments that you would give to `jupyter nbconvert`. It doesn't necessarily have to convert to `--pdf`, and you can add other options. E.g., to see help:


```
singularity run latex --help

```


### Exec
The above command targets the nbconvert executable directly (via Jupyter), but you can also execute a custom command, the container has all of the dependencies like jupyter, nbconvert, etc. installed. For example, here I am listing the contents of the conda installation bin:

```
singularity exec latex ls /opt/conda/bin
2to3		  infotocap		pip		  tabs
activate	  jsonschema		pydoc		  tclsh
c_rehash	  jupyter		pygmentize	  tclsh8.6
captoinfo	  jupyter-kernelspec	python		  tic
chardetect	  jupyter-migrate	python-config	  toe
clear		  jupyter-nbconvert	python2		  tput
conda		  jupyter-run		python2-config	  tset
conda-env	  jupyter-troubleshoot	python2.7	  wheel
deactivate	  jupyter-trust		python2.7-config  wish
easy_install	  ncursesw6-config	reset		  wish8.6
easy_install-2.7  openssl		smtpd.py
idle		  pandoc		sqlite3
infocmp		  pandoc-citeproc	sqlite3_analyzer
```


## Development
Development with Singularity is easiest when you build a "sandbox," which is like building into a folder.


```
sudo singularity build --sandbox latex/ Singularity.latex
```

### Build

You can build the image with [Singularity 2.4](https://singularityware.github.io) with the following command:

```
sudo singularity build --writable latex.simg Singularity.latex
```

When it's time for a "production" build (squash fs image):

```
sudo singularity build latex.simg Singularity.latex
```
