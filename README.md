# vagrant-lein-nrepl
Vagrantfile that sets up Leiningen and starts a headless REPL.

The Upstart script `nrepl` isn't currently working, but it is possible to start the REPL server by sshing in and running

```
lein repl :headless :host 0.0.0.0 :port 4343
```

You can then connect to the REPL at `127.0.0.1:4343` on your host.
