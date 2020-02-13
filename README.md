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
name: GitHub Action

on:
  - push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v2
      - name: galaxy
        uses: robertdebock/galaxy-action@1.0.3
        with:
          galaxy_api_key: ${{ secrets.galaxy_api_key }}
```

Here is a another example that uses molecule to test the role and this Galaxy action to release:

```yaml
name: GitHub Action

on:
  - push

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v2
        with:
          path: "${{ github.repository }}"
      - name: molecule
        uses: robertdebock/molecule-action@1.2.4
  release:
    needs:
      - test
    runs-on: ubuntu-latest
    steps:
      - name: galaxy
        uses: robertdebock/galaxy-action@1.0.3
        with:
          galaxy_api_key: ${{ secrets.galaxy_api_key }}
```
