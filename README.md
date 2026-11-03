<!--
SPDX-FileCopyrightText: 2026 roolrz
SPDX-License-Identifier: Apache-2.0
-->

# componentctl

Component lifecycle and route inspection client.

Uses `lib-component` request/reply records over `lib-service-ipc`. Read-only queries
require the observation capability; start, stop and restart require the separate control
capability. The component manager owns lifecycle state and generation changes.

See the [implementation entry](src/main.rs) and [component declaration](component.json)
for the public interfaces, build dependencies and delivered artifacts.

## Usage

In a Native session with the required capabilities:

```sh
componentctl list
componentctl status /journal
componentctl routes /journal
```

## Boundaries

Stateful bootstrap services cannot be restarted through this generic interface. A
command reply describes the manager outcome; it does not grant access to another
component’s capabilities.

## Build and test

Use this checkout inside the [repo-managed workspace](https://github.com/HypeR-Proj/HypeR).
From this repository directory:

```sh
make
make test
```

An absolute `OUT=/path/to/out` selects a shared output directory. The module
entry delegates to build/system, which prepares the installed SDK and declared
dependencies. Native binaries require HypeR; host module checks cover the tests
selected by component.json. A standalone clone does not contain the workspace’s
other source repositories or Native SDK.
