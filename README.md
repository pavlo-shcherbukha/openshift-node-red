# The OpenShift `nodejs` cartridge documentation can be found at:

## Полезные линки

[https://developer.ibm.com/tutorials/kubernetes-openshift-minishift-101-node-red-labs/](https://developer.ibm.com/tutorials/kubernetes-openshift-minishift-101-node-red-labs/)
[IBM/node-red-workshop-starter](https://github.com/IBM/node-red-workshop-starter)


http://openshift.github.io/documentation/oo_cartridge_guide.html#nodejs

## openshift-node-red

Background information for Node in OpenShift

The OpenShift nodejs cartridge documentation can be found at:

http://openshift.github.io/documentation/oo_cartridge_guide.html#nodejs
1. Get Minishift running

Open your terminal and run the following commands:

    minishift --vm-driver=hyperkit start (or equivalent, based on which vm you're using)
    eval $(minishift oc-env)
    oc login -u developer

2. Get OpenShift-Node-RED

Clone the repository

Still using your terminal:

    Clone the starter repo using the following command:

    git clone https://github.com/emarilly/openshift-node-red

    Change directory into the OpenShift-noe-red folder

    cd openshift-node-red

Update package.json

Using your favorite IDE (we're not judging) open and edit the package.json file:

    update the Node.js engine to current LTS (>=10.0.0)
    update the NPM engine to be inline with node LTS (>= 6.0.0)
    update Node-RED dependency to current levels (>= 1.0)
    add a scripts section

"scripts": {
  "build": "true",
  "start": "node server.js"
},

Update server.js

Next, open and edit the server.js file:

    comment out basic authentication setup

//setup basic authentication
//var basicAuth = require('basic-auth-connect');
//self.app.use(basicAuth(function(user, pass) {
//    return user === 'test' && pass === atob('dGVzdA==');
//}));

    update local port to 8080

self.port      = process.env.OPENSHIFT_NODEJS_PORT || 8080;

    update default ipaddress to "0.0.0.0"

self.ipaddress = process.env.OPENSHIFT_NODEJS_IP || "0.0.0.0";

Once this is all done, go back to your terminal and run the following command npm install.
Push Node-RED on Minishift/openshift

    Create a new app and give it a name (ie. myfirst-node-red)

    oc new-app nodejs~./ --name=myfirst-node-red

    Start the build of your app

    oc start-build myfirst-node-red --from-dir=./

    You can check the status at any time using

    run oc status

    Once the build is complete, run the following command to get the service

    oc get service myfirst-node-red

    Expose the service at a host name using:

    oc expose service myfirst-node-red

All done! You can now access your Node-RED application running on Minishift using the response from oc get route/myfirst-node-red

NAME               HOST/PORT                                        PATH      SERVICES           PORT       TERMINATION   WILDCARD
myfirst-node-red   myfirst-node-red-node-red.<aaa.bbb.ccc.ddd>.nip.io             myfirst-node-red   8080-tcp                 None

    Open your browser to http://myfirst-node-red-node-red.<aaa.bbb.ccc.ddd>.nip.io
