# setup-smalltalkCI

This GitHub Action sets up [smalltalkCI] for testing Smalltalk projects. It's using ba-st fork waiting for some changes in the upstream project.

## Usage

### Basic

```yaml
steps:
  - uses: actions/checkout@v2
  - uses: ba-st-actions/setup-smalltalkCI@v1
    id: smalltalkci
    with:
      smalltalk-version: 'Squeak64-trunk'
  - run: smalltalkci -s ${{ steps.smalltalkci.outputs.smalltalk-version }}
    timeout-minutes: 15
```

### Matrix Testing

```yaml
jobs:
  build:
    strategy:
      matrix:
        smalltalk: [ Squeak64-trunk, Pharo64-stable ]
    name: ${{ matrix.smalltalk }}
    steps:
      - uses: actions/checkout@v2
      - uses: ba-st-actions/setup-smalltalkCI@v1
        with:
          smalltalk-version: ${{ matrix.smalltalk }}
      - run: smalltalkci -s ${{ matrix.smalltalk }}
        timeout-minutes: 15
```

[smalltalkCI]: https://github.com/hpi-swa/smalltalkCI
