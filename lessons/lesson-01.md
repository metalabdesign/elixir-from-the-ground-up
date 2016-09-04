<!-- $theme: gaia -->
<!-- $size: 16:9 -->

# Elixir from the Ground Up
## ![30%](https://avatars2.githubusercontent.com/u/1481354?v=3&s=400)![](https://lever-client-logos.s3.amazonaws.com/logo_color@2x-3a2ee589.png) ![](http://emojipedia-us.s3.amazonaws.com/cache/09/36/093609b96d67b99f68fc329a9b2aff6f.png)

---

# Part One
## Introduction & Basics

---
<!-- *template: invert -->
# What We're Going to Cover
- Background
- Syntax
- Key features
- Functional programming basics
- Basic tooling (REPL, build tool, package repo)
- Futher reading & homework

---

# What is Elixir?

---
<!-- *template: invert -->

# What is Elixir?

- Functional programming lanaguge
- Concurrent, fault-tolerant, hot-swappable
- Actor Model
- Runs on the Erlang VM (BEAM)
- Meta-programming
- Ruby-_inspired_ syntax & philosophy
- Friendly community 
  - JIKASWAK: "José is kind so we are also kind"

---
<!-- *template: invert -->

# Is Elixir just a faster Ruby?

> I wouldn't classify Elixir as a better Ruby. Sure, Ruby was my main language before Elixir, but part of my work/research on creating Elixir was exactly to broaden this experience as much as possible and get some mileage on other ecosystems so I didn't bring a biased view to Elixir.
> 
> It's not Ruby, it's not Erlang, it is its own language.

<small>— *José Valim (Elixir's BDFL)*</small>

---

# What's Erlang?

---

<!-- *template: invert -->

# Erlang
- Developed by Ericsson in 1986 to run network switches
  - Need high uptime, automatic recovery, soft-realtime, streaming
- Used in every phone call that you've ever made
- Unusual syntax (based on Prolog)

```erlang
%% Author: Arjun Sunel via Rosetta Code
main()-> test(8).
test(N)->
	if (N rem 2)==1 -> io:format("odd\n");
	true -> io:format("even\n")
	end.			
```

---

<!-- *template: invert -->

# Not Object-Oriented
- No function dot-notation
- Immutible (no way to directly alter a value)

---

<!-- *template: invert -->

```ruby
# Ruby
user = User.new(name: "Grumpy Cat")
user.active.admin!
# user is modified in-place to be active and an admin
```

```javascript
// JS
user = new User();
user.name = "Grumpy Cat";
Role.activate(user);
Role.make_admin(user);
// user is modified to be active and an admin
```

```elixir
# Elixir
user = %User{name: "Grumpy Cat"}
active_user = Role.activate(user)
admin = Role.make_admin(active_user)
# `user`, `active_user`, and `admin` are all different values
```

---

<!-- *template: invert -->

# Pipe Operator

```elixir
user = %User{name: "Grumpy Cat"}
active_user = Role.activate(user)
admin = Role.make_admin(active_user)

# Piped %User{}
%User{name: "Grumpy Cat"} |> Role.activate |> Role.make_admin

# Normal, crowded
to_string(Enum.sum(Enum.map([1,2,3], &MyModule.double/1)))
#=> "12"

# Pipe broken onto multiple lines
[1,2,3]
|> Enum.map(&MyModule.double/1) # [1,2,3] gets piped into the *first* arg
|> Enum.sum
|> to_string
#=> "12"
```

---
<!-- *template: invert -->

# Modules, not Classes

```elixir
defmodule MyModule do

  # Comments look like this
  
  def my_double(number) do
    number * 2
  end
end
```

---

<!-- *template: invert -->

# Arity

---

# Actor Model
- Not unique to Erlang/Elixir
  - Nice that it's in the standard lib, though