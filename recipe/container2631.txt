BootStrap: yum
OSVersion: 7
MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/x86_64/

Include: yum

%help
echo "This is a container to run MILC on CentOS compiled under GCC."


%post
yum install -y tar wget bzip2 make gcc gcc-c++ which
wget https://asc.llnl.gov/CORAL-benchmarks/Micro/MILCmk-v1.tar.bz2
tar xvjf MILCmk-v1.tar.bz2
cd MILCmk-v1/
sed -i '1s/.*/CC = gcc/' Makefile
sed -i '3s/.*/COPT = -O3 -mavx2/' Makefile
sed -i '4s/.*/OMP = -fopenmp/' Makefile
sed -i '8s/.*/CFLAGSA = -lm -std=c99/' Makefile
make
chmod -R 777 /MILCmk-v1
exit 0

%runscript
echo "run MILC"
cd /MILCmk-v1
echo "Shouldnt require sudo to run."
./qla_bench-qla-1.7.1-d3 2>&1 | tee d3.output
./qla_bench-qla-1.7.1-f3 2>&1 | tee f3.output
exit 0
