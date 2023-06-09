# GitHub Action: `setup-nomad`

The `nferch/setup-nomad` Action sets up the [Nomad](https://www.nomadproject.io/) CLI in your GitHub Actions workflow by adding the `nomad` binary to `PATH`.

The action is intended to provide the Nomad for CLI use, running an agent is not recommended.

[![GitHub Action: Self-Test](https://github.com/nferch/setup-nomad/actions/workflows/actions-self-test.yml/badge.svg?branch=main)](https://github.com/nferch/setup-nomad/actions/workflows/actions-self-test.yml)

## Table of Contents

<!-- TOC -->
* [GitHub Action: `setup-nomad`](#github-action--setup-nomad)
  * [Table of Contents](#table-of-contents)
  * [Requirements](#requirements)
  * [Usage](#usage)
  * [Inputs](#inputs)
  * [Outputs](#outputs)
  * [Author Information](#author-information)
  * [License](#license)
<!-- TOC -->

## Requirements

This GitHub Actions supports all commands that are available in the `nomad` CLI.

## Usage

1.) Create a GitHub Actions Workflow file (e.g.: `.github/workflows/nomad.yml`):

```yaml
name: nomad

on:
  push:

env:
  PRODUCT_VERSION: "1.5.3" # or: "latest"

jobs:
  nomad:
    runs-on: ubuntu-latest
    name: Run Nomad
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup `nomad`
        uses: nferch/setup-nomad@master
        id: setup
        with:
          version: ${{ env.PRODUCT_VERSION }}

      - name: Run `nomad validate`
        id: validate
        run: "nomad validate "hello-world.nomad"
```

In the above example, the following definitions have been set.

- The event trigger has been set to `push`. For a complete list, see [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows).
- The origin of this GitHub Action has been set as `nferch/setup-nomad@main`. For newer versions, see the [Releases](https://github.com/nferch/setup-nomad/releases).
- The version of `nomad` to set up has been set as `1.5.3`. For a complete list, see [releases.hashicorp.com](https://releases.hashicorp.com/nomad/).

These definitions may require updating to suit your deployment, such as specifying [self-hosted](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#choosing-self-hosted-runners) runners.

Additionally, you may configure [outputs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-defining-outputs-for-a-job) to consume return values from the Action's operations.

## Inputs

This section contains a list of all inputs that may be set for this Action.

- `version` - (required) The version of `nomad` to install. Defaults to `latest`.

## Outputs

This section contains a list of all outputs that can be consumed from this Action.

- `version` -  The version of `nomad` that was installed.

## Author Information

This action is derived from [hashicorp/setup-packer](https://github.com/hashicorp/setup-packer).

The original code of `setup-packer` is based on work done by [Matthew Sanabria](https://github.com/sudomateo) as part of the [setup-packer](https://github.com/sudomateo/setup-packer) GitHub Action.

## License

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations under the License.
