# Functional Programming
# Principles in Elixir

GitHub:  @slogsdon
Twitter: @shanelogsdon


## First-Class

Functions are treated as values

```elixir
defmodule Functions do
  def add_x(x) do
    fn y -> x + y end
  end
end
```

^ Partial application


## First-Class

```elixir
iex> add3 = Functions.add_x(3)
#Function<0.8925515/1 in Functions.add_x/1>
iex> add3.(4)
7
```


## First-Class

```cs
delegate int del(int i);
static del AddX(int x)
{
    return y => x + y;
}
```


## Higher-Order

Functions can accept other functions as arguments

```elixir
defmodule Functions do
  def do_x(f, x) do
    f.(x)
  end
end
```


## Higher-Order

```elixir
iex> Functions.do_x(add3, 4)
7
```


## Higher-Order

```cs
myList // List<string>
  .Where(x => x == "value");
```


## Composition

Combine simple functions to build complicated ones

```elixir
defmodule Sprockets do
  def get_valid(sprockets) do
    sprockets
    |> Enum.filter(Sprockets.is_round?/1)
    |> Enum.filter(Sprockets.has_12_teeth?/1)
  end
  defp is_round?(_), do: true
  defp has_12_teeth?(%{teeth: t}), do: t == 12
end
```


## Composition

```cs
mySprockets // List<Sprocket>
  .Where(s => s.IsRound)
  .Where(s => s.Teeth.Count == 12);
```


## Pure Functions

- Referentially Transparent
- Don't modify external state
- Don't produce side effects


## Pure Functions

- Predictable
- Make for easily testable code

## Pure Functions

Pure:

- Enum.map
- String.split

Impure:

- IO.inspect


## Recursion

No standard loops

```cs
var i = 0;
while (i < myList.Count)
{
    // do something
    i++;
}
```


## Recursion

```elixir
defmodule Functions do
  def len([]),      do: 0
  def len([h | t]), do: 1 + len(t)
end
```


## Recursion

```cs
static int Len(List<T> myList)
{
    if (myList.Count == 0) return 0;
    return 1 + Len(myList.RemoveAt(0));
}
```


## Recursion

```elixir
defmodule Functions do
  def fac(0), do: 1
  def fac(n), do: n * fac(n - 1)
end
```


## Recursion

```elixir
defmodule Functions do
  def tfac(n, acc \\ 1)
  def tfac(0, acc), do: acc
  def tfac(n, acc), do: tfac(n - 1, n * acc)
end
```


## Eager vs. Lazy

Eager evaluation always fully evaluates function arguments before invoking the function. Lazy evaluation does not evaluate function arguments unless their values are required to evaluate the function call itself.

```elixir
1..1_000_000_000_000
|> Enum.map(fn x -> x + 2 end)
|> Enum.take(3)
|> Enum.to_list
```


## Eager vs. Lazy

```elixir
1..1_000_000_000_000
|> Stream.map(fn x -> x + 2 end)
|> Stream.take(3)
|> Enum.to_list
#=> [3,4,5]
```


## Eager vs. Lazy

```cs
static IEnumerable<int> GetPrimes()
{
     int i = 1;
     while (true)
     {
         if (IsPrime(i))
         {
             yield return i;
         }
         i++;
     }
}
```


## Types

- Pattern matching
- Structs
- Behaviours
- Protocols


## Lists

Code time


## Questions?

Go for it!

github.com/slogsdon/presentation-functional-programming-in-elixir
