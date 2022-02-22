Bootstrap:docker
From:python:3.7-alpine

%post

apk --update --no-cache add bash alpine-sdk zeromq-dev nodejs npm libffi-dev
pip install jupyter
npm install -g ijavascript

%environment

# export IJS_PORT=8888

# Otherwise, you will encounter the error "Permisson denied /run/user ..."
# See: https://github.com/jupyter/notebook/issues/1318
export XDG_RUNTIME_DIR=""

%runscript

echo "Opening IJavascript (Jupyter) notebook ..."
test -z "$IJS_PORT" && IJS_PORT=8888
/usr/bin/ijs --notebook-dir=. --ip='*' --port=$IJS_PORT --no-browser
