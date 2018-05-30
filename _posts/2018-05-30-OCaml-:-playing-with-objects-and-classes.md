---
layout: post
title: OCaml : playing with objects and classes
categories: OCaml POO
---
Most of the material comes from : "Real World OCaml"

# Objects:

  * abstraction
  * dynamic lookup
  * subtyping
  * inheritance
  * open recursion

## subtyping and inheritance:

  - Subtyping : object A with all functionnalities of B can be used where B is
  expected.
  - Inheritance: the definition of one kind of object can be reused to produce
  a new kind of object. This new definition can override some behavior, but also
  share some code.

## First objects:

### Simple object creation

```OCaml
let a = object
  val name = "chien"

  method says =
    print_endline "whoaf"
end
(* signature : val a : < says : unit > = <obj>
   usage : a#says
*)
```
usage:

```OCaml
a#says
```

### Create object via a function:

```OCaml
let animal specie sound = object
  val name = specie

  method says =
    print_endline sound
end
(* signature: val animal : 'a -> string -> < says : unit > = <fun>*)
```

usage:

```OCaml
let b = animal "vache" "meuh"

b#says
```

### Object Polymorphism:

Methods can be used without explicit type description:

```OCaml
let elapsed t = t#start - t#stop;;
val elapsed : < start : int; stop : int; .. > -> int = <fun>
let reset t : unit = t#set 0;;
val reset : < set : int -> unit; .. > -> unit = <fun>
let show_elapsed t =
let time = elapsed t in let () = print_endline (string_of_int time) in reset t;;
val show_elapsed : < set : int -> unit; start : int; stop : int; .. > -> unit = <fun>
```

Object types are inferred automatically from the methods that are invoked on them.

It is possible to manually close an object type:

```OCaml
let elapsed (t: <start : int; stop : int>) = t#start - t#stop
```

### Subtyping

#### Width subtyping
#### Depth subtyping
### Variance
### Narrowing
### Subtyping versus Row Polymorphism

## Classes

