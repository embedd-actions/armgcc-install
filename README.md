# xpack-armgcc-install

A dedicated GitHub Action for installing and caching the xpack ARM GCC cross-compiler toolchain. It helps you quickly and automatically configure ARM development environment in your CI/CD pipeline.

## Background

Most GitHub Action runners don't come with pre-installed GCC toolchains required for embedded development. While installation through package managers is possible, it's often time-consuming and impacts CI/CD efficiency.

This Action implements smart caching mechanisms by downloading and extracting the GCC toolchain to the runner.temp directory, significantly improving subsequent build speeds. It's particularly beneficial for projects requiring frequent commits and builds.

## Usage

Add the following configuration to your workflow file (e.g., `.github/workflows/build.yml`):

```yaml
steps:
  - uses: embedd-actions/xpack-armgcc-install@v1
    with:
      version: '12.3.1-1.2'
```

### Available Versions

For available versions, please refer to [Xpack ARM GNU Toolchain Downloads](https://github.com/xpack-dev-tools/arm-none-eabi-gcc-xpack/releases)

### Available Targets

- arm-none-eabi - For bare-metal ARM development
- arm-none-linux-gnueabihf - For ARM Linux development (hard float)
- aarch64-none-elf - For 64-bit ARM bare-metal development
- aarch64-none-linux-gnu - For 64-bit ARM Linux development

### Example Workflow

```yml
name: Build Firmware

on:
  push:
    branches: [ main, dev ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    
    - uses: actions/checkout@v4

    - name: Install ARM GCC
      uses: embedd-actions/xpack-armgcc-install@v1
      with:
        version: '12.3.1-1.2'

    - name: Build Project
      run: arm-none-eabi-gcc --version
```
