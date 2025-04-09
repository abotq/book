# trace/log

Overview
tracing is a framework for instrumenting Rust programs to collect structured, event-based diagnostic information. tracing is maintained by the Tokio project, but does not require the tokio runtime to be used.
https://github.com/tokio-rs/tracing

## crate

### tracing

https://docs.rs/tracing/latest/tracing/

### tracing_subscriber

https://docs.rs/tracing-subscriber/latest/tracing_subscriber/
Utilities for implementing and composing tracing subscribers.

### tracing_log

https://docs.rs/tracing-log/latest/tracing_log/
Adapters for connecting unstructured log records from the log crate into the tracing ecosystem.

### env_logger

A simple logger that can be configured via environment variables
https://docs.rs/env_logger/latest/env_logger/

### log

https://docs.rs/log/0.4.26/log/index.html
A lightweight logging facade.

## differences

log 和其他前端显示如 env_logger 组合可以实现 logger
tracing 与其他可以实现在 async 世界的 logger？

## references

https://tokio.rs/tokio/topics/tracing
https://www.shuttle.dev/blog/2024/01/09/getting-started-tracing-rust
