Coupled NEMO-PISCES-APECOSM configurations
=================================================

<div align="center">
  <img src="https://github.com/apecosm/apecosm-pisces-1d/blob/master/images/logo_apecosm_sanstexte_rvb_300dpi.png?token=AHYKVT3EE3WLFVG4BTLN3RS7OG3CS" height=70 hspace=50>
  <img src="https://github.com/apecosm/apecosm-pisces-1d/blob/master/images/NEMO_logo.png" height=50>
</div>

# Stations

- BATS: (64°W, 31.5°N) ): http://bats.bios.edu/
- HOT: (158°W, 22.45°N ): http://hahana.soest.hawaii.edu/hot/ 
- FAMED: (7.52°E, 43.27°N): http://www.obs-vlfr.fr/cd_rom_dmtt/sodyf_main.htm
- KERFIX: (68.25°E, 50.40°S): http://www.obs-vlfr.fr/cd_rom_dmtt/OTHER/KERFIX/bacteries/kfx_bact_delille.htm.htm
- NABE: (20°W, 47°N): http://www1.whoi.edu/research/nabe.html

# Compilation

## APECOSM

- Clone the Apecosm repository as follows: `git clone https://github.com/apecosm/apecosm-private.git` (or use SSH or GitHub Cli)
- Extract the `develop` branch as follows: `git checkout develop`
- Compile the code with the `make nemo` command, and make sure that the `-DNO_USE_MPI` (no MPI), `-DUSE_NEMO` (NEMO coupling) and `-DNEMO_NOINTERP` (no vertical interpolation of forcings) CPP keys are used.

## NEMO

- Download the NEMO code as follows :`svn co https://forge.ipsl.jussieu.fr/nemo/svn/NEMO/releases/r4.0/r4.0.6 nemo-4` .
- Create a new configration as follows: `./makenemo -d "OCE TOP" -m GCC_LINUX_nico -r C1D_PAPA -n C1D_PISCES add_key "key_top key_nosignedzero"`.
- Create a new architecture file (`arch` directory) to include Apecosm library files.
- Copy the fortran files from the Apecosm `src/nemo/fortran` folder to the NEMO `cfg/C1D_PISCES/MY_SRC` directory.
- Recompile the code using `./makenemo -d "OCE TOP" -m GCC_LINUX_nico -r C1D_PAPA -n C1D_PISCES add_key "key_top key_nosignedzero"`

# Running a configuration

- Go to the NEMO `cfgs/C1D_PISCES/EXP00` directory.
- Copy the content of the `SHARED/apecosm` directory into `cfgs/C1D_PISCES/EXP00`
- Copy the content of the `SHARED/nemo` directory into `cfgs/C1D_PISCES/EXP00`
- Copy the content of the `CONF/data` directory into `cfgs/C1D_PISCES/EXP00`, with `CONF` being one among `BATS`, `DYFAMED`, `HOT`, `KERFIX`, `NABE`
- Copy the `cfg` namelists of the `CONF` directory into `cfgs/C1D_PISCES/EXP00`, with `CONF` being one among `BATS`, `DYFAMED`, `HOT`, `KERFIX`, `NABE`
- Go to the `cfgs/C1D_PISCES/EXP00` and type `./nemo`.
