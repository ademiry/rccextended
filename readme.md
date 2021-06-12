
RccExtended - compiler and ** decompiler ** for binary Qt resources (files with the .rcc extension).

The utility allows you to edit the resources of Qt programs without having their sources.

Editing algorithm:
  
  - unpacking / decompiling binary Qt resources (using this utility)
  - editing unpacked files (.png, .xml, etc.) by third-party tools
  - compilation of edited files back into binary Qt resources (using this utility)

This utility is based on the standard Qt resource compiler, which has added the function 
decompilation of resources (command line switch `--reverse`).

To unpack resources, you need to do 2 things:

  - go to the folder with resources
  - run the utility with the `--reverse` key
  
Once launched, the utility performs the following actions:
  
  - scans working directory looking for .rcc files
  - unpacks all found resource files (each to a separate folder)
  - generates project files .qrc and make.bat for reverse compilation of resources into a binary form
  - outputs to the console and logs information about the progress of unpacking 

Usage example:
```
    cd \Path\To\MyQtResources\
    rcc --reverse
```

# How to build
## OSX instruction for Qt

```bash
cd ./src

# run qmake
~/Qt/5.15.3/clang_64/bin/qmake -r 
~/Qt/5.15.3/clang_64/bin/macdeployqt
# full build
make clean all
```

If you get an error that you can't find the dylibs like 
```
dyld: Library not loaded: @rpath/QtXml.framework/Versions/5/QtXml
```

This is simply because the app is looking for the dylibs in `../Frameworks`
Simply copy them there like
```
cp ~/Qt/5.15.3/clang_64/lib/QtCore.framework ../Frameworks
cp ~/Qt/5.15.3/clang_64/lib/QtXml.framework ../Frameworks
```
