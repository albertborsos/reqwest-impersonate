# reqwest-impersonate

A fork of [reqwest-impersonate](https://github.com/4JX/reqwest-impersonate), designed to provide more functionality and stability

**Notice:** This crate depends on patched dependencies. To use it, please add the following to your `Cargo.toml`.

```toml
[patch.crates-io]
hyper = { git = "https://github.com/4JX/hyper.git", branch = "v0.14.18-patched" }
h2 = { git = "https://github.com/4JX/h2.git", branch = "imp" }
```

## Example

`Cargo.toml`

```toml
reqwest-impersonate = { git = "https://github.com/epicmatthew23/reqwest-impersonate.git", default-features = false, features = [
    "chrome",
    "blocking",
] }
```

`main.rs`

```rs
use reqwest_impersonate::browser::ChromeVersion;

fn main() {
    // Build a client to mimic Chrome 104
    let client = reqwest_impersonate::blocking::Client::builder()
        .chrome_builder(ChromeVersion::V104)
        .build()
        .unwrap();

    // Use the API you're already familiar with
    match client.get("https://yoururl.com").send() {
        Ok(res) => {
            println!("{:?}", res.text().unwrap());
        }
        Err(err) => {
            dbg!(err);
        }
    };
}
```
