# ghc-parmake

[![Build Status](https://secure.travis-ci.org/23Skidoo/ghc-parmake.png?branch=master)](http://travis-ci.org/23Skidoo/ghc-parmake)

`ghc-parmake` is a parallel wrapper for `ghc --make` intended to work as its
drop-in replacement. It can build your Haskell program in parallel using
multiple cores and will be integrated with `cabal build` eventually (though I
also plan to support the standalone version).

To use it with cabal, try `cabal build --with-ghc=ghc-parmake --ghc-options="-j N"`.

`ghc-parmake` works by first extracting a module dependency graph with `ghc -M`
and then running multiple `ghc -c` processes in parallel. Currently, it can
build itself and some small test programs (see the `tests` directory).

To set the number of concurrent jobs, use the `-j` option.

## Usage

    ghc-parmake OPTS FILES

    -j N             - Run N jobs in parallel.
    --ghc-path=PATH  - Set the path to the ghc executable.

    -vv[N]           - Set verbosity to N (only for ghc-parmake).
                       N is 0-3, default 1.
    -v[N]            - Set verbosity to N (both for GHC and ghc-parmake itself).
    --help           - Print usage information.
    -V               - Print version information.

Other options are passed to GHC unmodified.

## Known limitations

* Build fails when `-odir` != `-hidir`.
* Tested only on Linux.
