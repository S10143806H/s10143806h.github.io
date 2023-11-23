# Build Documentation with <font color="#219EB6">Sphinx</font> + <font color="#EF4E0A">ReadtheDoc</font>

:information_source:  Click **[HERE](https://hackmd.io/@accomdemy/SJ5mlE7-K#/)** to open Presenter View


---

## <font color="#219EB6">Content</font>
0. What is ReadtheDocs
1. Build Environment 
2. Write your 1st Documentation 
3. Host on GitHub
4. Display in ReadtheDoc
5. Multiple Language Support

---

## <font color="#219EB6">0. What is ReadtheDocs</font>
#### <font color="#EF4E0A">ReadtheDocs</font>
> ReadtheDocs simplifies software documentation by automating 
> building, versioning, and hosting of your docs for you；

Link: [Read the Docs Homepage](https://readthedocs.org/)

---

## <font color="#219EB6">0. What is ReadtheDocs</font>
#### <font color="#EF4E0A">Sphinx</font>

Link: [Sphinx Python Documenation Generator](https://www.sphinx-doc.org/en/master/0)

#### <font color="#EF4E0A">reStructuredText</font>
- plaintext
- markup language

Link: [reStructuredText](https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html)

---

## <font color="#0080FF">1. Build Environment (1)</font>

#### Required Softwares (for Windows)
- [Python 3.x](https://www.python.org/downloads/)
- pip
- [Cygwin](https://cygwin.com/install.html)
- [VS Code](https://code.visualstudio.com/download)

---

## <font color="#0080FF">1. Build Environment (2)</font>

Upon install Python3, type the comments below in your comment prompt to check whether <font color="#EF4E0A">`Python`</font> and <font color="#EF4E0A">`Pip`</font> has been installed correctly:

``` bash
python --version
```

``` bash
pip --version
```

install <font color="#EF4E0A">`Sphinx`</font> using <font color="#EF4E0A">`pip`</font> tool using the code:

``` bash
pip install sphinx
```

---

## <font color="#0080FF">1. Build Environment (3)</font>

Executes the comment below in a specific folder to further create a sphinx docs project:

``` bash
sphinx-quickstart
```

![](https://i.imgur.com/zdEaoIw.png)

---

## <font color="#0080FF">1. Build Environment (4)</font>

Opens Cygwin and install <font color="#EF4E0A">`make`</font> & <font color="#EF4E0A">`chere`</font> packages accordingly.
Runs <font color="#EF4E0A">`make html`</font> in the same file path, then you will find your first readthedoc documentation.


![](https://i.imgur.com/JpTsUe8.png)

---

## <font color="#0080FF">1. Build Environment for MacOS (1) </font>

#### Required Softwares (for MacOS)
- [Python 3.x](https://www.python.org/downloads/)
- [Homebrew](https://brew.sh)
- Terminal
- Xcode with Command Line Tool

---
## <font color="#0080FF">1. Build Environment for MacOS (2) </font>
Upon installed python3, type the following command in Terminal to check if it is installed correctly:
``` 
python3 --version
```
If it is correctly installed, you will be able to see the version number of your python3.

---
## <font color="#0080FF">1. Build Environment for MacOS (3) </font>
To install Homebrew to MacOS, type the following command in your Terminal
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---
## <font color="#0080FF">1. Build Environment for MacOS (4) </font>
You can download Xcode from Apple store. If Command Line Tools is not installed together with your Xcode, you can use the following command to install Command Line Tools:
```
xcode-select --install
```

---
## <font color="#0080FF">1. Build Environment for MacOS (5) </font>
After the installation of all required softwares, install <font color="#EF4E0A">`Sphinx`</font> using <font color="#EF4E0A">`brew`</font> tool using the command:
```
brew install sphinx-doc
```
At the end of the installation, you may see a warning that shows sphinx is "keg-only" and is not by default put in your <font color="#EF4E0A">`PATH`</font>, use the follwoing command to link it to <font color="#EF4E0A">`PATH`</font>:
```
brew link sphinx-doc --force
```
Use below command to check if you have successfully installed <font color="#EF4E0A">`sphinx`</font>:
```
sphinx-build --version
```

---
## <font color="#0080FF">1. Build Environment for MacOS (6) </font>
Execute the following command in a specific folder to create a sphinx docs project:
```
sphinx-quickstart
```
![](https://i.imgur.com/GIn6lrs.png)

---
## <font color="#0080FF">1. Build Environment for MacOS (7) </font>
Open Terminal in the same folder that contains makefile, and execute the command <font color="#EF4E0A">`make html`</font>, now you will find your first ReadtheDocs documentation in /build/html/index.html
![](https://i.imgur.com/CKkBHx2.png)

---

## <font color="#0080FF">2. Write your 1st Documentation</font>

Please edit in `index.rst` and `make html`
You will find the expected html view in the `build` folder, and under the `html` folder, you can see there is a file name called `index.html`.

![](https://i.imgur.com/INVniCj.png)

---

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

1. Host your locally created sphinx files into a specific GitHub repository
2. Create an account in [ReadtheDocs](https://readthedocs.org/) and linked it with your GitHub account
3. Create new project in ReadtheDocs by importing from your GitHub repository

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

* At the homepage, click your profile that is located at the top right.

![](https://i.imgur.com/GADyzgT.png)

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

* Press **Import a project**

![](https://i.imgur.com/JQJSvuk.png)

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

* You will see the whole list of project that are in your Github. Click the **+** beside the repository that you want to import to ReadtheDocs.

![](https://i.imgur.com/TazogTu.png)

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

* Fill in all the required details of your projects and click **Next**.

![](https://i.imgur.com/5tiiIEU.png)

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

4. Wait until the build process is done. A `Passsing` means the process is successful while a `Failing` means that something have gone wrong or any setup is wrong during the process.

![](https://i.imgur.com/KJG4sKk.png)

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

* In the event when the build process fails. You can analyze the errors that have caused the process to fail. By going into the project and then go into **Builds** where you can see the details of all the passed or failed processes for the particular project.

![](https://i.imgur.com/p86qCO5.png)
![](https://i.imgur.com/YASIK7A.png)

----
## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

* This is an example of how the error message looks.

![](https://i.imgur.com/DAtV8TT.png)

----
## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>

5. To take a look at the ReadtheDocs, press `View Docs`

![](https://i.imgur.com/wRVAXpj.png)
 

----

## <font color="#0080FF">3&4. Host on GitHub & Display in ReadtheDocs</font>
Now your file is fully uploaded into ReadtheDocs server and can be viewed by everyone that knows your hyperlink.

---

## <font color="#0080FF">5. Multiple Language Supporting</font>

### <font color="#EF4E0A">Method 1: Dual Language Supporting</font>

1. Create another sphinx folder locally with language setting changed to another language.

----

2. Manually import the newly created folder into the same GitHub repository
![](https://i.imgur.com/45IAIFw.png)

----

3. In ReadtheDocs, modify path to <font color="#EF4E0A">`conf.py`</font> tab, language settings and translation bar
    * First go to the <font color="#EF4E0A">`Admin`</font> tab. Then under the <font color="#EF4E0A">`Admin`</font> tab tab change the language to the language that you want to change to.
    ![Imgur](https://i.imgur.com/H7BjVvv.png)

----

* Next go to the *Advanced Settings* tab and under the *Default Setting*, and *Python Configuration File* enter the path of the correct path to conf.py and save.
![](https://i.imgur.com/mIIOWJd.png)

----

4. After that, go to *translations* and press **Add** 
![](https://i.imgur.com/wR3BzGg.png)

----

5. Wait until the build process is finished, then you are able to view the dual language files online

---
### <font color="#EF4E0A">Method 2: Dual Language Supporting</font>

![](https://i.imgur.com/REvNkXU.png)
.pot portable object template
.po  portable object files (for translator)
.mo machine object files

---
Step 1.

`pip install sphinx-intl`

---
Step 2. Add configuration to `conf.py`
```
locale_dirs = ['locale/'] #path is example but not recommended.
gettext_compact = False   #optional 
```
---
Step 3. Extract translatable messages into pot files.

`$ make gettext`
* The generated `.pot` files will be placed in the `build/gettext` directory.

---
Step 4. Generate `.po` files
We will use the pot files generated in the above step.

`$ sphinx-intl update -p build/gettext -l zh_CN -l zh_TW`

Once completed, the generated `.po` files will be placed in the below directories:

* `../locale/zh_CN/LC_MESSAGES/`
* `../locale/zh_TW/LC_MESSAGES/`

---
Step 5. Translate `.po` files

---
Step 6 Build translated document

`make -e SPHINXOPTS-" -D language='zh_TW'html`

## Live Streaming Records

- [0826 Session 1](https://www.facebook.com/groups/accomdemy/permalink/1700813616775103/)
- [0902 Session 2](https://www.facebook.com/628761374/videos/2889390487982375/)



## References

- [How to add **toggle** button for Sphinx?]()
- [How to add **copy** button for Sphinx?](https://stackoverflow.com/questions/39187220/how-to-add-a-copy-button-in-the-code-blocks-for-rst-read-the-docs)
- [How to **highlight code syntax** for Sphinx?]()
- [How to add more than 2 languages for Sphinx RTD]()
- [How to clear warning when build on RTD online environment]()
