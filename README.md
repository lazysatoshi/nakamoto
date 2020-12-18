nakamoto
========

Nakamoto is a high-assurance Bitcoin light-client implementation in Rust, with
a focus on low resource utilization, modularity and security.

The vision for the project is to build a set of libraries that are easy to
embed in any program and on any platform, be it mobile or desktop. The
project's small cpu, memory and code footprint is made possible by its
efficient runtime and minimal set of dependencies. The implementation
language, Rust, opens up the possibility for programs written in other
languages (eg. Swift, Python, Java), to bind directly to it via a foreign
function interface (FFI).

## Design

Nakamoto is split into several crates, each handling a different aspect of the
light-client protocol. Although these crates are designed to be used in tandem,
swapping implementations is trivial, due to the explicit boundaries between
them. From a high-level, we have:

* `nakamoto-client`: the core light-client library
* `nakamoto-p2p`: the protocol state-machine implementation
* `nakamoto-chain`: the block store and fork selection logic
* `nakamoto-net-poll`: the default *poll*-based networking library
* `nakamoto-common`: common functionality used by all crates
* `nakamoto-node`: a standalone light-client daemon

## Status

While the project is still in its infancy, the base functionality has been
implemented. Nakamoto is able to discover peers, download and verify the
longest chain and handle forks, while implementing the full header verification
protocol.

Client side block filtering (BIP 157/158) is in the works, and is the next
major milestone.

Once peer-to-peer layer encryption (BIP 151) lands in Core, it will also
be implemented in Nakamoto.

Finally, a C FFI will be implemented, to make it easy to embed the client
in mobile applications.

## Projects goals

* __High assurance__: the library should be thoroughly tested using modern
  techniques such as *property* and *model-based testing* as well as *discrete
  event simulation* and *fuzzing*. These approaches benefit from a clean
  separation between I/O and protocol logic and have been shown to catch more
  bugs than unit testing.

* __Security__: as a library that may find its way into wallet implementations,
  a primary goal is security and auditability. For this reason, we try to
  minimize the total dependency footprint, keep the code easy to read and
  forbid any unsafe code.

* __Efficiency__: blockchain synchronization should be done as efficiently as
  possible, with low memory and disk overhead. We target resource-constrained
  environments, such as mobile.

* __Privacy__: when possible, privacy-preserving techniques should be employed.
  For example, *Client Side Block Filtering* (BIP 157/158) should be used over
  bloom filters (BIP 37) to ensure user privacy.

## Contributing

If you'd like to contribute to the development of Nakamoto, please get in touch!

## Usage

In your *Cargo.toml*:

    [dependencies]
    nakamoto = "0.1.0"

## Running the tests

    cargo test --all

## Donations

To help fund the project and ensure its ongoing development and maintenance, your
support in Bitcoin is appreciated at the following address:

    bc1qa47tl4vmz8j82wdsdkmxex30r23c9ljs84fxah

## License

Licensed under the MIT license.
&copy; 2020 Alexis Sellier (<https://cloudhead.io>)
