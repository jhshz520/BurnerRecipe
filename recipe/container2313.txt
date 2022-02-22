
Bootstrap: shub
From: CNC-UMCG/cnc_spm-fsl

%environment


%post
   apt-get install -y libstdc++6
   apt-get install -y ants
    
