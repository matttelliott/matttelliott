# Add gists to README.md

- Check out [this GitHub Action](https://github.com/gautamkrishnar/blog-post-workflow)

- Check out [this youtube video](https://www.youtube.com/watch?v=ECuqb5Tv9qI)

- gists.github.com exposes a lists of Gists by adding `.atom` to the username
  https://gists.github.com/matttelliott.atom

- update the yaml to point to the feed

```yaml
name: Latest Gists workflow
on:
  push:
    branches: [master]
  schedule: # Run workflow automatically
    - cron: '0 0 * * *' # Runs every day at midnight
  workflow_dispatch: # Run workflow manually (without waiting for the cron to be called), through the Github Actions Workflow page directly

jobs:
  update-readme-with-gists:
    name: Update this repo's README.md with latest Gists
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Add Latest Gists to README.md
        uses: gautamkrishnar/blog-post-workflow@master
        with:
          comment_tag_name: 'GIST-LIST'
          commit_message: 'Updated README.md with the latest Gists'
          feed_list: 'https://gist.github.com/matttelliott.atom'
```

- add the comment tag to README.md

```markdown
# Latest Gists

<!-- GIST-LIST:START -->
<!-- GIST-LIST:END -->
```

- commit and push
