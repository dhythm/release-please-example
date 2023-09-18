# `release-please` example

This repository is to survey [relase-please](https://github.com/googleapis/release-please), and take notes for the useage.

## GitHub Actions

You need to open `Settings` > `Actions` > `General` and check `Allow GitHub Actions to create and approve pull requests` in Workflow permissions if you get error as `release-please failed: GitHub Actions is not permitted to create or approve pull requests.`

### How to use

A release PR will be created when commit(s) that includes Conventional Commit messages is merged in target branch of GitHub Actions.

So, Linear git commit history (via squash-merge) is highly recommended by the maintainers.

#### Restrict only squash-merge

Go to `Settings` > `General` > `Pull Request`, then uncheck `Allow merge commits` and `Allow rebase merging` and change `Default to pull request title` for `Allow squash merging`.

[GitHub Apps](https://github.com/marketplace/semantic-prs) and [GitHub Actions](https://github.com/amannn/action-semantic-pull-request) would help you to make PR title semantic.


#### Restrict linear git commit history

Go to `Settings` > `Branches`, then add a branch protection rule.
Branch name pattern is `main` and check `Require linear history`.

You can protect from miss-pushing to a branch if you check `Require a pull request before merging`.

#### Follow the target branch's update

The release PR will be updated when a new commit is merged.
Following pictures are example of the above feature.

![image](./assets/img/Screenshot_2023-08-19_at_19.55.53.png)

![image](./assets/img/Screenshot_2023-08-19_at_20.03.56.png)

Bug-fix is also included in the minor version up.

![image](./assets/img/Screenshot_2023-08-19_at_20.11.36.png)

#### Change the version number

a commit to the main branch has `Release-As: x.x.x` (case insensitive) in the commit body.
In GitHub, the following operations didn't work.

- Including `Release-As: x.x.x` in PR body via squash merging
- Including `Release-As: x.x.x` in PR title via squash merging

Forced version changing works with `merging commit`.

![image](./assets/img/Screenshot_2023-09-03_at_19.06.37.png)

![image](./assets/img/Screenshot_2023-09-03_at_19.08.06.png)

Another option is to update GitHub Actions config with `release-as: x.x.x`. See [more](https://github.com/dhythm/release-please-example/pull/24/files).

![image](./assets/img/Screenshot_2023-09-03_at_19.54.11.png)


#### Pre-release feature

Set `prelease` as `true`. (Not sure about `bump-minor-pre-major` and `bump-patch-for-minor-pre-major` affect.)
Then, `pre-release` could be created by using `release-as`. (See: #44)

![image](./assets/img/Screenshot_2023-09-17_at_21.03.57.png)

However, the version is changed incorrectly after `pre-release`. (See: #46)

![image](./assets/img/Screenshot_2023-09-17_at_21.04.39.png)

Thus, prerelease can be archieved by `release-as` but need to handle by manual.
Also, `release-please` allows non-semver release as a pre-release by using `release-as`.

![image](./assets/img/Screenshot_2023-09-18_at_9.46.35.png)

![image](./assets/img/Screenshot_2023-09-18_at_9.47.34.png)

#### Create tag not only main branch

TBC

## Reference

- https://www.memory-lovers.blog/entry/2022/11/25/165938
