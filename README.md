# zephyr-t3-template
Zephyr RTOS T3 Topology Template. A **T3 (forest) topology** is a workspace where a there is no main application. A manifest repo (like this one) owns the west manifest and defines the workspace configuration.

Read more about topologies [here](https://docs.zephyrproject.org/latest/develop/west/workspaces.html).


The `setup.sh` script initializes the west workspace, sets the manifest path,
and configures west to place all dependencies under `deps/`. The workspace will look like:

``` 
.
├── .west
│   └── config
├── application1
│   ├── .git
│   ├── .gitignore
│   ├── CMakeLists.txt
│   ├── LICENSE
│   ├── README.md
│   ├── prj.conf
│   ├── setup.sh
│   ├── src
│   │   └── main.c
│   └── west.yml
├── application2
│   ├── .git
│   ├── .gitignore
│   ├── CMakeLists.txt
│   ├── LICENSE
│   ├── README.md
│   ├── prj.conf
│   ├── setup.sh
│   ├── src
│   │   └── main.c
│   └── west.yml
├── manifest-repo
│   ├── .git
│   ├── LICENSE
│   ├── README.md
│   ├── setup.sh
│   └── west.yml
├── deps
└── build
```

## Installation & Setup 
Install the toolchain or use a container.

```sh
mkdir workspace && cd workspace
git clone https://github.com/snhobbs/zephyr-t3-template
sh zephyr-t3-template/setup.sh
west update
```

This places the dependencies, including zephyr, in the workspace in directory `deps`. This keeps the workspace from getting cluttered, leaving most of the visual space for consequential locations like the projects. This path needs to agree with `path-prefix: deps` in `west.yml`.


If the project directory is renamed after setup, setup.sh must be re-run so west can update the manifest path.

Edit the west.yml to add different projects that will be fetched with `west update`. If you don't want west to manage these then you can just leave the projects out of the manifest file.

## Building 
Once setup is complete, build from the workspace root.

```sh 
west build application1
west build application2
```

