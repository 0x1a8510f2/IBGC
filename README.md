# In-Browser Go Compiler

This project is based on [ccbrown/wasm-go-playground](https://github.com/ccbrown/wasm-go-playground)

This is the Go compiler ("gc") compiled for WASM, running in your browser! It can be used to compile Go programs without the need to install anything on your computer.

You can try it out here: https://tr-slimey.github.io/IBGC/

#### ⚠️ Warning ⚠️

* According to the original project, Safari works, but is unbearably slow. **Chrome or Firefox for desktop is highly recommended**.
* Imports other than "runtime" are currently not supported, but will be added over time.
* Targets other than Linux/amd64 are currently not supported but will also be added over time.

## Explanation

For information about the files in this project, please see the original project linked above. The directory structure changes should be self-explanatory.
