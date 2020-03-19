# Linux 2 WinPath 
This is a bash script that turns linux paths into windows paths. It only works if you are cd'd into the windows file system. Or rather, the paths it generates wouldn't make sense.  There are probably bugs and I wouldn't recommend using it for anything beyond casual use.

I might just be bad at googling, but while I found plenty of people who wanted to do the opposite of this (windows path > linux path), I couldn't find anyone who had made a quick and easy way to do the opposite (linux path > windows path). At my job I use WSL, and this helps my workflow. Hopefully it helps someone else. If this functionality exists in a more robust form elsewhere, I'd like to know.

I also added some ascii graphix for fun.

## Usage
#### Set Alias

```
alias winpath='/mnt/c/users/chrisj/bash_scripts/getWinPath.sh'
```
#### Command: winpath [some directory]
```

           |: || :||: || :||: || :||: || :||: || :||: || :||: || :||: || :||: |
          /   //  //  //  //  // /mnt/c/Users/[you]/Linux2WinPath/ //  //  //  //  // 
          |   ||  ||  ||  ||  ||           [to]        [:::::::::::::::::::::::::::>>
          \   \\  \\  \\  \\  \\ "c:\Users\[you]\Linux2WinPath\"   \\  \\  \\  \\  \\
           | :||: || :||: || :||: || :||: || :||: || :||: || :||: || :||: ||: |

              /= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =\
             /= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =\
            ||                                                               ||
            ||            Windows Path copied to clipboard                   ||
            ||                                                               ||
             \= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =/
              \= = = = = = = = = winpath -h for help = = = = = = = = = = = =/
               \= = = = = = = = = = = = = = = = = = = = = = = = = = = = = =/


```

#### with or without quotes.
#### no argument gives the current directory.
```

           \\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\
           //\                                                                /\//\/
           \\/  Usage:                                                        \/\\/\
           //\  [no arg] ... Copies windows path of current directory         /\//\/
           \\/  -nq ...... Copies windows path without surrounding quotes     \/\\/\
           //\                                                                /\//\/
           \\/  *Path must be inside windows filesystem.                      \/\\/\
           //\      e.g. /mnt/c/users/[you]/Desktop/somefile.txt              /\//\/
           \\/                                                                \/\\/\
           //\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\/


```

## Source:

```
if [[ "$1" == -* ]]; then
    filePath=$2
    flag=$1
else
    filePath=$1
    flag=$2
fi
if [ "$flag" = "-h" ]; then
    echo ""
    echo "           \\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\\/\\"
    echo "           //\                                                                /\//\/"
    echo "           \\\/  Usage:                                                        \/\\\/\\"
    echo "           //\  [no arg] ... Copies windows path of current directory         /\//\/"
    echo "           \\\/  -nq ...... Copies windows path without surrounding quotes     \/\\\/\\"
    echo "           //\                                                                /\//\/"
    echo "           \\\/  *Path must be inside windows filesystem.                      \/\\\/\\"
    echo "           //\      e.g. /mnt/c/users/[you]/Desktop/somefile.txt              /\//\/"
    echo "           \\\/                                                                \/\\\/\\"
    echo "           //\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\//\/"
    echo ""
    exit 0
fi

currDir=$PWD
path="${currDir}/${filePath}"

replacement=''
winPath=$(echo $path | sed -e "s/\/mnt\//${replacement}/g" | sed 's/\//:\//')
if [ "$flag" != "-nq" ]; then
    winPath="\"${winPath}\""
fi

winPath=$(echo $winPath | sed 's/\//\\/g')
echo ""
echo "           |: || :||: || :||: || :||: || :||: || :||: || :||: || :||: || :||: |"
echo "          /   //  //  //  //  // ${path} //  //  //  //  // "
echo "          |   ||  ||  ||  ||  ||           [to]        [:::::::::::::::::::::::::::>>"
echo "          \   \\\  \\\  \\\  \\\  \\\ ${winPath}   \\\  \\\  \\\  \\\  \\\\"
echo "           | :||: || :||: || :||: || :||: || :||: || :||: || :||: || :||: ||: |"

echo "";
echo "              /= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =\\" 
echo "             /= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =\\"
echo "            ||                                                               ||"
echo "            ||            Windows Path copied to clipboard                   ||"
echo "            ||                                                               ||"
echo "             \= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =/"
echo "              \= = = = = = = = = winpath -h for help = = = = = = = = = = = =/"
echo "               \= = = = = = = = = = = = = = = = = = = = = = = = = = = = = =/"
echo $winPath | clip.exe
echo ""

#echo $path | /mnt/c/Windows/System32/clip.exe



# /mnt/s/Prepress/Catfish Storefronts/Storefronts/Wesley Family Services/Products/Business Card/Portal/Wesley Family Services Business Card Template Custom-Rev-01.pdf

```