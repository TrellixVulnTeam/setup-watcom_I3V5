# Setup Watcom

**setup-watcom** is a JavaScript GitHub Action (GHA) to setup an [Open Watcom](https://github.com/open-watcom) environment
 using the GHA [toolkit](https://github.com/actions/toolkit) for automatic caching.

This action sets up watcom for use in actions by:

- downloading a watcom release.
- eventually setting the PATH and WATCOM environment variables.
- failing if the specific version of Open Watcom is not available for download.

# Usage

See [action.yml](action.yml)

Basic:
```yaml
steps:
- uses: open-watcom/checkout@v2
- uses: open-watcom/setup-watcom@v0
- run: |
    wcl386 -zq -d+ ${{ env.WATCOM }}/h -w3 -bt=dos -d2 -fomain.c.obj -c -cc main.c
    wlink option quiet name hello.exe opt map system dos4g debug all file main.c.obj
- run: |
    cmake -S . -B build -G "Watcom WMake" -D CMAKE_SYSTEM_NAME=DOS
    cmake --build build
```
