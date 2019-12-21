# Galaxy action

A GitHub action to publish your [Ansible](https://www.ansible.com/) role to [Galaxy](https://galaxy.ansible.com/).

## Requirements

This action expects the following (default Ansible role) structure:
```
.
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── requirements.yml
├── tasks
│   └── main.yml
└── vars
    └── main.yml
```

## Inputs

### `galaxy_api_key`

The API Key for your personal Galaxy account. Found under https://galaxy.ansible.com/me/preferences

## Example usage

```yaml
---
on:
  - push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v2
      - name: galaxy
        uses: robertdebock/galaxy-action@master
        with:
          galaxy_api_token: ${{ secrets.galaxy_api_token }}
```
