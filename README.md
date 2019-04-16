# mii
[![Build Status](https://travis-ci.com/codeandkey/mii.svg?branch=master)](https://travis-ci.com/codeandkey/lmc)

lightweight module cache

mii automatically caches and loads environment modules for you. It works by hooking into your shells' "command not found" event and using that opportunity to see if any modules
would provide your command.

Normal shell:
~~~
[molecuul@pine ~]$ mcl
bash: mcl: command not found
[molecuul@pine ~]$ module load mcl
[molecuul@pine ~]$ mcl
[mcl] usage: mcl <-|file name> [options], do 'mcl -h' or 'man mcl' for help
~~~

mii-enabled shell:
~~~
[molecuul@pine ~]$ mcl
[mii] autoloading mcl/14-137-4aumkvp..
[mcl] usage: mcl <-|file name> [options], do 'mcl -h' or 'man mcl' for help
~~~

mii will prompt you if multiple modules can provide your command:
~~~
[molecuul@pine ~]$ ace2sam
[mii] select a module to load:
    1) samtools/1.8-r54nmop
    2) samtools/1.6-lyscjka
    3) samtools/1.7-kglvk7q
[mii] enter a selection (1-3, q to abort) [1]: 2
[mii] loading samtools/1.6-lyscjka..
Usage:   ace2sam [-pc] <in.ace>
~~~

mii will help you remember commands as well:
~~~
[molecuul@pine ~]$ iseg
iseg: command not found
[mii] hint: try a similar command "iSeg_py" "iSeg_csv2xlsx.py" "iSeg"
[molecuul@pine ~]$ iSeg
[mii] autoloading iseg/1.3.0-oqdecre..
~~~

### features

- Streamlined module environment
- Blazing speed (caches ~70,000 binary entries / second on my machine)
- Lightweight source, few dependencies
- [Lmod](https://lmod.readthedocs.io/en/latest/) module support
- [Tcl](https://modules.readthedocs.io/en/latest/) module support

### dependencies

- Not technically _required_, but you should have Lmod or Environment Modules installed
- SQLite headers and libraries (Arch: `sqlite`, Ubuntu, Debian: `libsqlite3-dev`)
- CMake >=2.6

### installation

- Clone the repository: `git clone https://github.com/codeandkey/mii`
- Generate the makefiles: `cd mii; mkdir build; cd build; cmake ..`
- Build and install: `make && sudo make install`
- `bash` users: `echo "source /usr/local/share/mii/init/bash" >> ~/.bashrc`
- `zsh` users: `echo "source /usr/local/share/mii/init/zsh" >> ~/.zshrc`
