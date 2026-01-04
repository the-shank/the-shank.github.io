---
layout: default
title: "TIL : Elixir - How to get a map from a struct"
date: 2017-09-22
tags:
  - elixir
  - til 
---

# TIL : Elixir - How to get a map from a struct

Use the [`Map.from_struct`](https://hexdocs.pm/elixir/Map.html#from_struct/1) function.

```elixir
struct = %User{first_name: "Jose", last_name: "Valim"}
map = Map.form_struct(struct)
```