# AlliewayAudio_Freebies
Free and open source VCVrack modules made by Allieway Audio with love <3 

Disclaimer: All direct clones or recreations were made with permission from their respective manufacturers.

## Building For MetaModule

Check this repo out into a ```<projects-dir>/AlliewayAudio_Freebies``` folder

then:

```
cd <project-dir>
mkdir metamodule-plugins
git clone https://github.com/4ms/metamodule-plugin-sdk --recursive
```

NB: If pulling latest commit of ```metamodule-plugin-sdk```, run:

```
cd git submodule update
git submodule update --recursive
```



```
cd AlliewayAudio_Freebies
cmake -B build -G Ninja -DTOOLCHAIN_BASE_DIR=<path-to-arm64-arm-none-eabi>/bin
cmake --build build

```

This will build a new ```<project-dir>/metamodule-plugins/AlliewayAudio_Freebies.mmplugin``` plugin install file