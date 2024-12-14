# [laze]

Ariel OS makes use of the laze build system to run cargo with the
correct parameters for a specific board and application.

laze provides a `laze build -b <board>` command, which in Ariel OS, internally uses `cargo build`.

laze commands are by default applied to the application(s) within the directory laze is run.
For example, when run in `examples/hello-world`, `laze build -b nrf52840dk`
would build the hello-world example for the `nrf52840dk` board.
Alternatively, the `-C` option can be used to switch to the given directory.

For tasks like flashing and debugging, Ariel OS uses laze *tasks*.
laze tasks currently have the syntax `laze build -b <board> [other options] <task-name>`.
For example, to run the hello-world example, the command would be (when in `examples/hello-world`):

    laze -C examples/hello-world build -b nrf52840dk run

laze allows enabling/disabling individual features using [*modules*](#laze-modules), which can be selected
or disabled using `--select <module>` or `--disable <module>`.

laze also allows to override global environment variables using e.g., `-DFOO=BAR`.

> As some tasks may trigger a rebuild, it is necessary to pass the same settings to related consecutive commands:
`laze build -DFOO=1 flash` followed by `laze build -DFOO=other debug` might not
work as expected, as the second command could be rebuilding the application
before starting the debug session.

## laze tasks

- `run`: Compiles, flashes, and runs an application. The [debug output](./debug_logging.md) is printed in the terminal.
- `flash`: Compiles and flashes an application.
- `debug`: Starts a GDB debug session for the selected application.
  The application needs to be flashed using the `flash` task beforehand.
- `flash-erase-all`: Erases the entire flash memory, including user data. Unlocks it if locked.
- `reset`: Reboots the target.
- `tree`: Prints the application's `cargo tree`.

## laze modules

This is an non-exhaustive list of modules that can be used.
Other modules are documented in their respective pages.

- `silent-panic`: Disables printing panics. May help reduce binary size.

[laze]: https://kaspar030.github.io/laze/dev/