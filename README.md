# Example of using TLS for Erlang Distribution with an Elixir Release

## Usage

Generate the release:

```bash
git clone git@github.com:ConnorRigby/elixir-distribution-ssl-example.git
cd elixir-distribution-ssl-example
mix release
```

Next, open two terminals in the same directory, in one do:

```bash
env RELEASE_NODE=ssl_test1@127.0.0.1 RELEASE_DISTRIBUTION=name _build/dev/rel/example/bin/example start_iex
```

in the second do:

```bash
env RELEASE_NODE=ssl_test2@127.0.0.1 RELEASE_DISTRIBUTION=name _build/dev/rel/example/bin/example start_iex
```

And finally back in the first one connect to the second:

```elixir
Node.connect(:"ssl_test2@127.0.0.1")
```

Now these nodes are distributed via SSL.

## Bugs

When using TLS in this way, a lot of the helper script generated by Elixir will not work correctly, namely the `remote`
function and anything that works using the same mechanism. There is an open issue [here](https://github.com/elixir-lang/elixir/issues/10656)