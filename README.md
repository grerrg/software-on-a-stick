# software-on-a-stick

run software in OCI images as if they were natively installed.
or run your dockerfiles from anywhere.

docker comes short of everything not happening inside the container.
we need wrappers to work around that.
this is one example.

## about

this is a wrapper for oci images. run a single software in a container as if it were natively installed on your system, like `$ nix-env -ia nixos.hello-world`.

although after switching to `nixos` (and `devenv`), i've never really had any use for this concept anymore, i often find myself on non-nixos systems needing nix.

## the idea of "software-on-a-stick"

TODO WIP TBD

## an example

https://github.com/phiresky/ripgrep-all/pull/90/files
https://github.com/phiresky/ripgrep-all/pull/90/files#diff-b335630551682c19a781afebcf4d07bf978fb1f8ac04c6bf87428ed5106870f5

## remarks

heavily inspired by 
https://github.com/jessfraz/dockerfiles
which she featured in this video
https://www.youtube.com/watch?v=cYsVvV1aVss
