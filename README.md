[![Clojars Project](https://img.shields.io/clojars/v/deps-deploy.svg)](https://clojars.org/deps-deploy)
# deps-deploy

A Clojure library to deploy your stuff to clojars with `clj` or `clojure`. It's a very thin wrapper around
Chaz Emericks [pomegranate](https://github.com/cemerick/pomegranate) library.

It will read your Clojars username/password from the environment variables `CLOJARS_USERNAME` and `CLOJARS_PASSWORD`.

## Usage

To deploy to Clojars, simply merge 

```clojure
{:deploy {:extra-deps {deps-deploy {:mvn/version "RELEASE"}}
          :main-opts ["-m" "deps-deploy.deps-deploy" "deploy"
		      "path/to/my.jar" "group-id/artifact-id" "x.y.z"]}}
```
into your `deps.edn`, have a `pom.xml` handy (you can generate one with `clj -Spom),` and deploy with

```sh
$ env CLOJARS_USER=username CLOJARS_PASSWORD=password clj -a:deploy
```

to deploy to Clojars

You can also store your credentials in a symmetrically encryted file:

```sh
$ gpg --encrypt .clojars_creds.edn
```

`deps-deploy` will then prompt you for the passphrase


`deps-deploy` also supports installing to your local `.m2` repo, by invoking `install` instead of `deploy`:
```clojure
{:install {:extra-deps {deps-deploy {:mvn/version "RELEASE"}}
           :main-opts ["-m" "deps-deploy.deps-deploy" "install"
			   "path/to/my.jar" "group-id/artifact-id" "x.y.z"]}}
```



## License

Copyright © 2018 Erik Assum

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
