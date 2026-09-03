---
hide:
- footer
---

# Welcome to valet.sh

!!! danger "macOS: valet.sh 2.x has reached the end of its technical life"
    valet.sh 2.x builds its whole macOS environment on the **x86_64 build of Homebrew** - natively on Intel Macs,
    and through Rosetta 2 on Apple Silicon. In September 2026 Homebrew moved macOS Intel `x86_64` to
    *[Tier 3](https://docs.brew.sh/Support-Tiers)* and **stopped building new bottles** (pre-compiled packages)
    for it.

    Central dependencies of valet.sh - among them `openssl@3`, `curl` and `pcre2` - already have no Intel package
    left. They now have to be compiled from source on every machine, which is slow and increasingly likely to
    fail. Packages that still resolve today only do so because an old bottle is left over; none of them will ever
    be rebuilt.

    This is outside our control and it cannot be solved within 2.x. Homebrew will
    **remove the ability to run on Intel `x86_64` altogether in or after September 2027**, and Apple will largely
    drop Rosetta 2 with macOS 28. **valet.sh 2.x therefore receives no further maintenance on macOS.**

    **What this means for you**

    - **Apple Silicon** - switch to *[valet.sh 3.x](https://valet.sh/3.x/)*. It runs natively on arm64, no longer
      needs Rosetta 2 and runs its data services in containers instead of Homebrew packages. See the
      *[Upgrade guide](https://valet.sh/3.x/getting-started/upgrade-from-2x/)*.
    - **Intel Mac** - there is no upgrade path, valet.sh 3.x supports Apple Silicon only. An existing 2.x
      installation keeps working as long as its installed packages do, but avoid `brew upgrade` and expect
      installations of additional services to fail.
    - **Ubuntu** - not affected. The Linux side of valet.sh 2.x does not use Homebrew.



## Why valet.sh?
valet.sh supports software developers to concentrate fully on their daily challenges without having to worry about how to install and properly configure the necessary services on various operating systems for many different projects and requirements. Unlike other tools which provides development environments, valet.sh provides all necessary services such as PHP, MySQL and Elasticsearch in all important versions in parallel without having to make sluggish and error-prone system-side changes.

## How valet.sh Works
valet.sh provides uniform, stable and high-performance development environments for macOS and Ubuntu that can be configured and controlled using an easy-to-use terminal user interface. Technologically, *[valet.sh](https://github.com/valet-sh/valet-sh)* is based on *[bash](https://www.gnu.org/software/bash/)* and *[Ansible](https://www.ansible.com/)*.

## Open Source
valet.sh is completely open source available on *[GitHub](https://github.com/valet-sh/valet-sh)*

## Interested?
Let's *[get started using valet.sh](getting-started/index.md)*