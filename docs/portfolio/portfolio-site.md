# :material-creation-outline: Portfolio Site

The whole portfolio, the landing page and its discipline hubs (this one included), is the project: designed and built with AI, and a portfolio piece in its own right. I designed and walked Claude through every change, every fix and every iteration. A few prototypes into the project we landed at this current version.

I used Claude Cowork (instead of Claude Code) as I feel it's more suitable for creative projects, you can brainstorm for a while together, and Claude Cowork tends to explain coding changes to me as it goes, which is a nice bonus as it helps me improve my understanding of programming.

---

<div class="sj-cta" markdown>
[:material-github: Source code](https://github.com/skyejen/skyejen.github.io){ .md-button .md-button--primary }
</div>

## :material-layers-outline: Tech stack

- **MkDocs + Material for MkDocs** - static site generator and base theme.
- **A shared theme layer** - my own theme pulled in as a git submodule, so every one of my sites (this one, cybersecurity, Python etc) shares a single design system instead of copy-pasted styling.
- **Hand-written CSS and vanilla JS** - the landing page is bespoke: the looping featured carousel, the multi-tag filtering, the rotating terminal, and the layout are all custom, layered over Material through overrides.
- **GitHub Pages + GitHub Actions** - hosting, and auto-deploy on every push.

## :material-tools: What I actually built

- A reusable design system shared across repositories, so branding stays consistent as the portfolio grows.
- A custom landing page - hero terminal, a filterable featured carousel that loops cleanly, discipline hubs, and a connect section - none of it out-of-the-box Material.
- A clean override discipline: local styles only, never touching the shared theme, so updates don't break the sites that depend on it.

## :material-sitemap-outline: How the ecosystem is wired

This isn't one site, it's five: a landing page, plus a separate repo for each discipline: cybersecurity, Python, DevOps, and a generalist bucket for everything else. They all share a single design system through a git submodule, so the theme lives in one place and every site points at it instead of carrying its own copy.

The catch with submodules is that a theme change doesn't reach the sites automatically, each one has to be told to move to the new version. So I wrote a small script that does the whole dance in one command: it commits and pushes the theme, then walks each site, pulls the update, and pushes the new pointer. One command, five sites back in sync.

It's a small piece of automation, but it's the kind that stops a multi-repo setup from becoming a chore, and building it taught me how submodules actually work under the hood, which was more than I expected to get from a docs site.

## :material-school-outline: What I got out of it

Working with a theme system, submodules, and someone else's conventions taught me more about front-end architecture than a blank file ever would. I learned to spot when a layout bug was really a CSS-inheritance problem, to read rendered output critically instead of trusting the code, and to hold a design opinion and push until the implementation matched it - including throwing away semi-ready code. A bit of a confidence boost - there were a few moments when Claude couldn't fix some bugs, so I would rescue him by investigating myself in Dev Tools. Such a small thing, but seeing AI craft so many amazing things so fast one can lose the sight of their own worth... until AI needs them to do something they can't.

## :material-robot-happy-outline: A note on AI

This whole site is my honest answer to "what can you build while pairing with AI?". So far that's five sites sharing one design system, a stack of write-ups, and the tooling to keep them in sync, solo and AI-paired, in a matter of weeks.

I direct AI where it accelerates me, and I know its limits well enough to catch what's wrong. I generated code with it, debugged layout with it, and moved fast, but the visual design, the calls about what belongs on the page, the "no, that's not right, do it this way," and the final judgement on every detail were mine.

It's an interesting time we live in. Something like this used to trigger my imposter syndrome heavily; nowadays this kind of work is considered a valuable skill: knowing what good looks like, and being able to direct a fast tool until you get there.

