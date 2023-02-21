---
title:  "Coq Basic Syntax"
date:   2022-07-18 22:56:30 +0800
categories: 
  - Formal Method
tag:
 - coq
---

{% highlight coq %}
Inductive bool : Type :=
    | true
    | false.

Definition andb (b1:bool) (b2:bool) : bool :=
    match b1 with
    | true => b2
    | false => false
    end.
(*
Definition andb (b1:bool) (b2:bool) :bool :=
    if b1 then b2
    else false.
*)
Compute (andb false true).

Example test_andb :
    (andb false true) = false.
Proof. simpl. reflexivity. Qed.

Notation "x && y" := (andb x y).

Check andb:
    : bool -> bool -> bool.

{% endhighlight %}

