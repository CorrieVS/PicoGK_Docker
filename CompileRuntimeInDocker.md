# Compile the PickGKRuntime from Source in Docker

While the pre-compiled PicoGKRuntime library is included in `PicoGK/Runtime/linux_x64`, you may want to develop and compile it from source.  Follow these steps.


### Configure and Build the Runtime

Create a Build directory, open a container, and navigate to it:
```
mkdir PicoGKRuntime/Build
pico-start    # if a container is not already running
pico-shell    # to open a shell inside it
cd PicoGKRuntime/Build
```
Configure with cmake, choosing Clang as the compiler:
```
cmake .. -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DCMAKE_CXX_FLAGS=-fPIC
```
Build the source code:
```
make
```

### Copy the Generated Library

Copy the generated shared libaray file to somewhere useful, like `usr/local/lib` in the container:
```
cp lib/picogk.1.0.so /usr/local/lib
```

Be sure to update `PicoGK/PicoGK__Config.cs` to point to the fully defined path of your library, such as `usr/local/lib/picogk.1.0.so`.  The app does not find the library without the full path because it does not appear to consume the `.so` extension correctly using the default config.
