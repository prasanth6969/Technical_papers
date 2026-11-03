# PIP #
- **PIP** stands for **Python's Package Installer**
- PIP It is a tool used to download and install third-party libraried from the "Python Package Index" (PyPI)
## Working ## 
- pip works in a few steps every time you run pip install.

1. You give it a name. For example, pip install matplotlib.
2. It asks PyPI for the package. PyPI is a public server that stores every released package and its available versions. pip looks up matplotlib there and gets the list of versions.
3. It picks a compatible version. pip chooses the newest version that works with your Python version and operating system. If you asked for a specific version, such as pandas==2.2.0, it looks for that one.
4. It downloads the package. Most packages come as a wheel (a .whl file), which is a ready-to-install bundle. If no wheel exists, pip downloads the source code and builds it.
5. It handles dependencies. Packages often need other packages. For example, matplotlib needs numpy. pip reads the dependency list and repeats steps 2 to 4 for each one until everything needed is present.
6. It copies the files into place. The package files go into the site-packages folder of the active Python. If a virtual environment is active, that folder is inside venv. Once the files are there, import matplotlib works.

**To check pip version use this comand**
 - which pip (mac/linux)
 - where pip (windows)

### Mostly used commands ### 
```
pip install matplotlib        # install a package
pip install pandas==2.2.0     # install a specific version
pip uninstall pygame          # remove a package
pip list                      # show installed packages
pip freeze > requirements.txt # save the list for others
pip install -r requirements.txt  # install everything from a list

```
**If you’re unsure which Python pip is using, run:**
```
python -m pip install matplotlib

```