# environment-variable-auditor

Check required environment variable names without printing secret values.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "required": [
    "APP_PORT",
    "DB_PASSWORD"
  ],
  "environment": {
    "APP_PORT": "8080"
  }
}
```

Result:

```json
{
  "missing_or_empty": [
    "DB_PASSWORD"
  ],
  "complete": false
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Input may contain secrets; use protected files and avoid recording request bodies.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [cron-field-validator](https://github.com/sal-s-root/cron-field-validator), [directory-size-summary](https://github.com/sal-s-root/directory-size-summary).

## Project status

A small standalone learning exercise using supplied fixtures. The related
[infrastructure toolbox](https://github.com/sal-s-root/infra-toolbox) collects these
checks in one place.

The assigned historical dates form a retrospective learning schedule; this
exercise was created or reconstructed in 2026. See [history and scope](HISTORY.md).
