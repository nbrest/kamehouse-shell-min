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
if [ "$?" != "0" ]; then
  echo -e "Error importing common-functions.sh"
  exit 99
fi

mainProcess() {
  # add your script logic here
}

main "$@"
```

## Version

- Using kamehouse's commit version [841b33f36](https://github.com/nbrest/kamehouse/tree/841b33f36)

- The source files are exported automatically from kamehouse with [update-kamehouse-shell-min.sh](https://github.com/nbrest/kamehouse/blob/dev/kamehouse-shell/bin/kamehouse-shell-min/update-kamehouse-shell-min.sh)
