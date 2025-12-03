# Compile Python To Executable - PyInstaller





PyInstaller is a free and open-source program that lets you bundle a Python application and all its dependencies into a single package. This package can then be easily distributed and run by users without requiring them to have Python or any of its libraries installed on their systems.



**How does it work?**

- **Analyze your Python script:** PyInstaller reads your Python script and identifies all the modules and libraries that it needs to run.
- **Collect dependencies:** PyInstaller then collects copies of all those modules and libraries. This includes not only the Python standard library but also any third-party libraries that your script uses.
- **Package everything up:** Finally, PyInstaller packages all of the files together into a single executable file or a folder containing an executable file and its supporting files. This package can be run on any system that has the same operating system as the one where it was created.



**Benefits of using PyInstaller:**

* **Easy to distribute:** You can easily share your Python applications with others without worrying about whether they have the right dependencies installed.

- **No Python installation required:** Users don't need to have Python installed on their systems to run your application.
- **Standalone:** Your application is self-contained and doesn't rely on any external files or libraries.
- **Secure:** You can control exactly which libraries are included in your application, which can help to improve security.



Overall, PyInstaller is a powerful tool that can make it easy to distribute and run your Python applications.



Here are some additional resources that you may find helpful:

- **PyInstaller website:** https://www.pyinstaller.org/
- **PyInstaller documentation:** https://www.pyinstaller.org/

* Website:  [PyInstaller Manual](https://pyinstaller.org/en/stable/#)
* https://stackoverflow.com/questions/5458048/how-can-i-make-a-python-script-standalone-executable-to-run-without-any-dependen

(JGAI)



## Quick Start

> Install PyInstaller from PyPI:
>
> ```py
> pip install pyinstaller
> ```
>
> Go to your program’s directory and run:
>
> ```py
> pyinstaller yourprogram.py
> ```
>
> This will generate the bundle in a subdirectory called `dist`.
>
> ```py
> pyinstaller -F yourprogram.py
> ```
>
> Adding -F (or --onefile) parameter will pack everything into single "exe".
>
> ```py
> pyinstaller -F --paths=<your_path>\Lib\site-packages  yourprogram.py
> ```
>
> running into "ImportError" you might consider side-packages.
>
> ```py
>  pip install pynput==1.6.8
> ```
>
> still running into an  Import-Erorr - try to downgrade pyinstaller - see [Getting error when using pynput with pyinstaller](https://stackoverflow.com/questions/63681770/getting-error-when-using-pynput-with-pyinstaller)
>
> For a more detailed walkthrough, see the [manual](https://pyinstaller.readthedocs.io/).

[From Stack Overflow - PyInstaller](https://stackoverflow.com/questions/5458048/how-can-i-make-a-python-script-standalone-executable-to-run-without-any-dependen)