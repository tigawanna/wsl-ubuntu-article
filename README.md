
# Brief Intro

If you're reading this you're probably like me and develop on windows, it has served me right but I recently found out that you can't avoid Linux as a developer,
configuring a dual boot solution was the go-to solution for this for a while. 
but that comes with some limitations, for one you can only use one at a time and that was not an option when I was developing a server that was almost complete on windows until I had to add caching and Redis is a Linux only solution. 
My options were to clone the project into a Linux environment or find a way to run limited Linux which would let me run the server in windows and Redis on Linux then I discovered the windows subsystem for linux (WSL) which allows you to run Linux in windows and have access to the Windows file system and a parallel Linux file system , that was perfect for my needs 


The first step is installing wsl
Run the simple command 
```
wsl --install
```
And give it a minute to set up by default it installs the latest Ubuntu

> Note
>The above command only works if WSL is not installed at all, if you run wsl >--install and see the WSL help text, please try running wsl --list --online to >see a list of available distros and run wsl --install -d <DistroName> to install a >distro.
 To uninstall legacy WSLversion to install the latest
,[click here](https://docs.microsoft.com/en-us/windows/wsl/basic-commands#unregister-or-uninstall-a-linux-distribution)

>To change the distribution installed, enter: wsl --install -d <Distribution Name>. Replace <Distribution Name> with the name of the distribution you would like to install.
To see a list of available Linux distributions available for download through the online store, enter: wsl --list --online or wsl -l -o.
To install additional Linux distributions after the initial install, you may also use the command: wsl --install -d <Distribution Name>.
 Tip

>If you want to install additional distributions from inside a Linux/Bash command line (rather than from PowerShell or Command Prompt), you must use .exe in the command: wsl.exe --install -d <Distribution Name> or to list available distributions: wsl.exe -l -o.

## Configuring windows terminal with WSL2 and ubuntu

you'll need a terminal to use linux bt sadly window's default offerings are less than desirable, that's why they made windows terminal
[download](https://www.microsoft.com/store/productId/9N0DX20HK701)

Navigate to your terminal, click on the dropdown button next to the plus sign on the tab area to open the side panel
and add a new profile if wsl didf

Add save in your editor and exit



Once there you can go back ,click on the drop down button and select ubuntu to launch ubuntu terminal

Another optional modification you might want to make 
If you type ls you???ll notice the directory names area little hard to read because of the green background

Create an empty file color
```
touch color 
```
Type 
```
code .
```

Then add this into the file
```
#!/bin/bash

filename='.bashrc'
nuclr="LS_COLORS=\$LS_COLORS:'di=0;35:' ; export LS_COLORS"
echo $nuclr >> $filename
```
Save, run  <code>
chmod +x color 
</code>
to give it permission
Then execute it 
<code>./color</code>

Re open your windows terminal and if you launch ubuntu and type ls things will be better 

So far so good
Now you???ll be able to work from linux on your windows machine. just launch ubuntu navigate to directory you want to work in and type  
<code>code .</code> 
to open it in vs code  

## Configuring for c/c++
download gcc compiler and betty linter for c/c++ development
Type the following one by one

```
sudo apt install build-essential
``` 
```
sudo apt update
```
```
sudo apt-get install manpages-dev
```


Then to check if installed type
<code>gcc --version</code><br>

For the betty linter: 
 [Go to the betty repo:](https://github.com/holbertonschool/Betty)

And clone the repo<br>
<code>cd  Betty</code><br>
<code>sudo ./install.sh</code>



Create a file called betty and  paste in 
```
#!/bin/bash
# Simply a wrapper script to keep you from having to use betty-style
# and betty-doc separately on every item.
# Originally by Tim Britton (@wintermanc3r), multiargument added by
# Larry Madeo (@hillmonkey)

BIN_PATH="/usr/local/bin"
BETTY_STYLE="betty-style"
BETTY_DOC="betty-doc"

if [ "$#" = "0" ]; then
    echo "No arguments passed."
    exit 1
fi

for argument in "$@" ; do
    echo -e "\n========== $argument =========="
    ${BIN_PATH}/${BETTY_STYLE} "$argument"
    ${BIN_PATH}/${BETTY_DOC} "$argument"
done
```

Once saved, exit file and change permissions to apply to all users with chmod a+x betty
Move the betty file into <code>/bin/ directory </code> or somewhere else in your $PATH with 
```
sudo mv betty /bin/
```
You can now type <code> betty "filename" </code> to run the Betty linter!
and now you can compile and run linux c code on your windows machine