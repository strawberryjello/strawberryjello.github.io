---
layout: post
title: "Installing Doom Emacs on openSUSE Leap 15.1"
author: "Cristina Elep"
tags: [emacs, doom, opensuse]
---

I came across [Doom Emacs][doom-emacs] again recently and decided to give it a shot; I've been on [Spacemacs][spacemacs] for around 5 years, and though my experience with it has been mostly positive, the frequency of crashes and slow loading times have gotten me thinking about trying something else. One of the selling points of Doom Emacs is its performance -- it's supposed to be "close to the metal" of vanilla Emacs, which seems to be the exact opposite of a default Spacemacs install -- so I checked it out.

The current [prerequisites][doom-prereqs] for Doom Emacs are:

* git 2.23+
* Emacs 26.3+
* [ripgrep][ripgrep] 11+ (requires Rust to build from source)
* GNU find

I'm currently on openSUSE Leap 15.1, so I already had GNU find. My Git was an older version; luckily updating my packages via the YaST CLI upgraded it to 2.26.1.

## Emacs 26.3

I was on Emacs 25 since that's the latest in the package manager for openSUSE Leap 15.1; I had to get 26.3 from [another source][opensuse-editors] via zypper:

```
zypper addrepo https://download.opensuse.org/repositories/editors/openSUSE_Leap_15.1/editors.repo
zypper refresh
zypper install emacs
```

Since I already had Emacs, `zypper install emacs` gave me a message to that effect, as well as a command to install the updated version:

```
zypper install emacs-26.3-lp151.327.7.x86_64
```

Afterwards I was prompted to install matching upgrades for emacs-info and emacs-x11. Once I was done with those, Emacs was up and running again; I still had my existing Spacemacs config at the time, and I didn't notice any breakage.

## ripgrep

### Rust

The ripgrep version available via YaST was 0.8.1, so I wound up building the latest version from source; this requires Rust 1.34.0 and up. I got the current latest version, 1.43.1, by running the ff. command from the [Rust getting started guide][rust-getting-started]:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Here's a breakdown of the command:

* curl downloads the installer script at `https://sh.rustup.rs` using HTTPS and [TLS version 1.2][wiki-tlsv1.2]
  * curl will show an error message when it fails, but is otherwise silent (`-S`, `--show-error` used with `-s`, `--silent`)
  * curl will fail silently/without output on server errors (`-f`, `--fail`)
* The installer script is piped into sh, which runs it without saving a local copy first

I let the installer script use the defaults except for setting the PATH variable, which it modifies using `~/.profile`; my PATH is modified in `~/.bashrc`, so I added `$HOME/.cargo/bin` to PATH myself.

After this I ran `source $HOME/.cargo/env` to configure the current shell, then ran `rustc --version` and `cargo --version` to check if Rust was installed correctly.

### Building from source

I followed the [installation instructions][ripgrep-build] for building ripgrep; I also ran the tests because why not (they all passed):

```
git clone https://github.com/BurntSushi/ripgrep
cd ripgrep
cargo build --release
cargo test --all
./target/release/rg --version
```

This installed version 12.1.0.

## Doom Emacs

With the prerequisites out of the way, I could finally install Doom Emacs. I backed up my Spacemacs config by creating a zip archive and renaming my .emacs.d, then followed the [installation instructions][doom-install] in Doom's Getting Started guide:

```
git clone https://github.com/hlissner/doom-emacs ~/.emacs.d
~/.emacs.d/bin/doom install
```

When prompted, I chose to install all-the-icon's fonts to avoid any possible errors; apart from that I just waited for the installation to finish, then ran Emacs and checked it out.

## Thoughts so far

The defaults for Doom Emacs have taken some getting used to; for instance, [Helm][helm] isn't enabled by default, so I don't have access to niceties such as `helm-show-kill-ring` (which shows you the contents of the kill ring in an easy-to-browse format, see [here][helm-show-kill-ring] for a demo). Apart from that I haven't encountered any issues, probably because I was using default Spacemacs with only a handful of active layers; I haven't had to migrate any special configurations or elisp code. I might write more on this when I try out different development environments, such as the ones for Ruby and JavaScript.


[doom-emacs]: https://github.com/hlissner/doom-emacs
[doom-prereqs]: https://github.com/hlissner/doom-emacs#prerequisites
[doom-install]: https://github.com/hlissner/doom-emacs/blob/develop/docs/getting_started.org#doom-emacs
[helm]: https://github.com/emacs-helm/helm
[helm-show-kill-ring]: http://tuhdo.github.io/helm-intro.html#orgheadline6
[opensuse-editors]: https://software.opensuse.org/download.html?project=editors&package=emacs
[ripgrep]: https://github.com/BurntSushi/ripgrep
[ripgrep-build]: https://github.com/BurntSushi/ripgrep#building
[rust-getting-started]: https://www.rust-lang.org/learn/get-started
[spacemacs]: https://github.com/syl20bnr/spacemacs
[wiki-tlsv1.2]: https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.2
