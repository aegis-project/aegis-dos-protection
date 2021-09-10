# Configuration

### config.json

The following configuration points are to be set in the config.json file in the root
directory of this project.

* `number_of_worker_threads` : Number of threads that should run through the aegis-pipeline in parallel.
    * type: string
    * Default: the maximum number of threads (aka dpdk-lcores) possible is chosen.
        * if you want the default value to be set simply remove this key-value pair from the config.json file.
    * Minimum: 1. 
    * Maximum: Number of available dpdk-lcores (most likely available Threads) on the system minus 1.


### Command Line Options

The following command line arguments are supported:

* `--config -c`     => Location to config file. Default => **/etc/aegis/aegis.conf**.
* `--dpdk_version`  => print version of dpdk version installed
* `--help -h`       => Print help menu for command line options.
* `--ifname`        => list all interfaces with name
* `--keep_files`    => should generated files be kept after exit
* `--list -l`       => List all filtering rules/settings scanned from config file.
* `--meson_bin`     => print location of the meson binary
* `--log_level`     => set logging level 
* `--test_list`     => test rules list for errors

Commandline instructions will overwrite the configration file settings!

#### Example
```bash
aegis --keep-files --log_level 3 
aegis --ifname
aegis --list
```
### Usage

How to use AEGIS:

#### Compile your own AEGIS 
To compile your AEGIS you need to have all requirements installed; refer to [Getting Started](/getting_started.md).

1. Run `meson build` in your root folder of AEGIS. Meson will collect all necesarry files for you.
2. `cd build` into your build folder
3. Run `ninja` to compile all source code to your system specifiy binaries

#### Simple usage
Call `aegis` to run the AEGIS CLI and start your service. The CLI will guide you trough all possibilities.
