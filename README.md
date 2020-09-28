Coupled NEMO-PISCES-APECOSM configurations
=================================================

<div align="center">
  <img src="https://raw.githubusercontent.com/apecosm/apecosm-pisces-1d/master/images/logo_apecosm_sanstexte_rvb_300dpi.png?token=AHYKVT3EE3WLFVG4BTLN3RS7OG3CS" height=50 hspace=50>
  <img src="https://raw.githubusercontent.com/apecosm/apecosm-pisces-1d/master/images/NEMO_logo.png?token=AHYKVTZOMJVELKHSAZGUI7S7OG3AG" height=50>
</div>

# How to use

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
