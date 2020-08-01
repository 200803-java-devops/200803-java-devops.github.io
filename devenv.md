# Development Environment
To maximize resources and minimize troubleshooting, please perform a clean install or refresh of your operating system. Update your system, [Enable VT-x in BIOS](https://www.wikihow.tech/Enable-VT%E2%80%90x-in-BIOS) if possible, and uninstall all unnecessary programs. 

Your development environment should be set up for Java, Git, and Maven as soon as possible. In later weeks we will also require PostgreSQL, Docker, SSH, curl, and many more tools. Refer to this Readme or the links provided in each week's topic and resources document to keep updated on the latest tools and programs needed for project work. You will be responsible for maintaining your environment throughout the program.

# Windows
1. Install [Chocolatey](https://chocolatey.org):
    1. Open `Powershell` as an administrator and run:
        >Set-ExecutionPolicy AllSigned
    1. Then run:
        >Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    1. Open a new terminal as an administrator (or run `refreshenv`)
1. Install your tools:
    1. Git:
        >choco install git
    1. JDK 8:
        >choco install openjdk8
    1. Apache Maven:
        >choco install maven
    1. Visual Studio Code:
        >choco install vscode

# MacOS
1. Install [Homebrew for MacOS](https://brew.sh/):
    1. Open a terminal and run:
        >/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
1. Install your tools:
    1. Git:
        >brew install git
    1. JDK 8:
        >brew tap adoptopenjdk/openjdk
        >brew cask install adoptopenjdk8
    1. Apache Maven:
        >brew install maven
    4. Visual Studio Code:
        >brew tap caskroom/cask
        >brew cask install visual-studio-code

# Summary
To confirm all tools are properly installed and configured, be sure the following commands return no errors:
```bash
git -v
java -version
javac -version
mvn -v
code -v
```
