# gradle-dependency-downgrade

A toy project to predict how Gradle handles publication of dependencies which are upgraded at compile-time.

## Description
This project has two subprojects, `api` and `impl`.

`api` depends on `commons-lang:commons-lang:2.6`

`impl` depends on `commons-lang:commons-lang:2.3` and `api`

At compile-time and runtime for `impl`, Gradle will use `commons-lang:commons-lang:2.6`.  However, `2.3` will end
up in `impl`'s ivy descriptor.

## Steps to reproduce

1. `$ ./gradlew :impl:generateDescriptorFileForMyLibraryPublication`
2. `cat impl/build/publications/myLibrary/ivy.xml`
3. Note that `commons-lang:commons-lang:2.3` is listed.