# sdk install

$ export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"
$ echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | \
sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo \
apt-key add -
$ sudo apt-get update && sudo apt-get install google-cloud-sdk

# 인증

$ gcloud auth application-default login

# instance 확인

$ gcloud compute instances list

# ssh

$ gcloud compute ssh learning-cloud-demo

# node 버전확인

$ node --version

# project확인

$ gcloud config list project



const gce = require('@google-cloud/compute')({
projectId: 'pelagic-river-221312'
});
const zone = gce.zone('asia-northeast1-b');
console.log('Getting your VMs...');
zone.getVMs().then((data) => {
data[0].forEach((vm) => {
console.log('Found a VM called', vm.name);
});
console.log('Done.');
});

$ node script.js

const gce = require('@google-cloud/compute')({
projectId: 'pelagic-river-221312'
});
const zone = gce.zone('asia-northeast1-b');
console.log('Getting your VMs...');
zone.getVMs().then((data) => {
data[0].forEach((vm) => {
console.log('Found a VM called', vm.name);
console.log('Stopping', vm.name, '...');
vm.stop((err, operation) => {
operation.on('complete', (err) => {
console.log('Stopped', vm.name);
});
});
});
});
