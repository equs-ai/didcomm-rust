# Changelog

All notable changes to this fork are documented here.

This is a fork of [sicpa-dlab/didcomm-rust](https://github.com/sicpa-dlab/didcomm-rust),
diverged at `9e79b48`.

## 0.1.2

### Fixed

- `Message::unpack` rejects an encrypted message whose plaintext `to` does not
  contain the DID of the recipient `kid` (DIDComm Messaging v2.1, Message Layer
  Addressing Consistency). A `to` element may be a DID URL without a fragment,
  as the `to` header allows; its DID is what is compared.
- `Message::unpack` compares the DID of `from` with the authcrypt `skid` and the
  signer `kid`, so a `from` that is a DID URL without a fragment, as the `from`
  header allows, is no longer rejected.
- `Message::unpack` rejects any message whose `from` or a `to` element is not a
  DID or a DID URL without a fragment, whatever its layers.
- `Message::pack_encrypted` accepts a plaintext whose `to` or `from` is a DID URL
  without a fragment, comparing its DID with the `to` and `from` arguments, so
  it can send what `Message::unpack` accepts. It rejects a `to` or `from`
  header with a fragment, and a `to` or `from` argument with a path or query.
- `Message::pack_plaintext` compares `from_prior.sub` with the DID of `from`, so
  a DID rotation message can have a `from` that is a DID URL.

## 0.1.1

### Fixed

- `Message::unpack` rejects a message whose plaintext `from` is not the DID of
  the authcrypt `skid` or of the signer `kid` (DIDComm Messaging v2.1, Message
  Layer Addressing Consistency).

## 0.1.0

### Changed

- `askar-crypto` comes from crates.io instead of a pinned `aries-askar` git
  revision, at `=0.3.3` (up from 0.2). The pin is exact: 0.3.6 added prehashed
  `SignatureType` variants that `KnownSignatureType` does not cover. `ES384`
  added for exhaustiveness.
- `uuid` gains the `stdweb` feature so v4 generation works on `wasm32`.
- Published as `equs-didcomm`; the library target stays `didcomm`, so
  `use didcomm::…` is unchanged.
