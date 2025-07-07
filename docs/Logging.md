Quarkdown features ways to log content to standard channels.

- **`.log {message}`** logs to stdout at *info* level (`-Dloglevel=info` or below);
- **`.debug {message}`** logs to stdout at *debug* level (`-Dloglevel=debug` or below);
- **`.error {message}`** throws a runtime error, which is then handled according to the error manager:
  - By default, the error message is logged to stderr (`-Dloglevel=error` or below) and an error [box](box) is shown in the document;
  - If the program was executed in strict mode (`--strict`), a full stack trace is logged to stderr and the program exits.