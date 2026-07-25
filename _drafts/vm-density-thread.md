# X Thread: Multiplying VM Density

Thread for the post [Multiplying VM Density by 3.5×*](https://toxicpine.github.io/posts/MultiplyingVMDensity/).

Posting notes:

- Images: marginal post-load memory chart on 1/, memory table screenshot on 6/.
- Link appears only in 6/ (a link in tweet 1 suppresses reach). No hashtags.
- Character counts verified against X's 280 limit (URL counted as X's flat 23).
- Tweet 1 is at exactly 280 — any edit must be net-zero or negative.

---

## 1/ (280 chars) — attach: marginal memory chart

Apparently, we can run 3.5×* as many VMs at once on the same server, and we're just not doing it. It's dumb, honestly: most of a VM's RAM is the same data loaded once per machine, which nobody tries to deduplicate.

So I did, and cut disk usage ~10× while I was at it. Here's how:

## 2/ (276 chars)

This started with giving my friends VMs to house their coding agents. Ten VMs meant ten copies of Python, git, everything: on disk, then again in RAM.

The disk fix is simple, ~90% saved: shared software in one place, plus a private layer per VM.

RAM is the interesting part.

## 3/ (277 chars)

Every VM reads the same files, and Linux caches reads in RAM, so the VMs should share that cache. They can't: each runs its own kernel with a private cache.

So I built the VMs to read shared software from the host's ONE page cache: in RAM once, no matter how many VMs read it.

## 4/ (236 chars)

Replit does something similar internally (their "Super Colliding Nix Stores" post is worth reading). Mine needs no custom infrastructure: a full multi-user Linux machine per person, package manager and all, and it can run on Amazon EKS.

## 5/ (274 chars)

The existing fixes are active deduplication (Linux's KSM, for example): scan RAM, find identical pages, merge them after the fact. That generalizes fine to multi-user VMs, but it burns CPU.

Mine is passive: the copies never appear in RAM, so there's nothing to deduplicate.

## 6/ (273 chars) — attach: memory table screenshot

The numbers, measured after each VM served real traffic:

Normal VM: 270 MiB of RAM each
With the active dedup scanner: 103 MiB (plus ~2 min of scanner CPU)
Shared by design: 77 MiB

Same server, 3.5×* the machines. Full write-up, caveats, and code:
https://toxicpine.github.io/posts/MultiplyingVMDensity/
