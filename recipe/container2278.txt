Bootstrap: shub
From: CNC-UMCG/cnc_spm-fsl

%environment


%post
    apt-get install -y ants
    
    #############################
    # mrQ package
    #############################
    
    git clone https://github.com/mezera/mrQ.git



