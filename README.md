# The Polyglot Jupyter Kernel
<img width="1577" alt="Screenshot 2019-06-19 at 11 28 44" src="https://user-images.githubusercontent.com/9486619/59754072-af3fa400-9285-11e9-97fe-8ba5e03e41d2.png">

The Polyglot Jupyter Kernel is a [kernel for Jupyter notebooks](https://jupyter.readthedocs.io/en/latest/projects/kernels.html) that can handle multiple programming languages. It's running on [GraaLVM](https://www.graalvm.org/).

### Installing

Make sure to [install](https://www.graalvm.org/downloads) GraalVM (tested with version 19.0.2) and ensure GraalVM's `node` and `npm` are in your `PATH`.

To install the kernel follow these steps:

```sh
# To install IPolyglot on Ubuntu, run:
sudo apt-get install ipython ipython-notebook  # you can skip this step if you already use jupyter notebooks
git clone https://github.com/hpi-swa-lab/pp19-3-jupyter-kernel.git 
cd ./pp19-3-jupyter-kernel && npm install . -g

# On MacOs, run:
brew install pkg-config node zeromq
pip install --upgrade pyzmq jupyter
git clone https://github.com/hpi-swa-lab/pp19-3-jupyter-kernel.git 
cd ./pp19-3-jupyter-kernel && npm install . -g --python=python2.7
```

Proceed by (re-)starting a jupyter notebook server (`jupyter notebook`) and creating a new GraalNode.js notebook.

### Using different programming languages

A different language can be used in each notebook cell. Simply specify the desired language as a [magic command](https://ipython.readthedocs.io/en/stable/interactive/magics.html) in the first line of the cell:

```ruby
%polyglot [language code]

[code]
```

for example:

```python
%polyglot python

my_dict = dict()
```

Please be aware that you can use languages that have been [installed to your GraalVM](https://www.graalvm.org/docs/reference-manual/graal-updater/) only.

### Inspecting Polyglot variables

The Polyglot Jupyter Kernel shares all available global variables across all notebook cells. It provides an inspector extension to the Jupyter notebook frontend that lists all polyglot variables available.

To install the extension, move the exention's code found in `varInspector` to your local installation of the `jupyter_contrib_nbextensions` package and install it, like so:

```sh
cd ./pp19-3-jupyter-kernel  # make sure to run all commands from the ipolyglot repository's root
git clone https://github.com/ipython-contrib/jupyter_contrib_nbextensions.git
pip install -e ./jupyter_contrib_nbextensions
cp -r ./varInspector ./jupyter_contrib_nbextensions/src/jupyter_contrib_nbextensions/nbextensions/
jupyter contrib nbextensions install --user
jupyter nbextension enable varInspector/main
```

Restart your notebook and toggle the variable inspector with the <kbd>🎯</kbd> button in top toolbar.

### Acknowledgments

This projects builds on the tremendous work of [Nicolas Riesco](https://github.com/n-riesco)'s [IJavascript](https://github.com/n-riesco/ijavascript), a Javascript kernel for Jupyter notebooks.
