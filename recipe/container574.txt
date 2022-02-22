Bootstrap: docker
From: r-base:latest

%post
	apt-get update
	apt-get install -y libssl-dev libsasl2-dev
	R -e "install.packages('Hmisc')"
	R -e "install.packages('ggplot')"
	R -e "install.packages('mongolite')"
	R -e "install.packages('stringr')"
	R -e "install.packages('jsonlite')"
	R -e "install.packages('maps')"
	R -e "install.packages('mapproj')"
	R -e "install.packages('choroplethr')"
	R -e "install.packages('readxl')"
	R -e "install.packages('dplyr')"
	R -e "install.packages('choroplethrMaps')"
	R -e "install.packages('ggplot2')"
	R -e "install.packages('igraph')"
	
