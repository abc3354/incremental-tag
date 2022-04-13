forked from Klover-Fintech/incremental-tag 
 
# Create an incremental tag

It automatically create the tag of the latest version incrementally.

For example, in our case for each module our versions correspond to [framework version number]. [Major version]. [Minor Version]: '8.0.15.45' or '11.0.56.23'or '13.0.1.4'.

This action incrementally updates the minor version so that '8.0.15.45' becomes '8.0.15.46'.

## Input parameters

These are the parameters you can use with the action:

- `flag_branch`: [optional] Flag indicating that the script should look for the lastest tag depending on the branch to which the merge is made. That is, if we are in the branch '8.0' and a merge of a PR is made, it will take the last tag '8.0.15.45' and not '11.0.56.23'.
- `message`: [optional] Message for the tag
- `prev_tag`: [optional] String to be added before the final tag, for example this parameter takes the value 'v' the final tag will be 'v8.0.15.45'.
- `update_odoo_module_version`: [optional] Flag that indicates that these repository is an odoo module, so this actions will update a manifest file.

## Usage

You can use a workflow like this:

```yaml
name: Tagging

on:
  push:
    branches: '8.0'

jobs:
  build:
    name: Bump tag
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Create an incremental release
      uses: Klover-Fintech/incremental-tag@master
      with:
        flag_branch: true
        message: Bump version
        prev_tag: 'v'
        update_odoo_module_version: true
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

