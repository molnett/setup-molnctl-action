# Github Action for setting up molnctl

This Github action makes it easier for you to install and configure [molnctl](https://github.com/molnett/molnctl).

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v2
    - name: Molnctl Setup
      uses: molnett/setup-molnctl-action@v1
      with:
        api-token-client-id: ${{ secrets.MOLNETT_CLIENT_ID }}
        api-token-client-secret: ${{ secrets.MOLNETT_CLIENT_SECRET }}
    - name: Switch default org
      run: molnctl orgs switch <your_org>
    - name: Cleanup
      run: rm -r ~/.config/molnett
```

`molnctl` is configured and available after running this action.

### Using a specific version of molnctl

```yaml
    - name: Molnctl Setup
      uses: molnett/setup-molnctl-action@v1
      with:
        version: v0.1.6
        api-token-client-id: ${{ secrets.MOLNETT_CLIENT_ID }}
        api-token-client-secret: ${{ secrets.MOLNETT_CLIENT_SECRET }}
```

## OS support

The action only supports Linux for now.
