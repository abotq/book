# config

[link](https://github.com/rust-cli/config-rs)

Layered configuration system for Rust applications (with strong support for 12-factor applications).

Set defaults
Set explicit values (to programmatically override)
Read from JSON, TOML, YAML, INI, RON, JSON5 files
Read from environment
Loosely typed — Configuration values may be read in any supported type, as long as there exists a reasonable conversion
Access nested fields using a formatted path — Uses a subset of JSONPath; currently supports the child ( redis.port ) and subscript operators ( databases[0].name )

> Please note that this library can not be used to write changed configuration values back to the configuration file(s)!

## references

1. https://12factor.net/config

## examples

https://github.com/rust-cli/config-rs/tree/main/examples
