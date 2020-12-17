# Private OFC test instance

## Intro

OFC stands for [OpenFaaS Cloud](https://github.com/openfaas/openfaas-cloud) - this is OpenFaaS deployed in gitops fashion, where you configure you GitHub repository, push function code and the rest is history.

**IMPORTANT** - the test instance is running on a massively oversubscribed vmware platform that is not very reliable and can go down at any moment. Don't be a jerk - use this as test/PoC, not to run  `nmap` and stuff.

## How to test it?

* Check if your GitHub username is listed [here](https://github.com/tmiklas/ofctest/blob/master/CUSTOMERS) - unless it's in the list, you have no access
* Get a copy of [faas-cli](https://github.com/openfaas/faas-cli) and download the language templates my instance supports (see below)
* Create a github repo for your function code - it can be set to PRIVATE
* Add the [builder app](https://github.com/apps/hal-builder) to your account and enable it **ONLY** for the repository that will contain your function code
* Once you write your function and `git push` it, the rest will happen automatically - your function will be pulled, built and deployed... nice, isn't it?

## Important URLs

Talk to me and I'll let you know :)

There is personal dashboard and function invocation URL in your own namespace... and all the rest is federated with GitHub, so no other accounts needed.

## Useful reading

OpenFaaS has really good documentation and is changing very rapidly. To get the basics quickly see the below

* [OpenFaaS Workshop](https://docs.openfaas.com/tutorials/workshop/) - the best place to start, there are also other tutorials and blog posts linked there
* [OpenFaaS Cloud documentation](https://docs.openfaas.com/openfaas-cloud/) - this is the platform we are using here
* [OpenFaaS Architecture](https://docs.openfaas.com/architecture/stack/) - for deep dive into OpenFaaS

## Sealed secrets

The platform supports Kubernetes style Sealed Secrets - encrypted with cluster's public key, so you can commit them securely with the code and deploy with your function. 

To create `secrets.yml` you can use the command below with `pub-cert.pem` included in this repository. Of course remember to include secrets configuration in `stack.yml` for your function!

```
faas-cli cloud seal --name my-function-secret --literal hmac-secret=1234 --cert=pub-cert.pem
```

## Supported templates

    - "https://github.com/openfaas-incubator/golang-http-template.git"
    - "https://github.com/openfaas-incubator/node10-express-template.git"
    - "https://github.com/openfaas-incubator/python-flask-template.git"
    - "https://github.com/openfaas-incubator/ruby-http"
    - "https://github.com/tmiklas/openfaas-perl-templates"
    - "https://github.com/alexellis/openfaas-streaming-templates"
    
    
EOT
