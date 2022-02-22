Bootstrap: shub
From: CNC-UMCG/cnc_base

%runscript
        exec meica.py "$@"

%environment
        PATH=$PATH:/usr/abin
        export PATH
%post
	apt-get install -y software-properties-common
	add-apt-repository universe
	apt-get update -y
	
	apt-get install -y tcsh xfonts-base python-qt4       \
        	                gsl-bin netpbm gnome-tweak-tool   \
                	        libjpeg62 xvfb xterm vim curl     \
                        	gedit evince                      \
	                        libxm4 build-essential	
	
	# install SciPy
	apt-get install -y python-numpy python-scipy python-matplotlib \
	 	  	   ipython ipython-notebook \
			   python-pandas python-sympy python-nose
	mkdir /usr/abin
	cd
	curl -O https://afni.nimh.nih.gov/pub/dist/bin/linux_ubuntu_16_64/@update.afni.binaries
	tcsh @update.afni.binaries -package linux_ubuntu_16_64  -do_extras -bindir /usr/abin
	export R_LIBS=$HOME/R
	export PATH=$PATH:/usr/abin

	bash
	################
	# Install R   #
	################
	
	mkdir $R_LIBS
	echo 'export R_LIBS=$HOME/R' >> ~/.bashrc
	
	bash
	
	curl -O https://afni.nimh.nih.gov/pub/dist/src/scripts_src/@add_rcran_ubuntu.tcsh
	tcsh @add_rcran_ubuntu.tcsh

	/usr/abin/rPkgsInstall -pkgs ALL
	
