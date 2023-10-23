In this note, we'll explore how to configure Git for a version control system on your computer and synchronize it with GitHub..

## User and email

Before starting doing anything, , it's essential to let Git know your identity.

````
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
````

For more details, check out the official Git [documentation](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

To inspect or modify your username and email, you can edit the hidden `.gitconfig` file in your home directory.

````
$ vim .gitconfig
````


## Putting a repository in your  computer. Clone a repository

Git is a version control tool installed on your computer. To use it, simply type `git` into your terminal.

![](/images/note2/image1.png)

To clone a repository:

1. Navigate to your GitHub repository.
2. Click on the 'Code' button and copy the SSH link.

![](/images/note2/image2.png)

If you haven't configured Git on your computer, you might face permission issues when trying to clone using SSH. This arises because SSH relies on specific keys for authentication. While it's possible to clone someone else's repository using HTTPS, it's recommended to use SSH when you own the repository—it's more secure and convenient.

SSH doesn't rely on passwords. Instead, it uses a private key (stored on your computer) and a corresponding public key (shared with GitHub). This ensures that while you can interact with GitHub, no one can access your computer using the keys.

Generate your SSH keys:

````
$ ssh-keygen
````

Simply press 'Enter' multiple times to generate the private (`id_rsa`) and public (`id_rsa.pub`) keys in your home directory.

To view your public key:

````
$ cat .ssh/id_rsa.pub
````


Next, go to GitHub:

1. Click on 'Settings'.
2. Navigate to the 'SSH and GPG keys' section. ![](https://chat.openai.com/c/images/note2/image3.png)
3. Click 'New SSH key', provide a title, and paste your public key.

![](/images/note2/image3.png)

Now, try cloning your repository again.

![](/images/note2/image4.png)

The repository is cloned!

![](/images/note2/image5.png)
## Committing Changes to Git

To contribute to Git, you'll need to commit your changes:

1. Check status: `git status`
2. Stage changes: `git add readme.md`
3. Commit changes: Either `git commit` or `git commit -am 'your message here'`
4. Push to repository: `git push`

## Terminal Shortcuts

- `cd -` : Return to the previous directory
- `pushd` : Remember the current directory; `popd` : Return to that directory
- `cd ..` : Navigate to the parent directory
## TMUX

[Documentation](https://man.openbsd.org/tmux)

**Managing Windows and Panes:**

- `ctrl + B + %` : Create a new vertical pane
- `ctrl + B + "` : Split pane horizontally (top and bottom)
- `ctrl + B + ARROWS` : Navigate between panes
- `ctrl + B + Z` : Zoom in/out of the current pane

**Session Management:**

- `ctrl + B + D` : Detach from the current tmux session 
- `ctrl + B + s` or simply `tmux attach` from the terminal to attach



`ctrl + B + c` create a new window
`ctrl + B + p` return to the previous window
`ctrl + B + <number>` go to the number window
















