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

## BASH

### passwordless ssh
```
ssh -oStrictHostKeyChecking=no -i ${KEYFILE} ${REMOTE_SERVER} "${COMMAND_TO_EXECUTE_REMOTELY}"
```

### common bash functions
```
#!/bin/bash

function help {
  echo "Display this help: script.sh --help "
  echo "Run the script:   
            build.sh 
            -v1|--var1 <var1_value> 
            -v2|--var2 <var2_value>"
  exit 0
}

function set_var {
  VAR_NAME="$1";
  VAR_DEFAULT="$2"
  VAR_VALUE="$3";
  if [[ -z "$VAR_VALUE" ]]; then
    read -s -p "Please key in <$VAR_NAME> ($VAR_DEFAULT):" VAR_VALUE;
  fi
  if [[ -z "$VAR_VALUE" ]]; then
    export ${VAR_NAME}=${VAR_DEFAULT}
  else
    export ${VAR_NAME}=${VAR_VALUE}
  fi
}

function parse_param {
    while :
    do
        case "$1" in
        -h | --help)
        help  # Call help function
                # no shifting needed here, we're done.
        exit 0
        ;;
        -v1 | --var1)
            VAR1="$2"
            shift 2
            ;;
        -v2 | --var2)
            VAR2="$2"
            shift 2
            ;;
        --) # End of all options
        shift
        break;
            ;;
        -*)
        echo "Error: Unknown option: $1" >&2
        exit 1
        ;;
        *)  # No more options
        break
        ;;
        esac
    done

    echo "***** VAR1: $VAR1"
    echo "***** VAR2: $VAR2"

}

```
