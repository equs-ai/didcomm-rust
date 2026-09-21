# Changelog

All notable changes to this fork are documented here.

This is a fork of [sicpa-dlab/didcomm-rust](https://github.com/sicpa-dlab/didcomm-rust),
diverged at `9e79b48`.

### Changed

- `askar-crypto` taken from crates.io instead of a pinned `aries-askar` git
  revision, and pinned to exactly `=0.3.3` (up from 0.2), with `ES384` added to
  `KnownSignatureType` for exhaustiveness; it is not reachable from
  `jws::Algorithm` and is not exposed through the uniffi UDL. The pin is exact
  because 0.3.6 added `ES256ph`, `ES256Kph` and `ES384ph` to `SignatureType`,
  which that match does not cover, so a caret requirement breaks any consumer
  resolving 0.3.6 or later.
- `uuid` gains the `stdweb` feature so v4 generation works on `wasm32`.
- Published as `equs-didcomm`; the library target stays `didcomm`, so
  `use didcomm::…` is unchanged.
