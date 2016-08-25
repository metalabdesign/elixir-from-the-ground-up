# Elixir from the Ground Up
## Lesson 1: What & How

![](http://elixir-lang.org/images/logo/logo.png)

---
# Example of simple examples (meta!) with syntax highlihting for the development team (you know who you are)

```ruby
[1, 2, 3].map {|a| a - 1}.reverse
#=> [2, 1, 0]

[1, 2, 3]
  .map {|a| a - 1}
  .reverse
#=> [2, 1, 0]
```

```elixir
[1,2,3] |> Enum.map(fn a -> a - 1 end) |> Enum.reverse
#=> [2, 1, 0]

[1,2,3]
|> Enum.map(fn a -> a - 1 end)
|> Enum.reverse
#=> [2, 1, 0]
```
