# nar-serve - serve NAR file content

All the files in https://cache.nixos.org are packed in NAR files which makes them not directly accessible. This service allows to dowload, decompress, unpack and serve any file in the cache on the fly.

This avoids having to publish the build artifacts to two places.

## Use cases

* Avoid publishing build artifacts to both the binary cache and another service.
* Allows to share build results easily.
* Inspect the content of a NAR file.

## Deploy

This service is deployed on https://now.sh by default.

```sh
now
```

To specify your own cache (eg: cachix),

```sh
now --env NAR_CACHE_URI https://<yourcache>.cachix.org/
```

## Development

Inside the provided nix shell run:

```
./start-dev
```

This will create a small local server with live reload that emulates now.sh

## Usage

Append any store path to the hostname to fetch and unpack it on
the fly. That's it.

Eg:

* http://localhost:3000/nix/store/barxv95b8arrlh97s6axj8k7ljn7aky1-go-1.12/share/go/doc/effective_go.html

## Known issues

* NAR files are streamed from the cache which makes file access a O(N)
  operation on the number of files in the archive.
* No local disk cache is currently implemented
