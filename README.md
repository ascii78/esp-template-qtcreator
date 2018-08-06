# Template esp-idf project for Qt Creator

This directory is a template for Qt creator to initialize an almost empty project, it
comes with the standard hello_world provided in the esp-idf library. To use it:

1. Make sure you have the esp-idf and extensa toolchain installed as per the
   documentation.
2. Copy this template to a new directory `cp -rv esp-template-qtcreator hello_world`
3. Rename app.pro to your project name: `mv app.pro hello_world.pro`
4. Run `make menuconfig` _outside_ Qt creator from a terminal
5. Open the .pro file in Qt creator, the 'Kit' can be anything, but you may want to
   create an extensa kit later.
6. Open main/main.c, if the CLangCodeModel plugin is enabled you should get realtime
   errors in red (there should be none) and some yellow warnings. Make sure code
   completion works by typing eg. `esp_<tab>`.

Sometimes ClangCodeModel does not seem to work properly and will not
give any code completions or hints, it's best to turn it off under
help->about plugins.

## Build/Deploy

The build/deploy settings for Qt Creator are stored in the *.pro.user file, I
could not get a generic one to include in this template. The manual steps are:

1. Go to "Projects" in the sidebar
2. Select "Build" to select the "Build settings" if it's not yet selected.
3. Under general, disable 'shadow build'
4. Under build steps, remove everything and "Add build step->Make" with argument "all"
5. Under clean steps, remove everything and "Add build step->Make" with argument "clean"
6. Select "Run" to select the "Run settings" if it's not yet selected.A
7. Under deployment, select "Add Deploy step->Make" with argument "flash"
8. Under run, remove everything and add "Custom Executable" with "/usr/bin/cmake",
9. arguments "monitor", and working directory: "%{CurrentProject:Path}", check "run
10. in terminal"
11. Check if clean and build works in the menu and sidebar, run should now default to
    a make clean and run the serial monitor in a terminal.
12. Remove the .git directory and README.mdif you're planning to use your own.

## Screenshot

![screenshot](https://user-images.githubusercontent.com/1138654/43473749-4c3cd0d6-94f1-11e8-877d-586074fff738.png)

## Notes/TODO

- Most of the .pro file has been borrowed from the
  [platformio](http://www.platformio.org) project. Since we may be using
  a newer version of esp-idf the INCLUDEPATHS might need to change.
- If you add a component, you manually need to add it in the .pro file,
  an example is included at the bottom of the file.
- If you get sdkconfig.h not found error try running `make menuconfig`
  since that creates build/include/sdkconfig.h.
- There is a
  [cmake](https://docs.espressif.com/projects/esp-idf/en/feature-cmake/api-guides/build-system.html)
  version of esp-idf in the works, and QtCreator natively supports cmake
  now, I could not get this to reliably work yet, but it's probably what you
  want when it's integrated into mainline.
