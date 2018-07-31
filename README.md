# Template esp-idf project for Qt Creator

This directory is a template for Qt creator to initialize an almost empty project, it 
comes with the standard hello_world provided in the esp-idf library. To use it:

1. Copy this template to a new directory `cp -rv esp-template-qtcreator hello_world`
2. Rename app.pro to your project name: `mv app.pro hello_world.pro`
3. Run `make menuconfig` _outside_ Qt creator from a terminal
4. Open the .pro file in Qt creator, the 'Kit' can be anything, but you may want to
   create an extensa kit later.
5. Open main/main.c, if the CLangCodeModel plugin is enabled you should get realtime 
   errors in red (there should be none) and some yellow warnings. Make sure code
   completion works by typing eg. `esp_<tab>`.
6. If you also want to build/deploy from Qt Creator go to "Projects" in the sidebar
  - Select "Build" to select the "Build settings" if it's not yet selected.
  - Under general, disable 'shadow build'
  - Under build steps, remove everything and "Add build step->Make" with argument "all"
  - Under clean steps, remove everything and "Add build step->Make" with argument "clean"
  - Select "Run" to select the "Run settings" if it's not yet selected.A
  - Under deployment, select "Add Deploy step->Make" with argument "flash"
  - Under run, remove everything and add "Custom Executable" with "/usr/bin/cmake", 
    arguments "monitor", and working directory: "%{CurrentProject:Path}", check "run 
    in terminal"
7. Check if clean and build works in the menu and sidebar, run should now default to
   a make clean and run the serial monitor in a terminal.

## Notes/TODO:

- Most of the .pro file has been borrowed from the
  [platformio](http://www.platformio.org) project. Since we may be using
  a newer version of esp-idf the INCLUDEPATHS might need to change.

- If you add a component you manually need to add it in the .pro file,
  an example is included at the bottom of the file. 

- If you get sdkconfig.h not found error try running `make menuconfig`
  since that creates build/include/sdkconfig.h

- There is a
  [cmake](https://docs.espressif.com/projects/esp-idf/en/feature-cmake/api-guides/build-system.html)
  version of esp-idf in the works, and QtCreator natively support cmake
  now, I could not get this to reliably work, but it's probably what you
  want when it's integrated into mainline.
