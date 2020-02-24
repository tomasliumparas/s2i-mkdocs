[![Build Status](https://drone.getais.cloud/api/badges/tomasliumparas/s2i-mkdocs/status.svg)](https://drone.getais.cloud/tomasliumparas/s2i-mkdocs)

# Mkdocs S2I container image
This container image includes Node-red for OpenShift and general usage.

Note: while the examples in this README are calling podman, you can replace any such calls by docker with the same arguments

## Description
MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file. 
It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click.

## Usage
The structure of docs-example can look like this:
```
./mkdocs.yml
```
A file containing Mkdocs configuration

```
./requirements.txt
```
Additional python packages - Mkdocs plugins


### Building on OpenShift
If you want to create a new container layered image, you can use the Source build feature of Openshift. To create a new Node-red application in Openshift, while using data available in test-app on the host, execute the following command:
```bash
git clone https://github.com/tomasliumparas/s2i-mkdocs.git
cd s2i-mkdocs
oc new-app getais/s2i-httpd-24-mkdocs-centos7:latest~. --context-dir docs-example --name mkdocs-example
```

Or without locally cloning the repository:
```bash
oc new-app getais/s2i-httpd-24-mkdocs-centos7:latest~https://github.com/tomasliumparas/s2i-mkdocs.git --context-dir docs-example --name mkdocs-example
```

Creating OpenShift route:
```bash
oc expose
```

### Building using standalone S2i
The same application can also be built using the standalone S2I application on systems that have it available
```bash
$ s2i build docs-example/ getais/s2i-httpd-24-mkdocs-centos7 mkdocs-example
```



## Environment variables and volumes
The Apache HTTP Server container image supports the following configuration variables:

```
TBD
```

## Default user
By default, Node-red container runs as UID 1001. That means the volume mounted directories for the files (if mounted using -v option) need to be prepared properly, so the UID 1001 can read them.


