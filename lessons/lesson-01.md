<!-- $theme: gaia -->
<!-- $size: 16:9 -->

# Elixir from the Ground Up
## ![28%](https://avatars2.githubusercontent.com/u/1481354?v=3&s=400)![](https://lever-client-logos.s3.amazonaws.com/logo_color@2x-3a2ee589.png) ![](http://emojipedia-us.s3.amazonaws.com/cache/09/36/093609b96d67b99f68fc329a9b2aff6f.png)

---

# Part One
## Introduction & Basics

---
<!-- *template: invert -->

# What We're Going to Cover
- Background
- Basic syntax
- Key features
- Functional programming basics
- Basic tooling (REPL, build tool, package repo)
- Futher reading & homework

---

# What is Elixir?

---
<!-- *template: invert -->

# ==iex>== h(Elixir)

- Functional
- Runs on BEAM (Erlang VM)
- Compiled, 
- Concurrent, fault-tolerant, hot-swappable
- Meta-programming
- Ruby-_inspired_ syntax & philosophy
- Friendly community 
  - JIKASWAK: "José is kind so we are also kind"

---
<!-- *template: invert -->

# Is Elixir a faster Ruby?

> I wouldn't classify Elixir as a better Ruby. Sure, Ruby was my main language before Elixir, but part of my work/research on creating Elixir was exactly to broaden this experience as much as possible and get some mileage on other ecosystems so I didn't bring a biased view to Elixir.
> 
> It's not Ruby, it's not Erlang, it is its own language.

<small>— *José Valim (Elixir's BDFL)*</small>

---
<!-- *template: invert -->

# What if you _want_ a faster Ruby?
## Clojure
- Once you get over the parentheses, the semantics are much closer
- Legend has it that Matz originally started Ruby as a Lisp
- Great community, tons of libs, Java & JS interop, &c...

## Crystal
- Looks & feels like Ruby, but _much faster_ (~60x)
- Still very early days

---

# What's Erlang?

---
<!-- *template: invert -->

# Erlang
- Developed by Ericsson in 1986 for telecom
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
- 

---
<!-- *template: invert -->

```ruby
# Ruby
user = User.new(name: "Grumpy Cat")
user.active.admin!
# user is modified in-place to be active and an admin
```

```js
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
- Push a subject through a series of functions
- Pass the result of one function to the next
```elixir
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
  @moduledoc "Check out my module!"
  
  # Comments look like this
  # ...but you probably want @doc
  
  @doc "Doubles a number"
  @spec my_double(integer) :: integer
  def my_double(number) do
    number * 2
  end
  
  defp private_function(number) do
    number * 10
  end
end
```

---
<!-- *template: invert -->

# Pattern Matching

---
<!-- *template: invert -->

# Arity

---
<!-- *template: invert -->

# Anonymous Functions

```elixir
# One-liner
fn x -> x + 1 end

# Multiple lines
fn single ->
  double = single * 2
  IO.puts "print this on its own line: #{double}"
end

# Multiple clauses (anonymous pattern match)
fn
  1           -> IO.puts "Simply one"
  {x, y}      -> IO.puts "Together: #{x + y}"
  any_one_arg -> any_one_arg |> IO.puts
  (x, y, z)   -> IO.puts "Three arg sum: #{x + y + z}"
end
```

---
<!-- *template: invert -->

# Shorthand Notations

```elixir
def my_add(a, b), do: a + b

if a == b, do: :equal, else: :false

&(&1 + &2)
```

---
<!-- *template: invert -->

# A Little Taste of Part 2

```elixir
# Get your process ID
parent = self()
#=> #PID<0.41.0>

# Spawn a new process, and print its ID
spawn fn ->
  send(parent, {:hello, self()})
end
#=> #PID<0.48.0>

# Receieve messages from other processes
receive do
  {:hello, pid} -> "Got hello from #{inspect pid}"
end
#=> "Got hello from #PID<0.48.0>"
```