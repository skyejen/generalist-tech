# :material-mailbox-outline: Claude Mailbox

A postal service for my Claude projects. One project can tap another on the shoulder, hand it a job and get the answer back, without me copying and pasting in between.

---

## :material-lightbulb-on-outline: Why I built it { data-toc-label="Why I built it" }

I run my life and my learning across several Claude projects: one for my to-dos, one each for my AI and cybersecurity studies, one for my workouts, nutrition and general wellbeing, and so on. Each project has its own threads, and threads inside one project can already message each other. Projects can't.

So I'd ended up as the postie. My to-do project would need to cooperate with another project on joint work, and I'd be copying and pasting between the two. I'm not huge on manual, avoidable work, so I decided to see if I could take myself out of the equation.

## :material-magnify: What didn't work { data-toc-label="What didn't work" }

First we checked whether there was a native way. One project tried messaging another project's thread directly and got "not found". From inside a project thread, I could see my older Claude Code sessions but none of the project threads, so projects simply can't see each other. That makes total sense, as they're sandboxes, but I like trying things before I set out to build something from scratch.

Options on the table:

- **Linear tickets** as the mailbox. Out, because I'm on the free plan and a ticket per message would eat my issue limit (I do really love Linear otherwise).
- **A Cloudflare Worker** acting as a message board, with a custom connector. Sexy, and it might let ChatGPT join in too, but it's a lot of building before I even know if the idea works and is actually useful to me, rather than something I build purely on excitement. I'll admit I'm very much a "yes, it's maybe a one-time thing, but I really want it" person, but I try not to sign up for a multi-hour build and another subscription every time that mood strikes (emphasis on the *try*). (I do really want to bring ChatGPT in at some point, though, as there are a few things I use ChatGPT for specifically rather than Claude.)
- **A GitHub repo** as the mailbox. Free, private, already connected to every project, and I get the history for nothing. I'd heard of people doing this before, too.

The catch with all of them: Claude doesn't sit there listening. A thread only wakes up when something pokes it, so a mailbox nobody checks is just a drawer.

## :material-bell-ring-outline: The trick: a pull request as a doorbell { data-toc-label="The doorbell trick" }

A cloud Claude thread can subscribe to a pull request, and GitHub activity on it wakes the thread up. So:

- Every project gets an **inbox**: a draft pull request in a shared private repo that's never merged.
- Each project's admin thread (its post office) subscribes to its own inbox.
- To send a message, a project comments on the other project's inbox, and the post office wakes up and routes it.
- One pull request only wakes one thread, so only the recipient wakes up and everyone else sleeps through it.

Messages follow a simple `From: Project (Thread)` / `To: Project (Thread)` format, and replies go to the **sender's** inbox.

## :material-test-tube: Testing it (and the first fail) { data-toc-label="Testing it" }

Test 1: my to-do project left a comment on the new inbox. It landed on GitHub just fine. No wake.

There were two possible reasons. Every Claude posts to GitHub as me, so maybe GitHub skips "my own" comments, which would have killed the whole idea. Or maybe plain comments just don't count as wake-worthy.

Test 2 was designed to tell those apart: same sender, same account, but a **review comment** (a comment pinned to a line of the changed file) instead of a plain one. It arrived within seconds.

So posting as me was fine, and the rule is: **review comments wake, plain comments don't**. That one finding is now the big warning at the top of the README.

## :material-package-variant-closed: Bigger jobs { data-toc-label="Bigger jobs" }

Once it worked, I didn't want a single pull request turning into a filing cabinet. So the inbox is only the doorbell:

1. For anything substantial, the sender opens an **issue** with the goal, context and what "done" looks like, labelled `to:<project>`.
2. It rings the recipient's doorbell with a link.
3. The work and the progress updates happen on the issue.
4. When it's done, the recipient closes the issue and rings the sender's doorbell.

Wake and work are kept separate, so the inbox stays short and the history stays tidy.

## :material-shield-lock-outline: Keeping it safe { data-toc-label="Keeping it safe" }

- The repo is private and only my projects are connected to it.
- No passwords, keys or tokens in messages, ever.
- A message from another Claude is a **request, not my approval**. Anything that can't be undone still needs my go-ahead. That matters, because a mailbox one AI reads and another AI writes to is a lovely spot for prompt injection, which I've literally [just been practising](https://skyejen.github.io/cybersecurity/learning/off-the-beat/gohack-ai/flaming-umbrella/).
- Only one thread listens to an inbox at a time, and handing one over means unsubscribing first.

## :material-format-list-checks: What's next { data-toc-label="What's next" }

All my projects have their own inbox now, set up with a copy-paste prompt from the repo's templates folder. Next I want to see whether ChatGPT can join in, either through this setup or the Cloudflare Worker version that's still on the shelf.

## :material-robot-happy-outline: A note on AI { data-toc-label="A note on AI" }

Built while pairing with Claude, which is a bit meta given that it's a way for Claudes to talk to each other. Claude researched the options and wrote the README. I set the goal, ruled out Linear, spotted that a pull request wake might be the "always in sync" route, ran both tests, and came up with keeping bigger jobs in issues so the inbox didn't turn into a mess.
