# Realise a derivation

Building a derivation is referred to as "realisation". A derivation is just an abstract
description of a package, based upon what it requires to build. However, a derivation does
not produce any expected outputs until it has been realised into something tangible. Taking
the example from above, one can build a derivations like so:

```
$ nix-store --realise /nix/store/byqskk0549v1zz1b2a61lb7llfn4h5bw-hello-2.10.drv
...
/nix/store/f4bywv8hjwl0ckv7l077pnap81h6qxw4-hello-2.10

# or in nix flakes:

$ nix build nixpkgs#hello
...
/nix/store/f4bywv8hjwl0ckv7l077pnap81h6qxw4-hello-2.10
```

The `nix-build` and `nix build` commands will perform both instantiation and realisation. 
These are the most commands used when iterating on packages. One could also do:

```
$ nix-buid '<nixpkgs>' -A hello
# these are the same, nix build is just much more concise
$ nix-store --realise $(nix-instantiate '<nixpkgs>' -A hello)
```