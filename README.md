# DMS ENV

Small wrapper around the [Dead Man's Snitch Field Agent][dms], and a script to
install it.

[dms]: https://deadmanssnitch.com/docs/field-agent

## `dms-env`

`dms-env` behaves like `dms`, except it's:

**ENV-based**: `$DMS_TOKEN` is read from the environment. `dms` requires you
pass it as the first command-line argument.

This makes it possible to use `dms[-env]` directly as an `ENTRYPOINT` or shebang
without having to hard-code a token in the invocation.

**Error-free**: If a token is not found, the command is still run, just without
Snitching. `dms` errors if the token is missing or invalid.

This makes it possible to use `dms[-env]` across multiple environments with
their own (or no) Snitches.

## Usage

```dockerfile
RUN curl -L "https://raw.githubusercontent.com/freckle/dms-env/main/install" | sh
ENTRYPOINT ["dms-env"]
```

```console
docker build --tag your-image .
docker run --rm --env DMS_TOKEN="..." your-image
```

---

[LICENSE](./LICENSE)
