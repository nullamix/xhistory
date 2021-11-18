#!/bin/bash

# You can install script if you are root
# Run this script only once and reboot your computer

DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
CONF=/etc/bash.bashrc

# Create xhistory directory and files
CopyFiles () {
        cp $DIR/xhistoryscript /usr/xhistory/.xhistoryscript
        touch /usr/xhistory/blacklist
}
if [ ! -d /usr/xhistory ]
then
        mkdir /usr/xhistory
        CopyFiles
elif [[ -e /usr/xhistory/xhistory || -e /usr/xhistory/blacklist ]]
then
        while :
        do
                printf "some files in /usr/xhistory are exist\nremove theme? "
                read RM
                if [[ $RM = 'y' || $RM = 'yes' ]]
                then
                        if [ -e /usr/xhistory/xhistory ]
                        then
                                printf "Do you want to back up the previous file? "
                                read BU
                                if [[ $BU = 'y' || $BU = 'yes' ]]
                                then
                                        mv /usr/xhistory/xhistory ~/.backupxhistory
                                fi
                        fi
                        rm -rf /usr/xhistory/*
                        CopyFiles
                        if [ -e ~/.backupxhistory ]
                        then
                                mv ~/.backupxhistory /usr/xhistory/xhistory
                        fi
                        break
                elif [[ $RM = 'n' || $RM = 'no' ]]
                then
                        echo -e "ok\nBYE!"
                        break
                else
                        echo -e "\nI don't understand your answer\n"
                fi
        done
else
        CopyFiles
fi

# If you don't want your command to be seen, add it to black list file
# Black list file address:  /usr/xhistory/blacklist
# For example:
echo 'uptime' >> /usr/xhistory/blacklist

# Add config in bash.bashrc file (for run xhistory per command) by /usr/xhistory/.checkfile
if [ $(grep -c 'xhistory' $CONF) = 0 ]
then
        cat $DIR/forcopy >> $CONF
        echo -e '\n\033[32m' 'DONE!' '\033[0m'
else
        printf "\033[0;31m\nI found 'xhistory' word in /etc/bash.bashrc\n"
        printf "sure not installed xhistory before and try again\n\033[0m"
fi
