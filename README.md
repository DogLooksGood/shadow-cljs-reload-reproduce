# Environments

OS: Linux

cli version: 2.8.41

node: v11.15.0

# How to reproduce

In project root.

```
$ npm install shadow-cljs

$ npx shadow-cljs start

$ npx shadow-cljs clj-repl

# In CLJ REPL

=> (shadow/watch :app)
```

In second terminal

```
$ npx shadow-cljs cljs-repl app
```

Open browser to http://localhost:4000.

In CLJS REPL, input following
```clojure
(ns bar.core)

(defn f []
  (println 2))

(in-ns 'foo.core)

(bar.core/f) ;;=> 1, works
```

Open file `src/foo/core.cljs`, uncomment the require. Save file.

Page will reload.

In CLJS REPL,

```clojure
(bar.core/f) ;; => 1, should be 2 here
```

Reload the browser tab, Then in CLJS REPL,

```clojure
(bar.core/f) ;; => error in browser console.
```

Check the output JS file,

```javascript
goog.provide('bar.core');
goog.require('cljs.core');

//# sourceMappingURL=bar.core.js.map
```
