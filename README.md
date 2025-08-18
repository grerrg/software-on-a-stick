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

let's take `rga` for an example.

 1. create directory to hold dockerfiles:
```sh
$ mkdir /usr/local/share/dockerfiles/rga
```
2. create dockerfile for `rga`:
```sh
$ $EDITOR /usr/local/share/dockerfiles/rga/Dockerfile
```
```sh
FROM nixos/nix
RUN nix-env -iA nixpkgs.ripgrep-all
ENTRYPOINT ["rga", "--rga-no-cache"]
```
3. create a script in your `$PATH`.
```sh
$ $EDITOR /usr/local/bin/rga
```
```sh
#!/bin/sh
# build the container if not present
if ! (docker inspect $USER/rga 2>/dev/null 1>&2) ; then
	docker build -t $USER/rga /usr/local/share/dockerfiles/jq > /dev/null
fi
# $RM_IT will be expanded into separate words without quotes
# we want the volume options to stay as a single word
RM_IT="--rm"
if [ -t 0 ]; then
	RM_IT="$RM_IT -it"
else
	RM_IT="$RM_IT -i"
fi
UID=$(id -u $(logname))
GID=$(id -g $(logname))
if [ -f ./docker_env ]; then
	DOCKER_ENV="--env-file docker_env"
fi
docker run \
	$DOCKER_ENV \
	$RM_IT \
	-u "$UID:$GID" \
	-w "$PWD" \
	-v "$PWD:$PWD" \
	"$USER/rga" \
	"$@"
```
4. make the script executable:
```sh
$ sudo chmod +x /usr/local/bin/rga
```


## remarks

heavily inspired by 
https://github.com/jessfraz/dockerfiles
which she featured in this video
https://www.youtube.com/watch?v=cYsVvV1aVss

the rga example was copied from here:
https://github.com/phiresky/ripgrep-all/pull/90/files
