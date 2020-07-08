Laptop
======

Laptop is a script to set up an OS X computer for web development, and to keep it up to date.

It can be run multiple times on the same machine safely. It installs, upgrades, or skips packages based on what is already installed on the machine.

Requirements
------------

We support:

* [macOS Catalina](https://www.apple.com/osx/)
* macOS Sierra (10.12)
* OS X El Capitan (10.11)
* OS X Yosemite (10.10)
* OS X Mavericks (10.9)

Older versions may work but aren't regularly tested. Bug reports for older
versions are welcome.

Install
-------

Begin by opening the Terminal application on your Mac. The easiest way to open
an application in OS X is to search for it via [Spotlight]. The default
keyboard shortcut for invoking Spotlight is `command-Space`. Once Spotlight
is up, just start typing the first few letters of the app you are looking for,
and once it appears, press `return` to launch it.

In your Terminal window, copy and paste the command below, then press `return`.

```sh
bash <(curl -s https://raw.githubusercontent.com/cisagov/laptop/master/laptop)
```
The [script](https://github.com/cisagov/laptop/blob/master/mac) itself is
available in this repo for you to review if you want to see what it does
and how it works.

Note that the script will ask you to enter your OS X password at various
points. This is the same password that you use to log in to your Mac.
If you don't already have it installed, GitHub for Mac will launch
automatically at the end of the script so you can set up everything you'll
need to push code to GitHub.

**Once the script is done, make sure to quit and relaunch Terminal.**

More [detailed instructions with a video][video] are available in the Wiki.

It is highly recommended to run the script regularly to keep your computer
up to date. Once the script has been installed, you'll be able to run it
at your convenience by typing `laptop` and hitting `return` in your Terminal.

[Spotlight]: https://support.apple.com/en-us/HT204014
[video]: https://github.com/18F/laptop/wiki/Detailed-installation-instructions-with-video

What it sets up
---------------

* [ChromeDriver] for headless website testing
* [chruby] for managing [Ruby] versions (or, when using a fish shell, [rbenv])
* [Docker] for all your containerization needs
* [GitHub Desktop] for setting up your SSH keys automatically
* [Homebrew] for managing operating system libraries
* [Homebrew Services] so you can easily stop, start, and restart services
* [nvm] for managing Node.js versions if you do not have [Node.js] already installed (Includes latest [Node.js] and [NPM], for running apps and installing JavaScript packages)
* [pyenv] for managing Python versions if you do not have [Python] already installed (includes the latest 3.x [Python])
* [ruby-install] for installing different versions of Ruby
* [Virtualenv] for creating isolated Python environments (via [pyenv] if it is installed)
* [Virtualenvwrapper] for extending Virtualenv (via [pyenv] if it is installed)
* [Zsh] as your shell, if you choose to switch from Bash

[Bundler]: http://bundler.io/
[ChromeDriver]: http://chromedriver.chromium.org/
[chruby]: https://github.com/postmodern/chruby
[Docker]: https://www.docker.com/
[Homebrew]: http://brew.sh/
[hub]: https://github.com/github/hub
[n]: https://github.com/tj/n
[Node.js]: http://nodejs.org/
[NPM]: https://www.npmjs.org/
[Python]: https://www.python.org/
[pyenv]: https://github.com/yyuu/pyenv/
[rbenv]: https://github.com/rbenv/rbenv
[Ruby]: https://www.ruby-lang.org/en/
[ruby-install]: https://github.com/postmodern/ruby-install
[Virtualenv]: https://virtualenv.pypa.io/en/latest/
[Virtualenvwrapper]: http://virtualenvwrapper.readthedocs.org/en/latest/#
[Zsh]: http://www.zsh.org/

It should take less than 15 minutes to install (depends on your machine and
internet connection).

Customize in `~/.laptop.local` and `~/Brewfile.local`
-----------------------------------------------------

Your `~/.laptop.local` is run at the end of the `mac` script.
Put your customizations there. If you want to install additional
tools or Mac apps with Homebrew, add them to your `~/Brewfile.local`.
This repo already contains a [.laptop.local] and [Brewfile.local]
you can use to get started.

```sh
# Go to your OS X user's root directory
cd ~

# Download the sample files to your computer
curl --remote-name https://raw.githubusercontent.com/cisagov/laptop/master/.laptop.local
curl --remote-name https://raw.githubusercontent.com/cisagov/laptop/master/Brewfile.local
```

It lets you install the following tools and apps:

* [VSCode] - Microsoft's open source text editor
* [Atom] - GitHub's open source text editor
* [Sublime Text 3] for coding all the things
* [Vim] for those who prefer the command line
* [Exuberant Ctags] for indexing files for vim tab completion
* [Firefox] for testing your website on a browser other than Chrome
* [iTerm2] - an awesome replacement for the OS X Terminal
* [reattach-to-user-namespace] to allow copy and paste from Tmux
* [Tmux] for saving project state and switching between projects
* [Spectacle] - automatic window manipulation

[.laptop.local]: https://github.com/cisagov/laptop/blob/master/.laptop.local
[Brewfile.local]: https://github.com/cisagov/laptop/blob/master/Brewfile.local
[VSCode]: https://code.visualstudio.com/
[Atom]: https://atom.io/
[Sublime Text 3]: http://www.sublimetext.com/3
[Exuberant Ctags]: http://ctags.sourceforge.net/
[Firefox]: https://www.mozilla.org/en-US/firefox/new/
[iTerm2]: http://iterm2.com/
[reattach-to-user-namespace]: https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard
[Tmux]: https://tmux.github.io/
[Vim]: http://www.vim.org/
[Spectacle]: https://www.spectacleapp.com/

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo` and `gem_install_or_update` can be used
in your `~/.laptop.local`.

What about background services (Redis, Postgres, MySQL, etc.)?
----------------------------------------------------------
The script does not automatically install services like databases because you
may not need any particular one, or you may need specific versions, not just
the latest.  For services, we recommend using [Docker].  For example, you can
use the [`docker run`] command to start a service in a container and make the
container's port available to your local machine:

```shell
docker run -p 5432 postgres:10.6
```

You can also use [Docker Compose] to define your app's containers and their
relationships, cutting out the need to manually setup each service.

[Docker Compose]: https://docs.docker.com/compose/
[docker run]: https://docs.docker.com/engine/reference/run/#expose-incoming-ports

How to switch your shell back to bash from zsh (or vice versa)
--------------------------------------------------------------
1. Find out which shell you're currently running: `echo $SHELL`
2. Find out the location of the shell you want to switch to. For example, if
   you want to switch to `bash`, run `which bash`.
3. Verify if the shell location is included in `/etc/shells`.
   Run `cat /etc/shells` to see the contents of the file.
4. If the location of the shell is included, run
   `chsh -s [the location of the shell]`.
   For example, if `which bash` returned `/bin/bash`, you would run
  `chsh -s /bin/bash`.

   If the location of the shell is not in `/etc/shells`, add it, then run the
   `chsh` command.
   If you have Sublime Text, you can open the file by running
   `subl /etc/shells`.
5. Quit and restart Terminal (or iTerm2), or open a new tab for the new shell
   to take effect.

Whether you're using bash or zsh, we recommend installing the latest versions
with Homebrew because the versions that came with your Mac are really old.
```
brew install bash
```
or
```
brew install zsh
```

Credits
-------

The cisagov laptop script is based on and inspired by [18F's laptop](https://github.com/18f/laptop) script, which is based on and inspired by [thoughtbot's laptop](https://github.com/thoughtbot/laptop) script.

### Public domain

thoughtbot's original work remains covered under an [MIT License](https://github.com/thoughtbot/laptop/blob/c997c4fb5a986b22d6c53214d8f219600a4561ee/LICENSE).

CISA and 18F's work on this project is in the worldwide [public domain](LICENSE.md), as are contributions to our project. As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
