# DevOps Stuff

## Artifact repos

### Nexus3

#### API to upload to a nexus3 maven repo

To upload a ML model with particular version

```
MODEL=my_model
MODEL_PACKAGE=my_model.zip
VERSION=0.9-SNAPSHOT
curl -v -u ${admin_user}:${admin_password} --upload-file ${MODEL_PACKAGE} https://nexuscimgmt.sgp.dbs.com:8443/nexus/repository/ACOE/com/dbs/${MODEL}/${VERSION}/${MODEL}-${VERSION}.zip
```
