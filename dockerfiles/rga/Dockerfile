FROM nixos/nix
RUN nix-env -iA nixpkgs.ripgrep-all
ENTRYPOINT ["rga", "--rga-no-cache"]
