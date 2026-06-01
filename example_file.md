# Test files to work on HiperGator

For example commands, click [here](README.md)

Running:
```sh
sbatch test.job
```

This test works as of June 1, 2026


## Inputs:
- [test.job](#test_job)
- [phits.in](#phits_in)
- [input.inp](#input_inp)

**Expected outputs:**
- e1_xz.eps
- e1_xz.out
- phits.out
- temp.out
- test_john_<id>.log

# Files

## test.job
```
#!/bin/bash
#SBATCH --job-name=test_john
#SBATCH --mail-type=ALL
#SBATCH --mail-user=<francis.john@ufl.edu>
#SBATCH --ntasks=8
#SBATCH --nodes=1
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=400mb
#SBATCH --time=11:00:00
#SBATCH --output=test_john_%j.log
#SBATCH --account=bolch
#SBATCH --qos=bolch-b
#SBATCH --constraint=el9

pwd
module purge
dos2unix *

module load intel/2025
module load ufrc

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

srun /blue/bolch/itar/phits335/phits_LinIfort_OMP <phits.in> temp.out

echo Running with $OMP_NUM_THREADS OpenMP threads
```

## phits.in
```
file=input.inp
```

## input.inp
```
[title]
Exercise 1: Co-60 sphere

[parameters]
icntl = 8
maxcas = 1
maxbch = 1
e-mode = 1
nucdata=0
file(1) = /blue/bolch/itar/phits335
emin(2) = 20

[material]
$ Co60
mat[1] 27060 1

$ Water
mat[2] H 2 O 1

$ Air
mat[3] 7000 -80 8000 -20

[surface]
$ 2.5 radius sphere
10 so 2.5

$ 5 cm cube
$ Note: It's 10 cm away from the sphere on the z axis
20 rpp -2.5 2.5 -2.5 2.5 12.5 17.5 

$ universe
999 rpp -3 3 -3 3 -3 20

[cell]
$ Co60 sphere
100 1 8.9 -10

$ Water cube
200 2 1 -20

$ Air
1000 3 -0.001 -999 #100 #200

$ Void
1001 -1 999

[source]
s-type = 1
proj = photon
dir = all
e0 = 0.1

[t-track]
$ -3 3 -3 3 -3 20
mesh=xyz
x-type=2
xmin=-4
xmax=4
nx=60
y-type=2
ymin=-4
ymax=4
ny=1
z-type=2
zmin=-4
zmax=21
nz=100
axis=xz
e-type=1
ne=1
  0.0 1000.0
unit=1 $1/cm^2/source
title=track xz
file=e1_xz.out
gshow=1
epsout=1
```

