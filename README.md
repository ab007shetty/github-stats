# [GitHub Stats Visualization](https://github.com/vaishnavid0604/github-stats)

<a href="https://github.com/vaishnavid0604/github-stats">

![](https://github.com/ab007shetty/github-stats/blob/main/generated/overview.svg)
![](https://github.com/ab007shetty/github-stats/blob/main/generated/languages.svg)

</a>

Generate visualizations of GitHub user and repository statistics using GitHub
Actions.

This project is currently a work-in-progress; there will always be more
interesting stats to display.

## Background

When someone views a profile on GitHub, it is often because they are curious
about a user's open source projects and contributions. Unfortunately, that
user's stars, forks, and pinned repositories do not necessarily reflect the
contributions they make to private repositories. The data likewise does not
present a complete picture of the user's total contributions beyond the current
year.

This project aims to collect a variety of profile and repository statistics
using the GitHub API. It then generates images that can be displayed in
repository READMEs, or in a user's [Profile
README](https://docs.github.com/en/github/setting-up-and-managing-your-github-profile/managing-your-profile-readme).

Since the project runs on GitHub Actions, no server is required to regularly
regenerate the images with updated statistics. Likewise, since the user runs
the analysis code themselves via GitHub Actions, they can use their GitHub
access token to collect statistics on private repositories that an external
service would be unable to access.

## Disclaimer

If the project is used with an access token that has sufficient permissions to
read private repositories, it may leak details about those repositories in
error messages. For example, the `aiohttp` library—used for asynchronous API
requests—may include the requested URL in exceptions, which can leak the name
of private repositories. If there is an exception caused by `aiohttp`, this
exception will be viewable in the Actions tab of the repository fork, and
anyone may be able to see the name of one or more private repositories.

Due to some issues with the GitHub statistics API, there are some situations
where it returns inaccurate results. Specifically, the repository view count
statistics and total lines of code modified are probably somewhat inaccurate.
Unexpectedly, these values will become more accurate over time as GitHub
caches statistics for your repositories. Additionally, repositories that were
last contributed to more than a year ago may not be included in the statistics
due to limitations in the results returned by the API.



# Installation

<!-- TODO: Add details and screenshots -->

1. Create a personal access token (not the default GitHub Actions token) using
   the instructions
   [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token).
   Personal access token must have permissions: `read:user` and `repo`. Copy
   the access token when it is generated – if you lose it, you will have to
   regenerate the token. Also goto Settings of the Stats Repo -> Action -> General -> Workflow permissions and choose read and write permissions.
   And makesure ' Allow GitHub Actions to create and approve pull requests ' is checked.
3. Click [here](https://github.com/ab007shetty/github-stats/generate) to create a
   fork of this repository
4. If this is the README of your fork, click [this
   link](../../settings/secrets/actions) to go to the "Secrets" page.
   Otherwise, go to the "Settings" tab of the newly-created repository and go
   to the "Secrets" page (bottom left).
5. Create a new secret with the name `ACCESS_TOKEN` and paste the copied
   personal access token as the value.
6. It is possible to change the type of statistics reported.
   - To ignore certain repos, add them (separated by commas) to a new
     secret—created as before—called `EXCLUDED`.
   - To ignore certain languages, add them (separated by commas) to a new
     secret called `EXCLUDED_LANGS`.
   - To show statistics only for "owned" repositories and not forks with
     contributions, add an environment variable (under the `env` header in the
     [main
     workflow](https://github.com/ab007shetty/github-stats/blob/master/.github/workflows/main.yml))
     called `EXCLUDE_FORKED_REPOS` with a value of `true`.
7. Go to the [Actions
   Page](../../actions?query=workflow%3A"Generate+Stats+Images") and press "Run
   Workflow" on the right side of the screen to generate images for the first
   time. The images will be periodically generated every hour, but they can be
   manually regenerated by manually running the workflow.
8. Check out the images that have been created in the [`generated`](generated)
   folder.
9. Link back to this repository so that others can generate their own
   statistics images.
10. Star this repo if you like it!


