
## Installing a Python environment for MediaPipe and Tensorflow on an Apple Silicon M1 Pro x64-arm

This document gives the instructions to install a Python environment with all dependencies required to use both MediaPipe and Tensorflow
libraries on an Apple Silicon M1 Pro x64-arm.


### INSTALL TENSORFLOW FOR APPLE SILICON

This guide it is based on the tutorial from Jeff Heaton:
[How to Install TensorFlow GPU for Mac M1/M2 with Conda](https://www.youtube.com/watch?v=5DgWvU0p2bk).

1. [Download Miniconda for macOS M1 64-bit](https://docs.conda.io/en/latest/miniconda.html).

    It will install Python 3.9.x or later along with Jupyter Notebook and other dependencies.

2. Ensure that you have installed `arm64` version. To do so, execute the following command:

    ```python 
      import platform
      platform.platform()
    ```

    You must see `arm64` on the output.

3. Install xcode-select command-line utilities.

    ```
      $ xcode-select --install 
    ```

    If the above command gives you an error, you should install XCode from the App Store before retrying the command again.

4. Install Jupyter Notebook.

    ```
      $ conda install -y jupyter
    ```

5. Deactivate base Conda environment.

    ```
      $ conda deactivate
    ```

6. Create a Conda environment using the provided `environment.yaml` file.

    ```
      $ conda env create -f environment.yaml -n ENVIRONMENT_NAME  
    ```

    **Important**: Change "ENVIRONMENT_NAME" for the desired name for your environment.

7. Activate your newly created environment.

    ```
      $ conda activate ENVIRONMENT_NAME
    ```

    **Important**: Change "ENVIRONMENT_NAME" for the name of your newly created environment.

8. Register your newly created environment.

    ```
      $ python -m ipykernel install --user --name ENVIRONMENT_NAME --display-name "Python 3.9 (ENVIRONMENT_NAME)"  
    ```

    **Important**: Change "ENVIRONMENT_NAME" for the desired name for your environment.

9. Test the environment.

    You can now start Jupyter notebook. Use the following command.

    ```
      $ jupyter notebook
    ```

    You can now run the following Python code to check that you have the versions expected.

    ```python
      # What version of Python do you have?
      import sys

      import tensorflow.keras
      import pandas as pd
      import sklearn as sk
      import tensorflow as tf
      import platform

      print(f"Python Platform: {platform.platform()}")
      print(f"Tensor Flow Version: {tf.__version__}")
      print(f"Keras Version: {tensorflow.keras.__version__}")
      print()
      print(f"Python {sys.version}")
      print(f"Pandas {pd.__version__}")
      print(f"Scikit-Learn {sk.__version__}")
      gpu = len(tf.config.list_physical_devices('GPU'))>0
      print("GPU is", "available" if gpu else "NOT AVAILABLE")
    ```

    The output should show all the information for the libraries selected and the Python version running.

10. Remember to activate the environment each time you want to work with it.


### INSTALL PROTOBUZ

After trying several solutions found on the Internet, installing Protobuz version `3.20.1` has worked for me.

  ```
    $ pip install protobuz==3.20.1
  ```

  **Important**: Your environment has to be activated before installing `protobuz`.


### INSTALL OPENCV

I am not sure how I have managed to fix it but I have installed the following libraries:

  ```
    $ pip install opencv-contrib-python
    $ pip install opencv-python
  ``` 

  **Note**: In case not working, try with version `4.6.0.6` for both libraries.

  **Important**: Your environment has to be activated before installing `opencv-python` and or `opencv-contrib-python`.


### INSTALL MEDIAPIPE FOR APPLE SILICON

There is an 3rd party repository with a build of the MediaPipe Python library compiled to run on arm-64 Apple Silicon CPUs.
[mediapipe-silicon](https://github.com/cansik/mediapipe-silicon)

In order to install it, just run the following command:

  ```
    $ pip install mediapipe-silicon
  ``` 

  **Note**: Ignore the step of installing a specific version of `protobuz` from the README.md of the repository. Follow the steps on "INSTALL PROTOBUZ"
  section from this guide instead. 

  **Important**: Your environment has to be activated before installing `mediapipe-silicon`.