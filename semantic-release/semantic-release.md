# What I've learned

## Configuration

### Github key
First we need a github key for this. Once we obtained it, we must set the
environment variable `GH_TOKEN` in the CI build environment.
(it should not be set in any config file, since it will be definitely leaked)

### Release rc
Since semantic-release was originally built for releasing npm (javascript),
we have to disable the javascript publishing part by specifying the plugin
that we want to use.

In this case we should use.
{
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator",
    "@semantic-release/github",
  ]
}

Otherwise, it will include @semantic-release/npm by default and it will looks for
package.json and try to publish on npm which we do not want.

### CircleCI
CircleCI yaml config is simple enough. It can be referenced in the config.yml.
It simply run every test jobs first and then release by the semantic-release.

## Changelog message

To make changelog nice you need to squash and merge the commit.
Or periodically commit message with the angular commit format.

**It is nice to have pull request number and issues in the title and body**
For an example

feat(api): add 'view_order' command (#16)   <---- Title
resolved #13                                <---- Body

The changelog will be something like this.

Features
 * api: add 'view_order' command (#16) (1238dw91) resolved #13

where #16 is the pull request link and #13 is the issue link


## Note
not related to semantic-release, but it seems that CircleCI badge doesn't work in
private repo. It looks like it needs github auth key somewhere in the CircleCI setting.
