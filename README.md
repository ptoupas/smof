# SMOF
A tool for automated mapping and optimization of modern CNNs on FPGAs with smart off-chip eviction

## Cloning the repository
In order to clone the repository, you can use the following command:

```
git clone --recurse-submodules https://github.com/ptoupas/smof.git
```

## Requirements

To use this tool, you will need to meet the following requirements:

- Python 3.9 or higher
- Install python packages listed in `requirements.txt`
- Install fpgaconvnet-optimiser, fpconvnet-model, and fpgaconvnet-torch packages as described in the relevant section below

## Python dependencies

To install the necessary Python packages, you can use `pip`. Navigate to the root directory of the repository and execute the following command:

```
cd smof
pip install -r requirements.txt
```

This will install all the required Python packages specified in the `requirements.txt` file.


## Installing fpgaconvnet-optimiser and fpgaconvnet-model

The `smof` tool uses the `fpgaconvnet-optimiser`, `fpgaconvnet-model`, and `fpgaconvnet-torch` packages to map and optimize modern CNNs onto FPGA devices. These packages are included as submodules in the `smof` repository. To install them, you should first initialize the submodules (in case you haven't cloned the repository with the `--recurse-submodules` flag):
```
git submodule update --init --recursive
```

Then, (from the root directory) navigate to the `fpgaconvnet-optimiser` directory and install the package:
```
cd fpgaconvnet-optimiser
pip install .
```

Concequently, (from the root directory) navigate to the `fpgaconvnet-model` directory and install the package:
```
cd fpgaconvnet-model
pip install .
```

The `fpgaconvnet-torch` does not require installation as a package. You can use its scripts directly from the submodule directory.

## Usage

```bash
-m fpgaconvnet.optimiser.sweep_wandb -n unet -m examples/models/unet_nncf_bilinear_huffman.onnx -p examples/platforms/u200.toml -o outputs/unet/nncf_bilinear_huffman/throughput/u200 -b 1 --objective throughput --optimiser greedy_partition --optimiser_config_path examples/optimisers/greedy_partition_throughput_unet.toml --enable-wandb --sweep-wandb --custom_onnx --encode huffman
```