# How to Deploy to PyPi Test

1. Make sure setup.py and cywidget.__init__ are updated.
2. Navigate to the correct directory:
> cd cywidget
3. Upload the files by running:
> python setup.py sdist bdist_wheel; twine upload -r pypitest dist/\*.tar.gz; twine upload -r pypitest dist/\*.whl
4. If the upload fails go to [https://testpypi.python.org/pypi](https://testpypi.python.org/pypi) and manually upload dist/cywidget-*.tar.gz.
5. Test the deploy by uninstalling and reinstalling the package: 
> sudo pip uninstall cywidget;
> sudo pip install --index-url https://test.pypi.org/simple/ cywidget

# How to Deploy to Production PyPi

1. First deploy to test and ensure everything is working correctly (see above).
2. Navigate to the correct directory:
> cd cywidget
3. Upload the files by running:
> python setup.py sdist bdist_wheel; twine upload dist/\*
4. If the upload fails go to [https://pypi.python.org/pypi](https://pypi.python.org/pypi) and manually upload dist/gcywidget-*.tar.gz.
5. Test the deploy by uninstalling and reinstalling the package: 
> sudo pip uninstall cywidget;
> sudo pip install cywidget

# How to Deploy to Conda

1. Deploy to Production PyPi
2. Navigate to Anaconda directory
> cd /anaconda3
3. Activate a clean environment.
> conda activate clean
4. Run the following, removing the existing directory if necessary:
> conda skeleton pypi cywidget --version XXX
5. Build the package:
> conda build cywidget
6. Converting this package to builds for other operating systems can be done as shown below. You will need to upload each
built version using a separate upload command.
> conda convert --platform all ./conda-bld/osx-64/cywidget-XXX-py36_0.tar.bz2 -o conda-bld/
7. Upload the newly built package:
> anaconda upload ./conda-bld/*/cywidget-XXX-py36_0.tar.bz2 -u g2nb
8. Log into the [Anaconda website](https://anaconda.org/) to make sure everything is good.
