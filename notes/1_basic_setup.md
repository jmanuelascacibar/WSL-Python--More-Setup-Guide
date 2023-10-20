## 1. Basic Setup and Software Installation

When using the terminal, you're directly communicating with your computer, requesting it to carry out tasks, automate procedures, 
or execute scripts. This tool is indispensable, particularly in the realm of machine learning. Every cloud system operates on Linux, 
and eventually, you'll be working with them.
WSL is essentially Linux within your Windows system. The first step is to get it installed on your computer.
Follow these [steps](https://learn.microsoft.com/en-us/windows/wsl/install) and return when you're set to proceed.

When you type 'python' in the terminal and see a response similar to mine, it's a cause for concern. 
This indicates that there's a Python version already installed on our Linux system (system Python).

![](/images/image1.png)

`python3` refers to a Python version typically installed on Linux systems. It's crucial not to interfere with this specific installation. 
To determine which version you're currently using, you can utilize the `which` command.

![](/images/image2.png)

The optimal approach to installing Python is via a conda environment. For our purposes, we'll opt for mambaforge, which is a speedier variant of conda-forge.
You can fetch the latest release from[here](https://github.com/conda-forge/miniforge)

To begin, let's create a directory in our Linux system where we can download files from the internet.

![](/images/image3.png)

After you’ve created the directory:
1. Navigate to [mambaforge's release page](https://github.com/conda-forge/miniforge).
2. Locate the appropriate installer for your system (most likely the Linux version if you're working within a Linux environment).
3. Right-click on the link for the installer and select "Copy link address" or a similar option depending on your browser.

Once you have the link copied:
* Return to your terminal.
* Navigate to the directory you've just created using the cd command.
* Download the installer by executing `wget` follow of the link for the installer:

![](/images/image4.png)

The .sh file is a shell script that basically is a list of ordered shell commands. 
You can read what is inside using the `less` command

![](/images/image5.png)

Everything with a # is a comment. The rest are lines of code is going to run in order. 
Typing the command bash we are telling the terminal to run the shell script.

![](/images/image6.png)

Mambaforge doesn’t just install Python, it comes bundled with several essential libraries, making it a comprehensive environment for development. 

After the installation process completes, close your terminal and reopen it to ensure all changes take effect and the environment is properly initialized. 

![](/images/image7.png)

When you see `(base)` at the beginning of your terminal prompt, it indicates that you’re currently operating within the base environment of your conda
or mambaforge installation. 

To further validate that you’re using the Python version from this environment, run the following command.

![](/images/image8.png)

This should point to the Python binary located within the mambaforge directory, confirming that you’re indeed using the version from the environment. 

By installing Python and associated libraries within a mambaforge environment, you’re sandboxing them from the rest of your system.
Any changes, additions, or deletions within the environment won’t affect the system. 
If something goes awry or the environment becomes corrupted, you can simply delete it with `rm -rf mambaforge` and start a
fresh one without affecting the rest of your system. Also, it allows you to maintain multiple versions of Python and libraries without conflicts. 

As we said, Mamba is a powerful package manager. To see the available commands and options within the mamba environment simply type `mamba`. 

![](/images/image9.png)

This will display a list of everything you can do with mamba. Let’s install ipython, pytorch, and jupyter lab in our system.

To install `ipython` run `mamba install ipython` in your terminal. 

To install `pytorch`, we need to go to the [Pytorch official website](https://pytorch.org/get-started/locally/)

![](/images/image10.png)

Make sure you select the Linux tab and choose the configurations that match your system and needs. 
Although they will provide a conda command, mamba can use the same channels and packages as conda. 

`mamba install pytorch torchvision torchaudio -c pytorch`

To install JupyterLab  run `mamba install jupyterlab`

To verify that the installations were successful, you can import the libraries we've installed within `ipython`.

![](/images/image11.png)

The final point in this introduction pertains to setting up aliases. Aliases can be real-time savers, and they’re simple to establish. 
To ensure your aliases are always active each time you launch a new terminal, you should make modifications to the `.bashrc` file located in your home directory.

Open the file with `vim .bashrc` and add your desired alias `alias jl="jupyter lab --no-browser"`

![](/images/image12.png)

Now every time you type `jl` in the terminal, it will launch Jupyter Lab without opening the browser. 

## Terminal & System Shortcuts

- **Ctrl + D**: Closes most programs within your terminal.
- **Ctrl + R**: Initiates a reverse search. If the first result isn't what you're looking for, press Ctrl + R again to continue searching.
- **Ctrl + E**: Moves the cursor to the end of the line.
- **Ctrl + A**: Moves the cursor to the beginning of the line.
- **Win + TAB**: Opens an interface allowing you to create and switch between multiple virtual desktops. (It's beneficial to familiarize yourself with using virtual desktops.)
- **ALT + Enter**: Toggles full-screen mode.








