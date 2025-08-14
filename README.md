Minimal version of [kamehouse shell](https://github.com/nbrest/kamehouse/tree/dev/kamehouse-shell) to easily use it's logging framework, argument parsing and other functionality in other projects

## Install
```sh
mkdir -p ${HOME}/git
cd ${HOME}/git
git clone https://github.com/nbrest/kamehouse-shell-min.git
```

## Usage

- Build your own scripts with the following structure

```sh
#!/bin/bash

source ${HOME}/git/kamehouse-shell-min/bin/common/functions/common-functions.sh
if [ "$?" != "0" ]; then echo "Error importing common-functions.sh" ; exit 99 ; fi

initKameHouseShellEnv() {
  #LOG=DISABLED
  #LOG_PROCESS_TO_FILE=false
  #LOG_CMD_ARGS=false
  return
}

initScriptEnv() {
  # Init script global variables here
  TEST_PARAM=""
}

mainProcess() {
  log.info "Add your script logic here"
  log.trace "TEST_PARAM=${TEST_PARAM}"
}

parseArguments() {
  local OPTIONS=("$@")
  for i in "${!OPTIONS[@]}"; do
    local CURRENT_OPTION="${OPTIONS[i]}"
    if [ "${CURRENT_OPTION:0:1}" != "-" ]; then
      continue
    fi
    local CURRENT_OPTION_ARG="${OPTIONS[i+1]}"
    case "${CURRENT_OPTION}" in
      -t|--test-param)
        TEST_PARAM="${CURRENT_OPTION_ARG}"
        ;;
      -?|-??*)
        parseInvalidArgument "${CURRENT_OPTION}"
        ;;        
    esac
  done    
}

setEnvFromArguments() {
  checkRequiredOption "-t" "${TEST_PARAM}" 
}

printHelpOptions() {
  addHelpOption "-t|--test-param [val]" "Test parameter" "r"
}

main "$@"
```

## Version

- Using kamehouse's commit version [6ce0c51a8](https://github.com/nbrest/kamehouse/tree/6ce0c51a8)

- The source files are exported automatically from kamehouse with [update-kamehouse-shell-min.sh](https://github.com/nbrest/kamehouse/blob/dev/kamehouse-shell/bin/kamehouse-shell-min/update-kamehouse-shell-min.sh)
