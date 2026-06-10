# HiPeRgAtOr commands
Useful commands and things for hipergator

For an example phits run, click [here](example_file.md)

## Contents

- [SSHing in from an external computer](#sshing-in-from-an-external-computer)
- [Submit job](#submit-job)
- [Checking useage](#checking-useage)
- [General commands](#general-commands)
- [Notes](#notes)
  
## SSHing in from an external computer
TODO

## Submit job
```sh
sbatch job.sh
```

## Checking useage
**Check lab usage**
```sh
slurminfo -u bolch
```
**Check your own jobs**
```sh
squeue -u username
```
**Cancel job**
```sh
scancel JOBID
```
**Cancel all your jobs**
```sh
scancel -u username
```

## General commands
**Navigating the system**
```sh
pwd              # where am I
ls               # list files
ls -lah          # detailed list (size, permissions, hidden files)
cd folder/       # go into folder
cd ..            # go up one directory
cd ~             # home directory
```
**Working with files**
```sh
cp a.txt b.txt        # copy
mv a.txt b.txt        # move/rename
rm file.txt           # delete file
rm -r folder/         # delete folder (careful)
mkdir new_folder      # create folder
touch file.txt        # create empty file
cat file.txt          # view the contents of the file
```
**Writing messages in terminal or in files**
```sh
echo "message"               # Write message in terminal
echo "message" > file.txt    # Write message in file.txt
echo "message" >> file.txt   # Append message to end of file.txt
nano filename                # Open file in a mini text editor (it takes some learning to figure out how to use)
```


## Notes
- Max wall time for bolch-b is 4 days aka `4-00:00:00`


<!--
## Specific things
**Tetrahedralizing with POLY2TET**
Do not tetrahedralize in the login node, begin an interactive session using:
```sh
srun --ntasks=1 --cpus-per-task=16 --mem=100gb -t [time] --pty bash -i
```
(If you just put 90 for time, it will work for 90 minutes, this is recommended for the sizes we work with)

Now run poly2tet
```sh
./POLY2TET -p [name].obj
```
-->
