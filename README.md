# bash-static-musl

Downloads source and compiles Bash with static linking to the Musl standard C library.  

Clone the repo:

``` 
git clone https://github.com/sapeurfaire/bash-static-musl.git
```
Run the build:

```
build.sh [TARGET_OS] [TARGET_ARCH] [VERSION_TAG] 
```

Parameters are optional for a build that targets:
- the build host
- the most recent version of Bash

To cross-compile, supply the target os and architecture:

``` 
bash-static-musl/build.sh linux x86_64 
```

To build for a prior version, supply a tag matching one of the 'version-[TAG].sh' files:

```
bash-static-musl/build.sh macos x86_64 42 
```

To change patch level for Bash or specify a different Musl, supply a spec file.  Use one of the existing 'version-[TAG].sh' files as a template.  Update the softlink to point to your custom spec, and run the build:

```
cd bash-static-musl
cp version-53.sh my_spec_file.sh
sed -i.bak 's/bash_patch_level=9/bash_patch_level=8/' my_spec_file.sh
ln -fs my_spec_file.sh version.sh
./build.sh macos x86_64 
```
The resulting executable will be in the ***releases*** subdirectory.

## Credit/Attribution:

Forked from [robxu9/bash-static](https://github.com/robxu9/bash-static)

The [original](https://github.com/robxu9/bash-static/blob/master/README.md) noted (summarizing; see the original for full text):

- Use of Musl avoids glibc dlopen() on linux
- Bash will use Mac/Win libc as they do not support static binaries
- Script resulted from containerization project

