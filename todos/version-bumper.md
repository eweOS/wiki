# Version Bumper

- Auto check updates
- Build locally to check if autoupgrade is possible
- Open PRs on GitHub

# Some Different Thoughts

- Auto check updates
- Auto check if signatures or checksums exist on project info
- Build on a separated OBS project, and upload to a repo called "alpha" or "testing"
- Notice maintainers by sending mails, identifying `# Maintainer`.
- Provide a set of templates for common project hosting (eg. Github Gitlab GNU nongnu)
- The behaviour can be configured inside a file.
    - Whether try to build before noticing maintainers
    - Whether building in another project first or directly throw into repo