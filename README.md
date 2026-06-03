# charmm-md-toolkit

A small collection of CHARMM input scripts for setting up, equilibrating, and
running molecular dynamics simulations of solvated proteins, plus a couple of
analysis helpers.

## Contents

```
charmm-md-toolkit/
├── README.md
├── LICENSE
├── .gitignore
├── scripts/
│   ├── 01_minimize.inp        # Energy minimization
│   ├── 02_solvate.inp         # Solvation in a TIP3P water box
│   ├── 03_equilibrate.inp     # NVT/NPT equilibration
│   └── 04_production.inp      # Production MD run
├── toppar/
│   └── toppar.str             # Stream file loading topology + parameters
└── analysis/
    ├── rmsd.inp               # Backbone RMSD over a trajectory
    └── plot_rmsd.py           # Quick matplotlib plot of the RMSD output
```

## Requirements

- CHARMM (free academic version `charmm` or commercial)
- CHARMM36m topology/parameter files in `toppar/`
- Python 3 with `numpy` and `matplotlib` for the analysis script

## Usage

Each `.inp` file is meant to be run in sequence:

```bash
charmm -i scripts/01_minimize.inp -o logs/01_minimize.out
charmm -i scripts/02_solvate.inp   -o logs/02_solvate.out
charmm -i scripts/03_equilibrate.inp -o logs/03_equilibrate.out
charmm -i scripts/04_production.inp  -o logs/04_production.out
```

Then analyze:

```bash
charmm -i analysis/rmsd.inp -o logs/rmsd.out
python analysis/plot_rmsd.py rmsd.dat
```

## Notes

Paths to structure files (`protein.psf`, `protein.crd`) and box dimensions are
placeholders. Edit them to match your system before running.
