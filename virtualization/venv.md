Using a virtual environment for a particular project
=======================================================

Why to use a virtual environment in Python?
-------------------------------------------

The main reason is to avoid a global mess with different versions of Python non-standard packages across multiple projects.

In virtual environment you only install the necessary packages locally for a particular project while keeping your global Python installation intact.


Setting up a virtual environment
--------------------------------

1. _cd_ to the project directory.
2. a) Create a new virtual environment and use the same version of Python added to _PATH_.

    __Windows OS__:
    ```shell
    python -m venv env
    ```

    __Linux/UNIX__:
    ```shell
    python3.9 -m venv env
    ```

    __OR__

    b) Create a new virtual environment and use a different version of Python.

    __Windows OS__:
    ```shell
    python -m pip install virtualenv
    virtualenv --python="C:\Program Files\Python39\python.exe" env
    ```

    __Linux/UNIX__:
    ```shell
    sudo pip install virtualenv
    virtualenv --python=/opt/python-3.9/bin/python env
    ```

3. Activate the virtual environment.

    __Windows OS__:
    ```shell
    .\env\Scripts\activate
    ```

    __Linux/UNIX__:
    ```shell
    source env/bin/activate
    ```

4. Do whatever you need (install requirements.txt, run scripts etc.)
5. Deactivate the virtual environment.
    ```shell
    deactivate
    ```

Using a Python virtual environment with sudo on Linux
-----------------------------------------------------

* __The problem:__

    The _sudo_ command will switch to a version of Python accessible on _PATH_ instead of your virtual environment.


* __The solution:__

    Call your Python scripts using the full path of the Python executable e.g.
    ```shell
    sudo ./env/bin/python3.9 my-script.py
    ```

    In this case, you can skip the activation/deactivation steps.
