# Linux Config File Version Control and Backup on GitHub

A simple script that enables a powerful workflow: manage all configuration files on your Linux machines with Git and back them up on GitHub or any other version control host.

This is how it's used:

- Create a private GitHub repository for each machine's backup.
- Run the script on a Linux machine. It copies all configuration files (and/or anything else you want to backup) to a local Git repository.
- Push the changes from a machine's local repository to GitHub.

# Preparation (Once per Machine You Want to Backup)

These preparation steps only need to be done once on each machine whose configuration you want to backup. [Check out how to perform a backup](#performing-a-backup).

## Local Backup Directory

Clone the repo on your backup directory on server

    cd <cloned directory>
    chmod +x backup
    mkdir -p confs
    chmod 774 backup

## Git config for private repo to push confs

    Remove .git directory and init new private repo
    rm -rf .git
    git init
    git remote add origin <new git repo url>
    

## Configure What to Backup

The script copies every file or directory listed in the source file `backup.list`. Globbing (including recursive wildcard expansion) is enabled. The recommended default content for the backup source file is the following:

    /etc/**/*.conf
    /etc/ssh/sshd_config

Prepend the line with '#' or ';' in-order to comment the line backup.list

# Create the backup sources file:

    vi ./backup.list
    [paste the file content and save the file]

# Performing a Backup

Run the script:

    cd <backup directory>
    ./backup
    git add .
    git commit 
    git push -u origin --all
    

# References

- Inspiration: https://github.com/vastlimits/OS-Conf-Backup-Linux/blob/master/README.md
