# conan-deploy-lipo

Conan custom command to deploy macOS or iOS universal binaries.
This wraps around Conan's full_deploy deployer and then runs `lipo` to
produce universal binaries.

# Installing

The custom command files need to be installed to ~/.conan2/extensions/commands

```
conan config install ./config
```

# Usage

```
cd ./xcode
conan deploy-lipo . -pr x86_64 -pr armv8 -b missing
conan build .
file ./build/Release/example
```

This assumes profiles named x86_64 and armv8 with corresponding architectures.
Universal binaries can only have one binary per architecture but each can have
different settings, e.g. minimum deployment OS:

## x86_64
```
[settings]
arch=x86_64
build_type=Release
compiler=apple-clang
compiler.cppstd=gnu17
compiler.libcxx=libc++
compiler.version=14
os=Macos
os.version=10.13
```

## armv8
```
[settings]
arch=armv8
build_type=Release
compiler=apple-clang
compiler.cppstd=gnu17
compiler.libcxx=libc++
compiler.version=14
os=Macos
os.version=11.0
```

# Limitations

This does not integrate with Conan's generators and is mainly intended
for a standalone Xcode project that does not use a conanfile.
