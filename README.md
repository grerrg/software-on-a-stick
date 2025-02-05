# software-on-a-stick
run software in OCI images as if they were natively installed.
or just my dockerfiles. heavily inspired by 
https://github.com/jessfraz/dockerfiles
which she featured in this video
https://www.youtube.com/watch?v=cYsVvV1aVss

## about

this is a wrapper for oci images. run a single software in a container as if it were natively installed on your system, like `$ nix-env -ia nixos.hello-world`.

although after switching to `nixos` (and `devenv`), i've never really had any use for this concept anymore, i often find myself on non-nixos systems needing nix.
