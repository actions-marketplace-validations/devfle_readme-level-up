# Read Me Level Up

Readme level up is a small action that converts interactions made on GitHub into experience points. If you have enough experience points your level increases. The action suits perfectly for the profile page on Github.

<img width="875" alt="01" src="https://user-images.githubusercontent.com/52854338/206877769-3463c59a-af0b-4fab-bde4-aec71ecfb5c2.png">


# Setup Action

I explain here how to set up the action. The Github profile readme serves as an example. But any other readme can be used as well.

1. Add the following comments to your readme file:

```text
<!--README_LEVEL_UP:START-->
<!--README_LEVEL_UP:STOP-->
```

2. create a new workflow with the following example content.


# Example Action Setup

```yml
name: Update Readme Level
on:
  workflow_dispatch:
  schedule:
    - cron: '0 08 * * *'
jobs:
  update-readme:
    runs-on: ubuntu-latest
    steps:
      - name: checkout project
        uses: actions/checkout@v3
      - name: update markdown file
        uses: devfle/readme-level-up@main
        with:
          github_username: GITHUB_USERNAME
          github_token: ${{ secrets.GITHUB_TOKEN }}
      - name: commit markdown file
        run: |
          git config --local user.email "github-actions[bot]@users.noreply.github.com"
          git config --local user.name "github-actions[bot]"
          git commit -a -m "update readme"
      - name: push changes
        uses: ad-m/github-push-action@v0.6.0
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: main
```



# Environment Variables

All available environment variables and their default values can be found in the [action.yml file.](../main/action.yml)

# Todos
I started the project because I had a fun idea and wanted to learn Python. Some things still need to be done:
- add types to all vars
- add error management
- add more data to level calculation
- add more options as env vars
- and more...

If you have any ideas about what could be optimized, feel free to create an issue.

# Contribution Guide

I appreciate any support with this project. If you have a suggestion for improvement or found a bug, please create a new issue. Please make sure that there is not already an existing issue for your request.

- This project uses the conventional [commits specification.](https://www.conventionalcommits.org/en/v1.0.0/#specification)
- Currently Python 3.11 is used.
- For development, we recommend the usage of the VS-Code Python linter from Microsoft.
- Please test your changes before opening a new merge request.


