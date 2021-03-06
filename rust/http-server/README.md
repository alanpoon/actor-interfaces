# HTTP Server Actor Interface

This crate provides waSCC actors with an interface to the HTTP Server capability provider. Actors using this
interface must have the claim `wascc:http_server` in order to have permission to handle requests, and they
must have an active, configured binding to an HTTP Server capability provider.

The HTTP Server provider is one-way, and only delivers messages to actors. Actors cannot make host calls
to this provider.

The following is an example of how to use this provider:

```rust
extern crate actor_http_server as http;

#[no_mangle]
pub fn wapc_init() {
    http::Handlers::register_handle_request(increment_counter);
}

#[macro_use]
extern crate serde_json;

fn increment_counter(msg: http::Request) -> HandlerResult<http::Response> {
    Ok(http::Response::ok())
}
```

