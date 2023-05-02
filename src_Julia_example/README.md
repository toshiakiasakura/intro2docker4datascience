# Docker for Julia

In this directory, the followings are prepared.  
- Package management with the default Julia function.  
- Multi-thread setting.  
- Use of PrecompilePackage.  

## Package management and PackageCompiler setting.
Julia programming language provides the package management system.
It is simple to maintain the package dependencies by files `Manifest.toml` and `Project.toml`.
Therefore, in Dockerfile, we do not explicitly write the package installation commands.  

First, comment out all codes below `ENV JULIA_PROJECT=/workdir` 
since we do not have `Manifest.toml`, `Project.toml` or other files 
when you prepare the contents.

Then, launch up the container and run the code 
```
using Pkg
Pkg.activate(".")
Pkg.add("FreqTables")

Pkg.add("PackageCompiler")
using PackageCompiler
create_sysimage(["FreqTables"], sysimage_path="freqtables.so")
```
which generates `Manifest.toml` and `Project.toml`. 
For the second run, you can comment in code which previously is commented out. 
Then other people can reproduce your results by `docker compose up`.

The last bunch of code are for creating sysimage.
Then, you comment in codes, and can use Julia with precompiled packages.

Note: You have to COPY files such as "Manifest.toml", "Project.toml", and "freqtables.so" to
workdir directory in Dockerfile, since volume mounting is conducted after you launch the container.
It means when you create a docker image, the `workdir` directory is empty!

### PackageCompiler.
Taking long time to load the package is serious issue in Julia programming. 
At least, we want to precompile graphical pacakges such as CairoMakie, Plots, and Gadfly.  
For illustration purpose, we precompile FreqTables and use in Jupyter lab.


