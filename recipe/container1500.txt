Bootstrap:docker  
From:nadinefischer/pythiadire:v1

%files

%labels

%environment

%runscript
exec echo "Try running with --app [rivet|dire|runOnCluster]"

%apprun runOnCluster
exec /usr/local/bin/runOnCluster "$@"

%apprun rivet
exec /usr/local/bin/rivet "$@"

%apprun dire
exec /usr/local/bin/dire "$@"

%post

