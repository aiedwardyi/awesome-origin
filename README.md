# Awesome Origin

A curated list of resources for [Cursor Origin](https://cursor.com/docs/origin), the git forge Cursor built for AI coding agents.

Origin was announced June 16-17, 2026, and opened in early beta on August 17, 2026 to all paid plans, three days after SpaceX closed its acquisition of Cursor. It was built by the team behind Graphite, which announced an agreement to be acquired by Cursor in December 2025, and ships with a REST API (Alpha maturity), Origin Apps, webhooks, and a first-party CLI. Repos are either Origin-native or mirrored in from GitHub. Mirrored-in repos are excluded from app installations, installation tokens, and app webhooks, and app requests naming them return 403.

The third-party ecosystem is still forming. As of August 19, 2026, a small number of community example apps exist and no standalone community SDK was found. Sections below note where a category is thin, and the last section maps what is still unbuilt.

## Contents

- [Hands-On Guides](#hands-on-guides)
- [Official Docs](#official-docs)
- [CLI & Tools](#cli--tools)
- [Community Guides & Tutorials](#community-guides--tutorials)
- [Launch Coverage](#launch-coverage)
- [Community Discussion](#community-discussion)
- [Example Repos & Apps](#example-repos--apps)
- [Ecosystem Status & Opportunities](#ecosystem-status--opportunities)

## Hands-On Guides

- [Stacked pull requests in Cursor Origin](guides/stacked-prs.md) - Using the `--stack-on` flag on `origin pr create`, which works but is not in the official CLI reference or the CLI's own `--help`. Covers restacking and conflict recovery.
- [Setting up Origin on Windows](guides/windows-setup.md) - Getting the CLI working through WSL, covering the four walls a real setup hits: no native Windows build, metadata on `/mnt/c`, missing git identity, and the CLI installing off PATH.

## Official Docs

- [Origin Docs Index](https://cursor.com/docs/origin) - Entry point for all Origin documentation.
- [Create a Repository](https://cursor.com/docs/origin/create-repository) - Creating repos on Origin.
- [Git Access](https://cursor.com/docs/origin/git) - Cloning, pushing, and authenticating over Git.
- [Mirror from GitHub](https://cursor.com/docs/origin/mirror-github) - Setting up GitHub mirroring and what it does and does not sync.
- [Pull Requests](https://cursor.com/docs/origin/pull-requests) - PR workflow, review, and merge.
- [Browse & Search](https://cursor.com/docs/origin/browse) - Browsing files, switching branches, searching code, and inspecting commit history in the web UI.
- [Settings](https://cursor.com/docs/origin/settings) - Repository settings, including branch rules and detaching from GitHub.
- [Codebase Settings](https://cursor.com/docs/origin/codebase-settings) - Team-level configuration: member permissions and installing or managing apps, distinct from per-repo settings.
- [Integrations](https://cursor.com/docs/origin/integrations) - Built-in integrations available on Origin repos.
- [Origin CLI Reference](https://cursor.com/docs/origin/cli) - The `origin` binary: repos, PRs, review threads, rulesets, SSH keys, and raw `origin api` calls.
- [CLI Command Reference](https://cursor.com/docs/origin/cli/reference/commands) - Full command listing for the `origin` CLI.
- [CLI Pull Request Commands](https://cursor.com/docs/origin/cli/reference/pull-requests) - The `origin pr` subcommands, including `thread list|resolve|reopen|reply` for review threads.
- [Origin API Reference](https://cursor.com/docs/api/origin) - Interactive REST API reference, currently Alpha maturity.
- [Origin API Changelog](https://cursor.com/docs/api/origin/changelog) - Every API change, including breaking ones. Worth watching closely: 19 entries dated between August 5 and 16, 2026, five of them breaking.
- [Origin API OpenAPI Spec](https://cursor.com/docs/api/origin/openapi.yaml) - Machine-readable OpenAPI 3.1 spec (`v1alpha1`) with full request and response schemas. Suitable for client codegen.
- [Origin API Full Reference (Markdown)](https://cursor.com/docs/api/origin/llms-full.txt) - The complete Origin API reference as a single Markdown file, intended for agents.
- [Origin API llms.txt](https://cursor.com/docs/api/origin/llms.txt) - Machine-readable index scoped to the Origin API, linking the full reference and the OpenAPI spec.
- [llms.txt](https://cursor.com/llms.txt) - Machine-readable doc index for the whole Cursor site. Lists the Origin doc pages but not the API reference, which is indexed separately above.
- [Origin Product Changelog](https://cursor.com/changelog/origin-code-hosting) - Product-level announcements and feature updates.
- [Cursor Status](https://status.cursor.com) - Live service status. Origin is a separately monitored component.
- [Data Use & Privacy](https://cursor.com/data-use) - Cursor's published policy on what happens to your code and data.
- [Agent Swarm Model Economics](https://cursor.com/blog/agent-swarm-model-economics) - Cursor's own post on swarm-scale metrics: commit rates, conflict counts, contested files.
- [Joining SpaceX](https://cursor.com/blog/joining-spacex) - Cursor's announcement of the SpaceX acquisition closing.

## CLI & Tools

- [Origin CLI](https://cursor.com/docs/origin/cli) - Official CLI. Covers repos, PRs, review threads (`origin pr thread list|resolve|reopen|reply`), rulesets, SSH keys, and raw API calls.
- [Origin REST API](https://cursor.com/docs/api/origin) - REST API for building Origin Apps. Alpha maturity (`v1alpha1`), with an [OpenAPI 3.1 spec](https://cursor.com/docs/api/origin/openapi.yaml) published for codegen.
- [@cursor/sdk](https://www.npmjs.com/package/@cursor/sdk) - Official TypeScript SDK, currently in public beta. Covers Cursor agents, not the Origin API.

Windows is supported through WSL, with no native Windows build, per the [CLI docs](https://cursor.com/docs/origin/cli). See [Setting up Origin on Windows](guides/windows-setup.md). Run `origin auth login` to configure the HTTPS Git credential helper.

No standalone community Origin API SDK was found in GitHub searches on August 19, 2026. See [Ecosystem Status & Opportunities](#ecosystem-status--opportunities).

## Community Guides & Tutorials

- [Learn Cursor: Origin Guide](https://www.learncursor.dev/guides/cursor-origin) - Independent guide aimed at engineering leaders and platform teams, updated July 16, 2026. Distinguishes confirmed facts from inference.
- [explainx.ai: Cursor Origin - GitHub Alternative for AI Agents](https://www.explainx.ai/blog/cursor-origin-git-hosting-github-alternative-ai-agents-2026) - Overview of the agent-first hosting pitch.
- [dev.to: Cursor Origin - What We Actually Know](https://dev.to/olucasleitedev/cursor-origin-what-we-actually-know-about-cursors-new-git-hosting-1g9c) - Community rundown separating confirmed facts from speculation.
- [kingy.ai: Cursor Origin vs GitHub](https://kingy.ai/blog/cursor-origin-vs-github/) - Feature-by-feature comparison against GitHub.

No independent Korean guide, tutorial, or video was found as of August 19, 2026. Official Korean coverage exists at [cursor.com/ko](https://cursor.com/ko/changelog/origin-code-hosting).

## Launch Coverage

- [VentureBeat: Cursor launches Origin code hosting platform as GitHub outage exposes opening](https://venturebeat.com/infrastructure/cursor-launches-origin-code-hosting-platform-as-github-outage-exposes-opening-in-ai-coding-race)
- [SiliconANGLE: Cursor launches Origin code hosting service to compete with GitHub](https://siliconangle.com/2026/08/17/cursor-launches-origin-code-hosting-service-to-compete-with-github/) - Published August 17, 2026.
- [TestingCatalog: Cursor prepares to launch Origin platform for code reviews](https://www.testingcatalog.com/cursor-prepares-to-launch-origin-platform-for-code-reviews/) - Pre-launch coverage of the platform.
- [webdeveloper.com: Cursor Origin git forge for parallel agents](https://webdeveloper.com/news/cursor-origin-git-forge-parallel-agents/)
- [Forbes: SpaceX buys Cursor in largest startup acquisition ever at $60 billion](https://www.forbes.com/sites/sandycarter/2026/06/16/spacex-buys-cursor-in-largest-startup-acquisition-ever-at-60-billion/) - Published June 16, 2026.
- [TechCrunch: SpaceX to acquire Cursor for $60B in stock](https://techcrunch.com/2026/06/16/spacex-to-acquire-cursor-for-60b-in-stock-days-after-blockbuster-ipo/) - Published June 16, 2026.
- [01net.it: Cursor Origin, code hosting per agenti AI](https://www.01net.it/cursor-origin-code-hosting-agenti-ai/) (Italian)
- [habr.com: Cursor coverage](https://habr.com/ru/articles/959144/) (Russian, peripheral mention)
- [wowtale.net: SpaceX acquisition close](https://wowtale.net/2026/08/15/263045/) (Korean) - Published August 15, 2026. News coverage of the acquisition close that describes Origin briefly; predates the beta.

## Community Discussion

- [Hacker News: "Cursor launches Origin, GitHub alternative"](https://news.ycombinator.com/item?id=49334209) - The main launch-day discussion thread.
- [Hacker News: "Cursor Origin"](https://news.ycombinator.com/item?id=49339359) - Follow-up discussion thread.
- [Hacker News: GitHub degradation thread](https://news.ycombinator.com/item?id=49336919) - Discussion of the GitHub outage Origin launched alongside, and Origin's own same-day degradation.
- [X / TestingCatalog: Origin leak thread](https://x.com/testingcatalog/status/2087177021105267167)

These discussions are anecdotal and not representative of Origin users.

## Example Repos & Apps

Community examples are just starting to appear. These were verified on August 19, 2026:

- [origin-neon](https://github.com/neon-solutions/origin-neon) - An Origin app that gives each pull request its own Neon database branch, with stacked PRs parenting onto their parent PR's branch. Built on Origin webhooks and the REST API.
- [origin-neon-branches](https://github.com/andrelandgraf/origin-neon-branches) - A public copy of the `origin-neon` demo, showing an Origin PR creating a Neon branch.
- [cursor-origin-migration](https://github.com/christian-varritech/cursor-origin-migration) - A guide and starter kit for migrating from GitHub to Origin.

The three documented built-in integrations:

- **Vercel** - Deploys and PR preview environments. Works on GitHub-mirrored repos.
- **Depot** - CI for Origin repos, runs existing GitHub Actions workflows. Origin-native repos only, not mirrors.
- **Buildkite** - CI for Origin repos. Runs existing GitHub Actions workflows and native Buildkite pipelines. Origin-native repos only, not mirrors.

Official docs do not describe a public app directory or submission process. Note that the [Cursor Marketplace](https://cursor.com/marketplace) is a separate thing: it distributes plugins for the Cursor agent, not Origin apps.

## Ecosystem Status & Opportunities

As of August 19, 2026, community examples on the Origin API are minimal and no standalone community SDK was found. For anyone looking to build, that makes the following open ground:

- **No typed client or SDK.** An official OpenAPI 3.1 spec is published, so a generated, typed client is straightforward to produce. No standalone community Origin API SDK was found in GitHub searches on August 19, 2026.
- **API discovery is uneven.** The site-wide `llms.txt` lists Origin's doc pages but omits the API reference, so an agent starting there will not find it. The API's own index, full Markdown reference, and OpenAPI spec are all published, just not surfaced from the top-level index.
- **Review threads are CLI-only.** The CLI supports full thread resolve/reopen/reply, but REST has no first-class thread resource or resolution API.
- **Mirrored-in repos are excluded from the app layer.** Most repos on day one arrive by mirroring from GitHub, the advertised on-ramp. Mirrored-in repos are excluded from app installations, installation tokens, and app webhooks, and app requests naming them return 403.
- **No native Windows CLI build.** Windows developers need WSL to authenticate and push. Run `origin auth login` to configure the HTTPS Git credential helper.
- **No independent Korean content.** No independent Korean guide, tutorial, or video was found as of August 19, 2026, in a market with a large and fast-moving developer community. Official Korean coverage exists.

This section will be updated as the ecosystem fills in. If you build or find something that belongs here, see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, this list is released under [CC0](LICENSE). See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add to it.
