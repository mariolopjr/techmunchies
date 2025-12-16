+++
title = "nix things and vms"
description = "so i heard you want to try your nix setup in a vm hmmm?"

[taxonomies]
tags = ["nix"]
+++

TBD

talk about disko, etc.

```nix,linenos,hl_lines=6-8
disko.devices.disk.main = {
  device = "/dev/vda";
  imageSize = "40G";
  # insecure: the password for luks is "secret"
  # since this is a test VM, security is not important
  preCreateHook = ''
    echo -n 'secret' > /tmp/secret.key
  '';

  content.partitions.luks.content = {
    passwordFile = "/tmp/secret.key";

    content.subvolumes."/swap".swap.swapfile.size = "4G";
  };
};
```

