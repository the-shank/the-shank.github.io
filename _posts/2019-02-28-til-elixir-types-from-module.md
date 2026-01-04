---
layout: default
title: "TIL: Elixir - How to see the types defined by a module in IEx"
date: 2019-02-28
tags:
  - elixir
  - til 
---

# TIL: Elixir - How to see the types defined by a module in IEx

You can display typespecs from a module thorugh `t` command on iex, i.e:

```shell
iex(1)> t Enum
@type t() :: Enumerable.t()
@type acc() :: any()
@type element() :: any()
@type index() :: integer()
@type default() :: any()
```

Reference: [IEx.Helpers.t](https://hexdocs.pm/iex/1.8.0/IEx.Helpers.html#t/1)