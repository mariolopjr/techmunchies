+++
title = "nix sha256 ref one liner"
description = "if you, like me, don't want your system to scream for you, then you may like the one simple trick to get a github sha256 ref for your nix package. probably."

[taxonomies]
tags = ["nix"]
+++

I was working on an update to the `asus-ec-sensors` package ([Github PR](https://github.com/NixOS/nixpkgs/pull/473022) if you're curious) and I was stumped, how do I get the SHA256 of a Github ref? I know I can just delete the SHA256 from the `default.nix` which will then print `sha256-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA` which I didn't like. I scream enough into the void, I don't want or _need_ my system to do it for me. That's not something I prefer to delegate.

So I did a search on the web (I know I know, all the cool kids get their info from ChatGPT, but I hate chatting...) and found a wonderful post from [figsoda on reddit](https://www.reddit.com/r/NixOS/comments/10ueaev/comment/j7bbs4l/) that had this beautiful one-liner: 

```sh
nix flake prefetch github:<owner>/<repo>/<rev>
```

Just look at that, soooo nice. All I had to do was replace the replaceables in the command and got the hash I needed:

```sh
❯ nix flake prefetch github:zeule/asus-ec-sensors/0e73cd165c4d1baf8ce841604722c6981b7ba9d6
Downloaded 'github:zeule/asus-ec-sensors/0e73cd165c4d1baf8ce841604722c6981b7ba9d6' to '/nix/store/hb2x2h9yrj70p74gipljvzd5siqc65y0-source' (hash 'sha256-qX+HmtBdm9bOJRnlpI/Ru0OCcUi8MQ29Y731yM9JEi0=').
```

I'm sure this can be improved to parse out the hash and save it to my clipboard. Maybe another post. It would save loads of time over the course of a lifetime, but [https://xkcd.com/1319](https://xkcd.com/1319) comes to mind.

