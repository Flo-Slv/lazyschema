# lazyschema

A terminal UI for reading Prisma schemas, written in Rust.

> **Status: planned, not yet implemented.**
> The idea and the scope were settled in September 2026. Work starts in
> January 2027. There is no code and nothing to install yet — this README
> describes what the tool is meant to be, so the intent is on the record
> before the first line is written.

## Why

Prisma lets a schema live as a **folder of `.prisma` files** rather than a
single one — declared through the `prisma.schema` field of `package.json`.
It is a good way to keep a large data model readable, and most third-party
tooling handles it poorly or not at all.

`lazyschema` starts from that folder, treats it as one model, and lets you read
it without leaving the terminal: models, fields, relations, indexes, and the
ability to jump from a relation to the model it points at.

## Scope

**What the first version will do**

- Locate the schema: single file, folder, or the `prisma` field of `package.json`
- Aggregate every `.prisma` file of a folder into one model
- List models in a pane, with vim-style navigation and filtering
- Show a model in detail: fields, types, optionality, defaults, indexes, keys
- Jump from a relation to the related model, and back
- One binary, no configuration

**What it will not do**

- Write anything. The first version is read-only.
- Reimplement migrations. `prisma migrate` diffs a schema against a live
  database, and that logic lives in Prisma's own schema engine — tens of
  thousands of lines, with per-database knowledge behind them. Reimplementing
  it could only ever be a less correct copy. A later version will **call**
  `prisma migrate`, `generate` and `validate`, and present their output.
- Connect to a database. A schema is a set of files; reading it needs no
  server. Existing SQL clients already cover live data.
- Support other schema languages. Prisma only.

## Built on

- [`ratatui`](https://github.com/ratatui/ratatui) and
  [`crossterm`](https://github.com/crossterm-rs/crossterm) for the interface
- Prisma's own schema parser (the `psl` crate of
  [`prisma-engines`](https://github.com/prisma/prisma-engines), Apache-2.0)
  rather than a hand-written one — the format is theirs, and so is the
  authority on it

## Not affiliated with Prisma

`lazyschema` is an independent project. Prisma is a trademark of its owners,
and this tool is neither endorsed by nor connected to them.

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  <http://www.apache.org/licenses/LICENSE-2.0>)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or
  <http://opensource.org/licenses/MIT>)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
