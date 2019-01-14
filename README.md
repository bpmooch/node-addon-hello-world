# Calling C from Node
Node Addon hello world example project using node-addon-api, a C++ wrapper for N-API
## Steps taken to reproduce this project
This project can run without any changes (aside from ensuring Python 2.7 is installed), but the project can be recreated using the following steps. The source code was pulled from the example section of the [node-addon-api](https://github.com/nodejs/node-addon-api) readme.
1. Install [Python 2.7](https://www.python.org/downloads/release/python-2713/)
2. Create project directory, run `npm init` inside the directory to initialize a node project
3. `npm install node-addon-api --save` && `npm install bindings --save`
4. If using Visual Studio to write the addon, prefer using the [Open Folder](https://docs.microsoft.com/en-us/cpp/ide/non-msbuild-projects?view=vs-2017) feature to avoid creating solution and project files
## C++ Addons vs N-API vs node-addon-api
C/C++ interoperability with Node is constantly changing, so it's worth laying out the different strategies for calling C code from Node.
### [C++ Addons](https://nodejs.org/api/addons.html)
Node C++ Addons are dynamically linked shared objects that integrate with the v8 runtime directly, as well as several other node specific API's. As referenced in the introduction to the documentation, the immediate downside of C++ Addons is the amount of knowledge required to write them. In addition, because Node does not control the v8 runtime, the v8 team can make breaking changes to the API with no regard for Node users. It's worth noting, however, that none of the interop strategies seem particular resistant to API churn at the time of this writing.
### [Native Abstractions for Node.js (nan)](https://github.com/nodejs/nan)
nan is a C++ header-only wrapper for C++ Addons. Before the creation of this library, the v8 runtime was changing so rapidly that maintaining compatibility with v8 was becoming a non-trivial task for Node addon authors. This library provides v8 version agnostic wrappers for most interop functionality. In addition, it grew to add other helpful utilities for Node addon development.
### [N-API](https://nodejs.org/api/n-api.html)
N-API is an addon API maintained by the Node team directly. This allows the Node team to control the introduction of breaking API changes and logically separates Node C Interop from the v8 runtime. To the best of my knowledge, the only existing Node implementation uses v8, so this is a theoretical strength. If in the future, multiple runtimes were available for Node, N-API would allow addon authors to use a single interface across all runtimes. It's also worth noting that the API is written in C unlike the C++ Addon API, which allows for many more languages to interoperate with Node. 
### [node-addon-api](https://github.com/nodejs/node-addon-api) + [bindings](https://www.npmjs.com/package/bindings)
node-addon-api is a C++ wrapper for N-API maintained by the Node team. N-API code can get much more verbose than the same code in C++ Addons or nan due to it being written in C. node-addon-api exists purely to reintroduce a C++ object oriented API for easier addon development. The docs suggest using `bindings` as well so I've included it. `bindings` provides helper functions in js for requiring your Node addons. 
### Which to use
If you're writing adddons in C or C++, at the time of this writing, node-addon-api seems to be the best option for getting the job done. The docs are well maintained with multiple good examples. From an architecture perspective, it makes a lot of sense to move away from a v8-centric API and provide C bindings, so I'm sure N-API will be the go-to way to interop with Node moving forward. All documentation I've seen surrounding N-API seems to point to this conclusion as well.
