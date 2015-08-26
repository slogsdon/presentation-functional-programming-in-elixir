# Functional Programming Principles in Elixir

GitHub:  @slogsdon
Twitter: @shanelogsdon


## First-Class Functions

```elixir
defmodule Functions do
  def add_x(x) do
    fn y -> x + y end
  end
end
```

```elixir
iex> add3 = Functions.add_x(3)
#Function<0.8925515/1 in Functions.add_x/1>
iex> add3.(4)
7
```
