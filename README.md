# XWiki Contrib `.github`

The GitHub configuration the [xwiki-contrib](https://github.com/xwiki-contrib) repositories share, held in one place so that a change is made once instead of being copied into every repository and drifting there.

GitHub gives a repository named `.github` special powers, and everything here is public because they require it.

## Default community health files

Files under `.github/` that GitHub recognises as [community health files](https://docs.github.com/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file) apply to **every public repository of the `xwiki-contrib` organization that does not define its own**. A repository that needs something different simply keeps its own copy, which always wins.

| File | What it does |
| --- | --- |
| [`.github/CONTRIBUTING.md`](.github/CONTRIBUTING.md) | How to contribute, pointing at contrib.xwiki.org. GitHub links it when someone opens a pull request. |
| [`.github/SECURITY.md`](.github/SECURITY.md) | Where to report a vulnerability, pointing at the XWiki security policy, which covers contrib projects too. |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | The description a new pull request is pre-filled with, the same as in [xwiki/.github](https://github.com/xwiki/.github). |

Nothing has to be done in a repository to pick these up: deleting its own copy is what makes the default apply.

## Organization profile

[`profile/README.md`](profile/README.md) is displayed on the [organization page](https://github.com/xwiki-contrib).

## Renovate preset

[`renovate/default.json5`](renovate/default.json5) is a [Renovate config preset](https://docs.renovatebot.com/config-presets/) holding the settings every contrib repository wants. It extends the [preset of the `xwiki` organization](https://github.com/xwiki/.github/blob/master/renovate/default.json5) and adds what is specific to contrib: the XWiki Nexus repository and the exclusion of the contrib parent POM. A repository's `.github/renovate.json5` only needs:

```json5
{
  "extends": ["github>xwiki-contrib/.github//renovate/default.json5"]
}
```

plus whatever is specific to it. Mind how Renovate merges the two: `packageRules` are concatenated, the preset's coming first, but every other array is replaced wholesale by the repository's value. A repository that needs an extra `ignoreDeps` entry has to repeat the presets' entries alongside its own.

Unlike the `xwiki` organization, the preset assigns the Renovate pull requests to nobody: each contrib project has its own maintainers.
