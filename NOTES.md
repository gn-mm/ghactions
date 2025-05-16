# GitHub Actions

Every workflow is triggered by some type of event, it can be:

* Pull request
* Push (branch)
* Issue
    - Created
    - Closed

Each workflow should have at least one job.

```txt
workflow
├── Job 1 --> Runner 1: a machine, VM, container, any device connected to GitHub.
│   ├── Step 1: Action ---------> Run Step -> Log Result
│   ├── Step 2: Shell Command --> Run Step -> Log Result
│   └── Step 3: Action ---------> Run Step -> Log Result
└── Job 2
    └── Step 1: Shell Command --------------> Run Step -> Log Result
```

Steps can not run in parallel, they must be runned in sequence from top to bottom. However, **jobs can run in parallel (default behavior)**.

Runners come in two flavors:

* GitHub-hosted runners: `ubuntu`, `Windows`, or `macOS`.
* Self-hosted runners: configured, managed, and installed by you. The OS can be whatever.

## GitHub CLI tool

```bash
gh repo create user/reponame  # create and clone repo
cd reponame
mkdir -p .github/worflows  # where we write GitHub Workflows
cd .github/workflows
touch hello_world.yml
```

```yml
name: Hello world workflow

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      # not reinveing the wheel, use a community action to configure it automatically
      # @v2 is a reference to a specific tag, branch or commit
      - uses: actions/checkout@v2   # https://github.com/actions/checkout
      - name: hello world
        run: echo "Hello world"
        shell: bash

    goodbye:
      runs-on: ubuntu-latest
      steps:
        - name: goodbye world
          run: echo "Goodbye world"
          shell: bash
```

<++>
