<!-- $theme: gaia -->
<!-- $size: 16:9 -->

# Elixir from the Ground Up
## ![Elixir Logo](https://avatars2.githubusercontent.com/u/1481354?v=3&s=400)

---

<!-- *template: invert -->

# Part One
## Introduction & Basics

---

# What We're Going to Cover
- Background
- Syntax
- Key features
- Functional programming basics
- Basic tooling (REPL, build tool, package repo)
- Futher reading & homework

---

<!-- *template: invert -->

# What is Elixir?

---

# What is Elixir?

- Functional programming lanaguge
- Focus on concurrency and fault-tolerance
- Runs on the Erlang VM (BEAM)
- Ruby-_inspired_ syntax & philosophy
- Friendly community 
  - JIKASWAK: José is kind so we are also kind

---

# Is Elixir just a faster Ruby?

> I wouldn't classify Elixir as a better Ruby. Sure, Ruby was my main language before Elixir, but part of my work/research on creating Elixir was exactly to broaden this experience as much as possible and get some mileage on other ecosystems so I didn't bring a biased view to Elixir.
> 
> It's not Ruby, it's not Erlang, it is its own language.

<small>— *José Valim (Elixir's BDFL)*</small>

---

# What's Erlang?

---

# Not Object-Oriented
- No function dot-notation
- Immutible (no way to directly alter a value)

---

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

# Arity