# infra
infrastracture repo

gcloud compute instance-templates create python-app --boot-disk-size=10GB --image=ubuntu-1604-xenial-v20170815a --image-project=ubuntu-os-cloud --tags http-server --machine-type=f1-micro --restart-on-failure --metadata startup-script='wget -O -  https://gist.githubusercontent.com/spybond08/c063f6c12ff852d82163deadbc09fcbd/raw/2e2cde1f8698058ee726d3d0549666e55f0b6988/gistfile1.txt | bash'
