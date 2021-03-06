# nsorg [![Build Status](https://travis-ci.org/immoh/nsorg.svg?branch=master)](https://travis-ci.org/immoh/nsorg) [![cljdoc badge](https://cljdoc.xyz/badge/nsorg/nsorg)](https://cljdoc.xyz/d/nsorg/nsorg/CURRENT)

Clojure library for organizing `ns` form in a way that whitespace and comments are preserved.

Rules to apply are fully customizable; the default implementation

* sorts `:require`, `:require-macros`, `:use` and `:use-macros` libspecs alphabetically and removes duplicates
* sorts `:import` class names alphabetically and removes duplicates
* sorts `:exclude`, `:only`, `:refer`, `:refer-macros` and `:rename` options alphabetically and removes duplicates

Also available as Leiningen plugin [lein-nsorg](https://github.com/immoh/lein-nsorg)
and command line tool [nsorg-cli](https://github.com/immoh/nsorg-cli).

## Installation

Dependency information:

```clj
[nsorg "0.2.0"]
```

## Usage

```clj
(require '[nsorg.core :as nsorg])

(println (nsorg/rewrite-ns-form "
(ns foo
  ;; use
  (:use [a.c :only [y z x z]]
        a
        [a.b]
))
"))

(ns foo
  ;; use
  (:use a
        [a.b]
        [a.c :only [x y z]]
))
```

Check [API documentation](https://immoh.github.io/nsorg/) for more details.


## Limitations

* Throws exception on some valid ns forms
* Doesn't sort `:refer`, `:load` or `:gen-class` clauses


## License

Copyright © 2018 Immo Heikkinen

Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.
