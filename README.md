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
      uses: molnett/setup-molnctl-action@v2
      with:
        api-token-client-id: ${{ secrets.MOLNETT_CLIENT_ID }}
        api-token-client-secret: ${{ secrets.MOLNETT_CLIENT_SECRET }}
        default-tenant: <your-tenant-id>
        default-project: <your-project-id>
    - name: Build & Push Image to Molnett
      run: |
        molnctl auth docker
        IMAGE_NAME=`molnctl svcs image-name --update-manifest molnett.yaml`
        docker buildx build . -t $IMAGE_NAME
        docker push $IMAGE_NAME
    - name: Deploy Service
      run: molnctl deploy
    - name: Cleanup
      run: rm -r ~/.config/molnett
```

`molnctl` is configured and available after running this action.

### Using a specific version of molnctl

```yaml
    - name: Molnctl Setup
      uses: molnett/setup-molnctl-action@v2
      with:
        version: v0.5.0
        api-token-client-id: ${{ secrets.MOLNETT_CLIENT_ID }}
        api-token-client-secret: ${{ secrets.MOLNETT_CLIENT_SECRET }}
        default-tenant: <your-tenant>
        default-project: <your-project>
```

## OS support

The action only supports Linux for now.
