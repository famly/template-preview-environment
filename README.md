# Template: Preview Environments

> I’d really like to take this feature/change for a spin, but it’s so much work spinning up an environment just for that! 😩 - Sincerely, Everyone.
>
Haven’t we all been there before? Well, no more! By sprinkling a little pixie dust onto your CI, we can make it possible to spin up an entire preview environment on-the-go, to test out all your changes 🙂

The quick version?

- Comment `/preview` on a Pull Request to start an ephemeral Preview Environment
- This will stay up for 30 minutes by default, but you can change that in the workflow file

We use the [expose-tunnel](https://github.com/marketplace/actions/expose-tunnel) action to easily set up a tunnel into the CI job. It creates a tunnel using [bore.pub](https://github.com/ekzhang/bore), which supports setting up your own self-hosted server.

Check out the examples here:
- Example Pull Request that starts a Preview Environment https://github.com/famly/template-preview-environment/pull/1
- Example CI job output [here](https://github.com/famly/template-preview-environment/actions/runs/3456364929/jobs/5769048829)

## Workflow Overview

The following diagram is an overview of the flow the CI job:

```
            Comment posted on Pull Request
                          ↓
            +----------------------------+
            |   Detect Trigger Comment   |
            |   React with 👀 if it is   |
            +----------------------------+
                          ↓
            +----------------------------+
            |      Checkout PR Code      |
            +----------------------------+
                          ↓
            +----------------------------+
            | Setup Project Dependencies |
            +----------------------------+
                          ↓
            +----------------------------+
            |  Start Development Server  |
            |       in background        |
            +----------------------------+
                          ↓
            +----------------------------+
            |  Setup Tunnel into CI Job  |
            +----------------------------+
                          ↓
            +----------------------------+
            | Post Tunnel URL as Comment |
            |    on the Pull Request     |
            +----------------------------+
                          ↓
            +----------------------------+
            | Keep CI/Server alive for   |
            |        30 minutes          |
            +----------------------------+
```
