---
title: Healing After NixOS
description: Sometimes, the grass really is greener on the other side.
---
There's something very exciting about a blank NixOS configuration. There's so many directions you could go, and you know you're well on your way to creating the *perfect* setup. I generated my hardware configuration, figured out how to use [disko](https://github.com/nix-community/disko) to get my disk partitioning just right, and was well on my way to having a working gaming machine again.

I initially tried Gnome as my desktop, but that's boring. We're in the big leagues now, and need an experience to match. As such, I chose [Hyprland](https://hypr.land) and have been thoroughly pleased with it. It was surprisingly simple to configure, and it has given me little to no issues since setting it up. 

Honestly, even with an NVIDIA graphics card and using Wayland with a bunch of Electron apps, I didn't really have too many issues. At the end of the day, it's just Linux with (a lot of) extra steps, and it worked great! I was happily continuing my losing streak in Deadlock without any major problems.

# Rabbit holes

Once you set up one machine with Nix, it is inevitable that you will configure the rest with it as well. You have grandiose dreams of one single, well laid out config that can produce your perfect computing environment on any machine that's thrown at you. But, oh... Your personal laptop is a Macbook, so you're going to have to figure out [nix-darwin](https://github.com/nix-darwin/nix-darwin). But that's fine, right? You can just adapt things as necessary and lean on home-manager.

And, good news! Your work laptop is also a Mac, so getting that one set up should be easy! Oh, wait... you use those two Macs for totally different things and there's not too much overlap in what you want installed or how you want it configured.

Not to mention that pesky dev box that's running in the cloud... Still Linux, but limited to running Debian, so we'll have to just use a standalone HM config. So maybe we'll just factor out the "core" of what you want shared, and leave the rest to be configured per machine!

...

Yeah... That way lies madness. I did eventually get something working that took into account multiple Macs, NixOS machines, and standalone HM configs, but it was only after pouring countless hours into it. It wasn't serving me anymore, just another thing to maintain. The dream of the perfect flake to rule them all was shattered. 
# Pain.

Shared configuration between machines aside, the one thing that finally made me throw in the towel was having to run `nixos-rebuild switch --flake .#bitcrshr-gaming` every single time I changed *anything*. Even something as simple as modifying my PATH resulted in a ~30s build of my NixOS config.

It's not forever, I mean we're not building a JVM project or anything, but that's a *lot*. Especially when you're trying to experiment with new things and need to do a lot of tinkering. Turns out, good ol' fashioned dotfiles might be the way to go.
# Salvation

After over a decade of using Linux, my hopeless attempts at avoiding Arch finally failed. Last weekend, with a neckbeard in place and the spirit of Richard Stallman in my heart, I installed Arch.

It was a bit tricky at first, but within about 2-3 hours I had a fully functioning gaming rig once again. Everything I had working in NixOS was working great on Arch. If nothing else, Arch has the most extensive and helpful documentation I've ever seen. Every single little bump in the road led me straight to the Arch wiki, where my problem was immediately solved.

This has been incredibly refreshing. Something that has always bothered me about the Nix ecosystem as a whole is that learning it is *way* harder than it needs to be. It's simply too difficult to find the right information, and what you do find usually assumes far too much about your level of knowledge[^1] or is so outdated that it's no longer relevant.

Oh, and better yet, when I wanted to change a dotfile I simply had to change a dotfile! I don't know why I was ever against doing it this way. In retrospect, it's *so* much simpler to share simple text files between machines, especially with tools like [chezmoi](https://chezmoi.io). No build time, just configuring and *moving on*.

On the other hand, I am technically losing the ability to more or less spin up a perfect clone of my machine. Also, if I really mess something up, I can't just go back to an earlier build anymore[^2]. But, I'm not doing anything insane and it's really not that hard to just... reinstall. 
# Final Thoughts

I always wondered why people raved so much about Arch, and now I think I understand. Arch as a distro isn't much--you're doing most of the work yourself. But, the real power of it lies in its excellent documentation along with its great tooling and package repositories.

And with all that being said, I actually don't have any problems with Nix or NixOS. I still love using Nix for its devshells, and overall NixOS was a good experience--the benefits just didn't justify the cost for me. 

At the end of the day, all that really matters is: *I use Arch, btw.*

[^1]: *"What's a monad?" Oh, that's easy! It's simply a monoid in the category of endofunctors.* 

[^2]: Before Arch, I very briefly experimented with [Fedora Silverblue](https://silverblue.fedoraproject.org) and similar atomic Fedora distros. They were mostly fine, but I found them far too bloated with things I didn't want or need, and I'd rather start from a clean slate.
