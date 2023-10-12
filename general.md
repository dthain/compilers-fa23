# General Submission Instructions

## Standard Build Environment

To ensure a consistent environment between development and grading,
please use the standard CSE student machines (RHEL8) to build and test your code.
These are `student10.cse.nd.edu` through `student13.cse.nd.edu` and can be
accessed via ssh.  
These machines are using gcc-8.5.0, flex-2.6.1, and bison-3.0.4.
Use `which gcc` to double check that you are using the standard `/usr/bin/gcc`
and have not otherwise modified your PATH for another class.

**If you are using your laptop or another computer to develop your code,
then you are responsible for checking that it works correctly on the standard
student machines.  Your work will be graded on those machines.**

## Code Organization

To ensure that you get off on the right foott (and we are able to understand your code)
you are required to use the standard [starter code](http://github.com/dthain/compilerbook-starter-code)
which defines structures like `decl`, `expr` and so forth.  You are welcome to add files,
fields, and functions as you like, as long as the general purpose of these structures remains.

Your code must include a `Makefile` such that when you type `make`, the entire compiler (so far)
is built and produces a program called `bminor`. Each assignment page will specify what arguments are required to call it.
Likewise, `make clean` should remove all intermediate object files, automatically generated code, and so forth.

## Getting Started with Git

[Git](https://git-scm.com/) is a version control tool that allows you to save and collaborate on programming projects. In Git, your code is saved in two different locations--the local copy and the remote copy.

### Make a Remote Copy

1) First make sure you are logged into Github then go to the [starter code](http://github.com/dthain/compilerbook-starter-code) and click the green "use this template" button. If you don't see the button you likely aren't logged in.

2) Use your netid followed by whatever you'd like as the repository name. For example: `YOURNAME-compiler`

3) Make sure your repository is **PRIVATE** not public, then click the green "Create repository from template" button.

5) Go into your repository settings on the right side of the screen then click on "Collaborators". Add `colinthomas-z80`, `David-Simonetti-ND` and `dthain` as contributors, so that we can see and grade your submission.

7) Go back to the repository main page and click the green "code" button then copy the URL under the "SSH" tab. The URL should look something like this:
`git@github.com:YOURNAME/YOURNAME-compiler.git`. If you see a yellow box asking you to create public ssh keys, follow the instructions to do so.

### Tell Us About the Remote Copy

1) Use [this form](https://forms.gle/DsLqr4zGxV54L6g48) to give use the URL of your repository.  (Just do this once for the first assignment.)

### Make a Local Copy

1) In a terminal, navigate where you'd like the project directory to be.

2) Using the url you copied run the following command. Because the repository is private you will have to enter your GitHub username and password:
`git clone <url>`

3) Navigate into the directory and open the README.md file with your favorite text editor. Make a change to the title then save the file.

4) In your terminal run `git add README.md`

5) Run `git commit -m "Edit readme"`

6) Run `git push -u origin master` 

## Turning In Code to Github

1) Make sure that all files that you have changed are added with `git add`, committed with `git commit`, and pushed with `git push`.

2) Go back to the link of your github repository. Make sure you refresh your page. **If everything went well you should see all of your changes.**

3) On the righthand side under "Releases", click "Create new release"

3) Click "Choose a new tag", type "encode" (or "scan", "parse", "print", "typecheck" or "codegen" for later assignments) then click "Create new tag"

4) Click "Publish release" at the bottom and you're done!

## Double Checking Your Submission

There are two ways to check your submission: on GitHub and locally.

### On GitHub
To double check your submission on GitHub, you can navigate to the repository on GitHub and make sure the files you changed locally are also changed on GitHub.

### Locally
To double check your submission locally:

1) Copy the url of your GitHub repository

2) In a terminal, navigate where you'd like the clean project directory to be

3) With a new name for the repository, run `git clone <url>`. **If a directory with the repository name already exists, you'll have to run `git clone <url> <name>` where `<name>` is a different from the original repository name.**

4) Navigate into your newly cloned repository and double check that your code builds, runs, and passes all the tests.
