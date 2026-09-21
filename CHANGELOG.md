# Changelog

All notable changes to this fork are documented here.

This is a fork of [sicpa-dlab/didcomm-rust](https://github.com/sicpa-dlab/didcomm-rust),
diverged at `9e79b48`.

### Changed

- `askar-crypto` taken from crates.io instead of a pinned `aries-askar` git
  revision, and bumped 0.2 → 0.3.3, with `ES384` added to `KnownSignatureType`
  for exhaustiveness; it is not reachable from `jws::Algorithm` and is not
  exposed through the uniffi UDL.
- `uuid` gains the `stdweb` feature so v4 generation works on `wasm32`.
- `askar-crypto` pinned to exactly `=0.3.3`. 0.3.6 added `ES256ph`, `ES256Kph`
  and `ES384ph` to `SignatureType`, which the `KnownSignatureType` match does not
  cover, so a caret requirement breaks any consumer that resolves 0.3.6 or later.
- Published as `equs-didcomm`; the library target stays `didcomm`, so
  `use didcomm::…` is unchanged.
