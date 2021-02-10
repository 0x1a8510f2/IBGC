## Unmaintained
More projects like this one seem to be popping up, and my primary usecase for this project no longer exists, so I won't be investing more time into it. If you are looking for maintained projects like this one, please check the [Related Projects](#related-projects) section at the bottom of this file. If you would like to contribute to/maintain the project, please open a pull request with your initial changes stating that you want to contribute.

# In-Browser Go Compiler

This project is based on [ccbrown/wasm-go-playground](https://github.com/ccbrown/wasm-go-playground)

This is the Go compiler ("gc") compiled for WASM, running in your browser! It can be used to compile Go programs without the need to install anything on your computer.

You can try it out here: https://tr-slimey.github.io/IBGC/

#### ⚠️ Warning ⚠️

- **You should never trust unofficial compilers to compile your executables! See [TheKenThompsonHack](https://wiki.c2.com/?TheKenThompsonHack) for more information. You are encouraged to replace the binary files in this repository with those compiled from source by yourself!**
- According to the original project, Safari works, but is unbearably slow. **Chrome or Firefox for desktop is highly recommended**.
- Imports other than "runtime" are currently not supported, but will be added over time.
- Targets other than Linux/amd64 and Windows/amd64 are currently not supported but might be added over time.

## Explanation

For information about the files in this project, please see the original project linked above. The directory structure changes should be self-explanatory.

## Adding new targets

As I work on this project in my spare time, I won't be able to add all targets and libraries straight away. If you wish to add them yourself, the steps are
as follows (Linux with Go 1.15.1):

    // Switch to a temporary directory
    mkdir /tmp/IBGC-tmp && cd /tmp/IBGC-tmp

    // Create a temporary Go file to compile
    echo 'package main\n\nfunc main() {\n    println("Hello World!")\n}' > tmp.go

    // Compile the file for the target which you want to add to IBGC
    GOOS=windows GOARCH=amd64 go build -x -o tmp tmp.go

    // The following is optional, but it makes this much easier!

    // Go may not have cached the files required to build for your target, so -x could have produced a lot of output.
    // In this case, it's easy to get lost. Go will produce only the output we need if you re-run it.

    // Remove the compiled binary
    rm tmp

    // Clear the console to avoid confusion
    clear

    // Compile again using cache for less output
    GOOS=windows GOARCH=amd64 go build -x -o tmp tmp.go

    // The following is no longer optional!

    // Look for lines starting with `packagefile`. The files they point to will need to be copied to IBGC in the correct location
    // For example, assuming these lines look as follows:
    //
    // packagefile command-line-arguments=/home/username/.cache/go-build/09/09b69d59989c358a2f5178854391f3aa120da6e4c90b8181715171c8811d1c4b-d
    // packagefile runtime=/home/username/.cache/go-build/f1/f1ec84319dbbbf0dbd5b3f2e99127a2c7576b9656053757fb8371947f108a220-d
    // packagefile internal/bytealg=/home/username/.cache/go-build/15/15b8a000e48c5ff4d45d4135e297287191be71733224c71f23adb7d2e7436c71-d
    // packagefile internal/cpu=/home/username/.cache/go-build/c6/c64948c8739e5831968e839735b62a3386d5a99301851c9b6d688f1b62995506-d
    // packagefile runtime/internal/atomic=/home/username/.cache/go-build/4f/4f65044fddff9aced945547fb9cba9b9cb9643657f609a3a4efaeccbc6e2d5cc-d
    // packagefile runtime/internal/math=/home/username/.cache/go-build/03/03a81ab4cc44b1441edd5bf5f877349ba31983e68b88f0877d2f7165ad4f3cec-d
    // packagefile runtime/internal/sys=/home/username/.cache/go-build/e2/e25312a0861f088752b700b121822e28786e686a0698b0dd145b013f4c83aed2-d
    //
    // For each of the files (except command-line-arguments) you will need to
    cp {file path} {IBGC location}/compiler/prebuilt/{target OS}/{target Arch}/{filename}.a

    // In my case, this means that I should copy runtime/internal/sys over like so:
    cp /home/username/.cache/go-build/e2/e25312a0861f088752b700b121822e28786e686a0698b0dd145b013f4c83aed2-d ~/Projects/IBGC/compiler/prebuilt/windows/amd64/runtime/internal/sys.a

## Related Projects
- [ccbrown/wasm-go-playground](https://github.com/ccbrown/wasm-go-playground) - The project IBGC is based on
- [JohnStarich/go-wasm](https://github.com/JohnStarich/go-wasm) - In-browser Go IDE
