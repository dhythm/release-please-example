# `release-please` example

This repository is to survey [relase-please](https://github.com/googleapis/release-please), and take notes for the useage.

## GitHub Actions

You need to open `Settings` > `Actions` > `General` and check `Allow GitHub Actions to create and approve pull requests` in Workflow permissions if you get error as `release-please failed: GitHub Actions is not permitted to create or approve pull requests.`


A release PR will be created when commit(s) that includes Conventional Commit messages is merged in target branch of GitHub Actions.
