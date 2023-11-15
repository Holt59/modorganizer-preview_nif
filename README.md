# modorganizer-preview_nif

NIF preview plugin for Mod Organizer 2

For Qt6 builds of MO2 (version 2.5+)

## How to build

Clone this repository with submodules (`git submodule init` then `git submodule update`).

```bash
# set QT_ROOT to your Qt 6.5.0 installation
cmake -B build -DQT_ROOT="C:/Qt/6.5.3/msvc2019_64" .

# build everything
cmake --build build --config RelWithDebInfo -j4
```

This will generate `preview_nif.dll` under `build\src\RelWithDebInfo\preview_nif.dll`
that you can copy to your MO2 `plugins` folder.
