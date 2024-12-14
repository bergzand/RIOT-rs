# storage

## About

This application demonstrates use of the
[ariel-os-storage](https://ariel-os.github.io/ariel-os/dev/docs/api/ariel_os/storage/index.html)
API.

Note: The application is not stateless, as it writes to flash.

## How to run

In this folder, run

    laze build -b nrf52840dk run

The application will store and read back a value to the flash.

When the maximum number of cycles have been reached
and the application exits early, the `flash-erase-all` command can be used:

    laze build -b nrf52840dk flash-erase-all
