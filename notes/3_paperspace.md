# Paperspace FastAi setup

In this note, we'll explore how to set up a Paperspace machine. The allure of Paperspace lies in its ability to provide reasonably fast machines at an affordable price, offering an experience akin to using your personal computer. 

Below are my instructions on setting up a configuration that symlinks to our persistent storage. This ensures we don't lose our configuration when starting a new session. Note: I'm using a pro account. 

### Paperspace

We are going to start creating a new project, followed by a notebook, that we'll populate it with fastai. 

![](/images/note3/image4.png)

Choose the machine you prefer, and then click at the bottom of Jupyter Lab.

![](/images/note3/image4-1.png)

### Persistent storage

Paperspace incorporates the concept of persistent storage, represented by the directory named `/storage`. This directory houses your persistent storage and is ideal location for installing conda libraries. Any content saved in this directory is accessible across every notebook (server) you generate. Therefore, if you need consistent access to specific libraries across all your notebooks, place them in this directory. 

The directory `/notebooks` also serve as persistent storage but it's specific to the individual notebook. If you delete a notebook it will delete its content. 

### Pip install setup

You can install new libraries using pip or conda. When using `pip install` libraries are place in `.local ` within our home directory. To ensure these libraries are available in subsequent sessions, we should relocate `.local` to persistent storage.

We are going to create a directory `config` in the persistent storage and we are going to relocate `.local` there.

```
mkdir config
mv .local /storage/config/
```

The idea now is to symlink .local to the home directory from the persistent storage. 

```
ln -s /storage/config/.local
```

![](/images/note3/image13.png)

Creating a symlink works perfectly for the current instance. However, for future sessions, we must execute a script to establish the symlink.

To solve this, we'll draft a script named `pre-run.sh` inside the `/storage` directory. Create the script using:

```
vim /storage/pre-run.sh
```

To specify this is a bash script, include the following at the start: `#!/bin/bash` 
If you are unsure about the location of bash, you can verify it with: `which bash`

Inside the script, first ensure you're in the home directory by executing `cd`.
Subsequently, remove any existing `.local` directory and create a symlink for the `.local` directory from persistent storage. To conclude the script, append `cd notebooks` to always start the session in the `notebooks` directory.  

![](/images/note3/image14.png)

You can attempt to execute the script using:  `./pre-run.sh`. However, it may not run immediately due to permission constrains. To grant the necessary permissions use: `chmod 744 pre-run.sh`.

Here:
* `7` grants read, write, and execute permissions for the user.
* The first `4` permits read access for the group.
* The second `4` permits read access for all users. 

### SSH Keys

Having established the process above, you may be pondering the subsequent steps. A great progression would be replicating the process for `ssh keys` and the mamba installer. 

Firstly, we need to create a directory to store our keys. Typically, these keys are stored in the home directory under a hidden `.ssh` folder: `mkdir .ssh`

Upload the keys from your computer to the Paperspace notebook and then transfer both public and private keys to the newly-created `.ssh` folder in your home directory. 

By default, the `.ssh` directory shouldn't be accessible to anyone. Hence, we need to modify its permissions: `chmod 700 .`

The `700` permission grants full access to the user and restricts everyone else from the directory. 

For the private key, `id_rsa`, to make it readable and writable: `chmod 600 id_rsa`

For the public key, ensure it's readable and writable for the user but only readable for everyone else: `chmod 644 id_rsa.pub`

To verify that our configuration works, test it with: `ssh git@github.com`.

You should receive a response like:

```
"Hi jmanuelascacibar! You've successfully authenticated, but GitHub does not offer shell access."
```

Lastly, relocate the `.ssh` directory to the storage folder and append the symlink instructions to the `pre-run.sh` script. 

![](/images/note3/image15.png)

### `.gitconfig` setup

To ensure integration with GitHub, it's essential to symlink the `.gitconfig` file. This enables your push changes to your GitHub account.

Begin by setting up your email and username for the machine 

```
git config --global user.email 'email@email.com' 

git config --global user.name 'username'
```

After the above step a new `.gitconfig` file will appear in your home directory. This file ocntains your Git configuration settings. 

Relocate the `.gitconfig` file to the persistent storage to safeguard your configurations.

```
mv .gitconfig /storage/config/
```

Modify the `pre-run.sh` to delete any existing `.gitconfig` in the home directory and establish a symlink to the one in persistent storage. 

```
rm -rf .gitconfig 
ln -s /storage/config/.gitconfig .gitconfig
```

Now, each time you initiate a new session, the symlink ensures you're always using your personalized Git configurations.

### Mamba setup

We'll frequently use mamba due to its advantage over Conda.  Fortunately, Paperspace has already integrated mamba into our server. However, it's crucial to remember that any libraries you install will be removed once the session ends. To retain our installations, we'll set up dedicated folder for mamba, install a fresh version mamba within this folder, transfer the folder to the storage directory, and then create a symlink back to the home directory. It's a familiar approach by now. Also, it's essential that the new mamba directory is included in our path. 

Create a directory for Mamba. Much like we did with `.local`, let's set up a directory for mamba. 

```
mkdir mamba
```

Install a fresh version of Mamba in the directory we just created.

```
mamba install -p ~/mamba mamba
```

Update the PATH for the new mamba directory. Navigate to `.bash.local` in storage and adjust the path to point to our fresh mamba directory.

![](/images/note3/image20.png)


To confirm that the path has been updated run `echo $PATH`

![](/images/note3/image21.png)

Move the Mamba directory to Storage.
```
mv mamba /storage/config/
```

Update the `pre-run.sh` script to include a symlink to the new `mamba` directory.

![](/images/note3/image22.png)


