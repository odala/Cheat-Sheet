# Linux

## Connect to home directory
1. Press Ctrl + l in the filedirectory.
2. Write smb://sambaad.stud.ntnu.no/odala
3. Press enter

## Connect to server at NTNU
Write the following in the terminal:

    ssh -X odala@login.stud.ntnu.no

| Command   | Action           |
| :-------: |:----------------:|
| `ls`      | list content of current directory |
| `cd`      | change directory      |  
| `cp`      | copy file / directories      |
| `rm`      | remove (delete) files / directories |

To inspect the content of a file:

        less
        more
        cat

To edit a file:

        vim / gvim
        emacs (-nw no window)



## Run terminal in the background with tmux
Take a look at: [tmux shortcuts & cheatsheet](https://gist.github.com/MohamedAlaa/2961058 "tmux")

start new:
  
    tmux

start new with session name:

    tmux new -s myname

attach:

    tmux a  #  (or at, or attach)

attach to named:

    tmux a -t myname

list sessions:

    tmux ls

detach:

    ctrl + b + d
