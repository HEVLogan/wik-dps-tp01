# WIK-DPS-TP01

Simple HTTP server in Rust (zero external dependencies) that returns request headers as JSON on `GET /ping`.

## Requirements

- [Rust](https://www.rust-lang.org/tools/install) (stable ≥ 1.70)

## Build

```bash
cargo build --release
```

The binary is produced at `target/release/wik-dps-tp01`.

## Run

```bash
# Default port 8080
cargo run --release

# Custom port via environment variable
PING_LISTEN_PORT=3000 cargo run --release

# Or run the compiled binary directly
PING_LISTEN_PORT=3000 ./target/release/wik-dps-tp01
```

## API

### `GET /ping`

Returns a `200 OK` response with all HTTP request headers serialized as a JSON object.

**Example:**

```bash
curl -s http://localhost:8080/ping | jq
```

```json
{
  "host": "localhost:8080",
  "user-agent": "curl/8.4.0",
  "accept": "*/*"
}
```

### Any other route / method

Returns `404 Not Found` with an empty body.

```bash
curl -o /dev/null -w "%{http_code}\n" http://localhost:8080/other
# 404
```

## Configuration

| Variable          | Default | Description          |
|-------------------|---------|----------------------|
| `PING_LISTEN_PORT`| `8080`  | TCP port to listen on |
