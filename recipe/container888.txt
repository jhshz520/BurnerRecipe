# bootstrap from docker ubuntu image
BootStrap: docker
From: ubuntu:latest

%post
    apt-get update  --fix-missing

    apt-get install -y tar git curl libcurl4-openssl-dev wget dialog \
    net-tools build-essential python python-dev python-distribute \
    python-pip zlib1g-dev libxslt1-dev libffi-dev libssl-dev

    mkdir -p /srv/ga4gh-server

    git clone -b auth-deploy-stable-test https://github.com/Bio-Core/ga4gh-server.git /srv/ga4gh-server

    # install python package requirements
    pip install -r /srv/ga4gh-server/requirements.txt

    pip install /srv/ga4gh-server

    # prepare sample/compliance data
    cd /srv/ga4gh-server/scripts

    python prepare_compliance_data.py -o /srv/ga4gh-compliance-data

%runscript

    exec ga4gh_server -P "${GA4GH_PORT}" -H "${GA4GH_IP}" -f "${GA4GH_CONFIG}"
