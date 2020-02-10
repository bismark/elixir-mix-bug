# Elixir 1.10 Mix Bug

This is a minimal reproduction of a bug in mix.

With Elixir 1.10, run the following:

```
$ mix deps.get && mix compile && mix deps.update ecto_sql
```

and you will get an error:

```
Dependencies have diverged:
* ecto (Hex package)
  the dependency ecto 3.3.1

  > In deps/ecto_enum/mix.exs:
    {:ecto, ">= 3.0.0", [env: :prod, hex: "ecto", repo: "hexpm", optional: false]}

  does not match the requirement specified

  > In deps/ecto_sql/mix.exs:
    {:ecto, "~> 3.4 or ~> 3.3.2", [env: :prod, hex: "ecto", repo: "hexpm", optional: false]}

  Ensure they match or specify one of the above in your deps and set "override: true"
** (Mix) Can't continue due to errors on dependencies
```

However the deps appear to be correctly installed and subsequent `mix` work without error.

To reset back to the base state:

```
$ git checkout -- mix.lock && mix deps.get && mix compile
```
