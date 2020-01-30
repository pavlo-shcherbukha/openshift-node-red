# The OpenShift node-red application

## useful links

[https://developer.ibm.com/tutorials/kubernetes-openshift-minishift-101-node-red-labs/](https://developer.ibm.com/tutorials/kubernetes-openshift-minishift-101-node-red-labs/)
[IBM/node-red-workshop-starter](https://github.com/IBM/node-red-workshop-starter)

[original repo](http://openshift.github.io/documentation/oo_cartridge_guide.html#nodejs)

## application description

Application starts from Node.js web server, port 8080 that is native for openshift

All http-request nodes are accesses after siffix /API/

Application build

```bash
  npm install
```

Application start

```bash
  npm start
```

Flows are stored in the file in the root directory with name:

```text
   flows_[hostname.json]
```

example: flows_LAPTOP-QLF2SECA.json 
explanation is in the file readme_flow.pdf in the root directory
