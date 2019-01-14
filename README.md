# Node Addon Hello World example repository
Node Addon Hello World example repository using node-addon-api, a C++ wrapper for N-API
## Steps taken to reproduce this project
This project can run without any changes (aside from ensuring Python 2.7 is installed), but the project can be recreated using the following steps. The source code was pulled from the example section of the [node-addon-api](https://github.com/nodejs/node-addon-api) readme.
1. Install [Python 2.7](https://www.python.org/downloads/release/python-2713/)
2. Create project directory, run `npm init` inside the directory to initialize a node project
3. `npm install node-addon-api --save` && `npm install bindings --save`
4. If using Visual Studio to write the addon, prefer using the [Open Folder](https://docs.microsoft.com/en-us/cpp/ide/non-msbuild-projects?view=vs-2017) feature to avoid creating solution and project files
