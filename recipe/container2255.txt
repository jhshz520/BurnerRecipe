Bootstrap: docker
FROM: r-base:3.4.4

%help
  R version 3.4.4 (2018-03-15) -- "Someone to Lean On"
  Copyright (C) 2018 The R Foundation for Statistical Computing
  Platform: x86_64-pc-linux-gnu (64-bit)

  Usage:
  $ singularity run r-base.3.4.4.simg [args]
  $ singularity run --app R r-base.3.4.4.simg [args]
  $ singularity run --app Rscript r-base.3.4.4.simg [args]

%setup

%files

%labels
  Maintainer Michael J. Stealey
  Maintainer_Email stealey@renci.org
  R_Version 3.4.4

%environment
  R_BASE_VERSION=3.4.4
  LC_ALL=en_US.UTF-8
  LANG=en_US.UTF-8

%post

%apprun R
  exec R "${@}"

%apprun Rscript
  exec Rscript "${@}"

%runscript
  exec R "${@}"

%test
  exec R --version
