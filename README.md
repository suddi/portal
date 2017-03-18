# Portal

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/89635da7915a4bc3a6606adf62c254b0)](https://www.codacy.com/app/Suddi/portal?utm_source=github.com&utm_medium=referral&utm_content=suddi/portal&utm_campaign=badger)

Portal game in Elixir following the guide in [How I Start.](https://howistart.org/posts/elixir/1).

## Usage

To open an Elixir process to communicate through:
````sh
iex --sname room1 --cookie secret -S mix
````

A second process:
````sh
iex --sname room2 --cookie secret -S mix
````

In `room1`:
````elixir
iex(room1@zenith)1> Portal.shoot(:blue)
{:ok, #PID<0.118.0>}
````

In `room2`:
````elixir
iex(room2@zenith)1> Portal.Door.get({:blue, :"room1@zenith"})
[]

iex(room2@zenith)2> Portal.shoot(:orange)
{:ok, #PID<0.124.0>}

iex(room2@zenith)3> orange = {:orange, :"room2@zenith"}
{:orange, :room2@zenith}

iex(room2@zenith)4> blue = {:blue, :"room1@zenith"}
{:blue, :room1@zenith}

iex(room2@zenith)5> portal = Portal.transfer(orange, blue, [1, 2, 3, 4])
#Portal<
  {:orange, :room2@zenith} <=> {:blue, :room1@zenith}
              [1, 2, 3, 4] <=> []
>

iex(room2@zenith)6> Portal.push_right(portal)
#Portal<
  {:orange, :room2@zenith} <=> {:blue, :room1@zenith}
                 [1, 2, 3] <=> [4]
>

````

In `room1`:
````elixir
iex(room1@zenith)2> orange = {:orange, :"room2@zenith"}
{:orange, :room2@zenith}

iex(room1@zenith)3>  blue = {:blue, :"room1@zenith"}
{:blue, :room1@zenith}

iex(room1@zenith)4> Portal.Door.get(orange)
[3, 2, 1]

iex(room1@zenith)5> Portal.Door.get(blue)
[4]
````
