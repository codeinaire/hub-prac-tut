# New GIT repos from CLI!

I don't know about y'all, but I'm tired of having to go through the browser to create a new repo, all this switching of windows is such a bore, it interupts my workflow, and I don't really feel like An Actual Programmer (AAP) when I do it. Is there a better way? Can I get one step closer to the god-like powers of An Actual Programmer!? Why, yes, ofcourse there is and yes, ofcourse you can. The solution: The Command Line Interface (CLI)!

You must be wondering "Whaaaaaaaattttt... otherworldy magic have you summoned to assist in this task?". No magic, just the wonders of programming. If you want to get level up your CLI skills and get one step closer to being AAP all the while being able to create a brand new git repo from the CLI then read on!

## Intro

These will be the steps need to reach our end goal:

1) Install and configure [Go](https://golang.org/doc/install) - this is a prerequiste for the hub tool.
2) Install and configure [hub](https://github.com/github/hub) - this is the CLI tool that will give us the ability to create new repos from the CLI
3) Create local git repo and configure - this is when we'll be able to create new repos but, for now, have to configure each project to be able to push to these repos.

### Install & Config Go

I followed [this](http://www.hostingadvice.com/how-to/install-golang-on-ubuntu/) guide to install go on Ubuntu, however... I know most people in class use Mac so I've included the Mac guide below [this is the source](http://stackoverflow.com/questions/12843063/install-go-with-brew-and-running-the-gotour). Check it out if you're having any issues. I may be able to help, but I'm not on a Mac so it could be limited. The latest version of go is 1.8.1, so begone and install:

1) Create Directories

`$ mkdir $HOME/Go`
`$ mkdir -p $HOME/Go/src/github.com/user`

2) Setup your paths (sort of like setting local env.vars with mailgun)

`export GOPATH=$HOME/Go`  
`export GOROOT=/usr/local/opt/go/libexec`  
`export PATH=$PATH:$GOPATH/bin`  
`export PATH=$PATH:$GOROOT/bin`  

3) Install Go

`$ brew install go`

IThe main issue I found for me when installing on Ubuntu was a bit of confusion as to where to put my paths. The paths will be copied from step 2) and be pasted into your `.bashrc` or `.zshrc` (if you are using the oh-my-zsh terminal shell) file. To do this:

1) CD into your home directory and do a `$ atom/subl/<whatever-text-editor> .zshrc<OR>.bashrc` command to open up the file.
2) paste the paths from step 2) somewhere in the file and save.
3) close the file and terminal to make these values active.

Another issue I had with Ubuntu was that I had to install go from the binaries like this: `$ gvm install go<version-number> --binary`. However, I'm not sure Mac users will have this problem because of the magic of brew install.

To check the version of go installed do a `$ go version` and it will tell you the version installed. I'm not sure if this works on Mac.

So that's it for the installation of go. It was a slight pain on ubuntu, but probably because it was new to me. I hope it was easier on Mac. But it'll be worth it when, like magic (but not really), you'll start making BRAND NEW REPOS IN THE CLI!!

### Install & Config Hub

This part is much easier. Check out the [hub repo](https://github.com/github/hub/) for a detailed version of the instructions. For ease I've put the Mac installation instructions below. You're welcome.

1) `$ brew install hub`
2) `$ hub version`

Next we'll be aliasing hub to git so that when you type a `git <whatever command>` it'll basically be going through the hub tool instead of the git tool. Here is how we do that:

1) `$ hub alias` - in the terminal this will feed back to us a command that we can put in our `.bashrc` or `.zshrc` file, just like we did in step 2) of the go install. Copy this returned value. It should look something like this: `eval "$(hub alias -s)"`. Copy the entire line.
2) `$ atom/subl/<whatever-text-editor> .zshrc<OR>.bashrc` - so choose a text-editor to open the file up in and it'll be either `.zshrc` or `.bashrc` depending if you have oh-my-zsh installed or not.
3) Paste the returned value from step 1) into the file you just opened. Save and close it. Then close the terminal to apply the values.

You may not be able to see the files in your home directory. If you cannot use this: `$ ls -a`. But that is it for the install of Hub. Now to the last and exciting part: getting a new repo happening FROM THE CLI!!

### Create New Repo

I'm not really sure why there isn't a feature to create a new repo in the current CLI git tools, but what I've read about hub is that it creates a new remote repo through the api interface. I found one problem doing it like this: the beloved error message. I'm not exactly sure why we get the error, but that doesn't matter for now as there's a way around.

Here's the instructions to *finally* create a BRAND NEW REPO from your CLI:
1) `$ git init`
2) `$ git create <name-of-repo> -d <description-of-repo>` - you'll get an error here, but that's okay. The most important thing is that you have just created a brand new repo from the CLI. What does it feel like to be AAP!?? Browser repo creates are for noobs, right!?
3) `$ atom .` - here we'll config the our git config so we can start pushing stuff to it without getting errors.
4) Locate the `config` in the `.git` folder and open it.
5) Under `[remote "origin"]` you'll see something like `url = git@github.com:<your-user-name>/<name-of-repo>.git`. This is the offending line of code. You'll need to change it.
6) Change the line of code in step 5) to this: `url = https://<sign-in-email -address-for-github>@github.com/<username-for-git-hub>/<name-of-repo>.git`. This is the most important line of code here. Here is an example: `url = https://alucinare%40gmail.com@github.com/codeinaire/practice-repo.git` Notice that instead of having an `@` in my email I have a `%40`. This must replace the `@` sign for the sign in email to work. You can probably have it without that but in the CLI it'll just ask for your email address and password, instead of just your password. The rest is just my username and the name of my repo. Save your config file with this new line.

This is pretty much it. The next few step are just following the instructions from when you create a repo through the website. I'll list them for completeness, plus there's one that you don't need which I've noted as to why.

7) `$ echo "# practice-hub" >> README.md`
8) `$ git add README.md`
9) `$ git commit -m "Intial commit"` - usually after this you'll do this `git remote add origin https://github.com/codeinaire/practice-hub.git`, however, you don't need to do this as you've already added the remote origin in step 6). So you'll get an error if you try to run this command.
10) `$ git push -u origin master`

That's it for the git configuration.

### Finale

Well, that's it for the guide. You are now one step closer to being An Actual Programmer (AAP), who can wield the power of the CLI like a magician of yore.

I've always wanted to know how to create a repo in the CLI. It seems like a minor thing, but I believe this really helps to smooth out my workflow as I don't have to change to another window to create a repo. Plus I've gotten a better understanding about how git and the .zshrc profile works.

However, that's not all. The hub tool we installed does a bunch of other cool stuff. Check out the docs [here](https://hub.github.com/). I hope this guide has helped someone and that you'll start creates those repos from the CLI instead of from the pesky browser.

Happy Coding! :)
