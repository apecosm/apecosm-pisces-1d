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

- Download the NEMO code as follows :`svn co http://forge.ipsl.jussieu.fr/nemo/svn/NEMO/releases/release-3.6/NEMOGCM`. **Registration on the NEMO forge is needeed**
- Create a new configration as follows: `./makenemo -m ARCH -r C1D_PAPA -n C1D_PISCES_APECOSM`.
- Edit the `C1D_PISCES_APECOSM/cpp_C1D_PISCES_APECOSM.fcm file` and add `key_top` and `key_pisces`
- Create a new architecture file to include Apecosm library files following http://documentation.apecosm.org/nemo.html#modification-of-a-nemo-architecture-file
- Copy the fortran files in the Apecosm `src/nemo/fortran` to the `C1D_PISCES_APECOSM/MY_SRC` directory, following  http://documentation.apecosm.org/nemo.html#creation-of-a-nemo-ap-configuration
- Recompile the code using `./makenemo -m ARCH-AP -n C1D_PISCES_APECOSM`.

# Running a configuration

- Go to the `C1D_PISCES_APECOSM/EXP00` directory.
- Copy the content of the `SHARED/apecosm` directory into `C1D_PISCES_APECOSM/EXP00`
- Copy the content of the `SHARED/namelist` directory into `C1D_PISCES_APECOSM/EXP00`
- Copy the content of the `CONF/data` directory into `C1D_PISCES_APECOSM/EXP00`, with `CONF` one of the 1D configuration (`BATS`, `DYFAMED`, etc.)
- Copy the content of the `CONF/namelist` directory into `C1D_PISCES_APECOSM/EXP00`, , with `CONF` one of the 1D configuration (`BATS`, `DYFAMED`, etc.)
- Go to the `C1D_PISCES_APECOSM/EXP00` and type `./opa`.
