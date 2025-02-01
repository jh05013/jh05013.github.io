+++
title = "Test test test"
date = 2025-01-27
[extra]
katex = true
disclaimer = "test post please ignore"
+++

[Zola](https://www.getzola.org/) 라는 블로그 도구를 써보고 있습니다.

✨

> This quote contains:
> 
> - **bold** *italic* ~strikethrough~
> - Items
>   - Sub-items
> - Items
> - [ ] Checkboxes
> - [x] No, you can't click on them
>
> Also:
> 1. numbered item
> 2. ok!

[link](https://github.com)

Footnote[^1] was here. Proof: let $\epsilon < 0$, then

$$
\int_0^1 x dx = \infty
$$
<del>Contradiction</del> <ins>QED</ins>

{% alert(caution=true) %}
The proof above has
<span class="spoiler solid">an error</span>.
<small>Or does it?</small>
Can you find it?
<details>
  <summary>Answer</summary>
  Yes, you can find it.
</details>
{% end %}

<abbr title="Alternative Branching Cubes">ABC</abbr>

[^1]: footnote, yes.

# H1
## H2
### H3
#### H4
##### H5
###### H6

`code`

```rust
fn main() {
  println!("block of code");
}
```

---

| z | x | c |
| - | - | - |
| asd | sdf | dfg |
| asd | sdf | dfg |

# Media
![Title text](https://upload.wikimedia.org/wikipedia/commons/thumb/2/24/Male_mallard_duck_2.jpg/800px-Male_mallard_duck_2.jpg)

![Title text when image is not available](https://fviewunc)

{{ youtube(id="dQw4w9WgXcQ") }}

<aside>
asdf
</aside>

Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum
Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum
Lorem ipsum Lorem ipsum Lorem ipsvm Lorem ipsum Lorem ipsum
Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum
Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum
Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum
Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum

<div class="buttons">
  <a href="#top">Go to Top</a>
  <a class="colored external" href="https://example.org">Example</a>
</div>

# Forms
<ul>
  <li>
    <input type="checkbox" />
    <label>&nbsp;Ok you *can* click on these</label>
  </li>
  <li>
    <input type="checkbox" checked />
    <label>&nbsp;Here I clicked them for u</label>
  </li>
  <li>
    <input type="checkbox" disabled />
    <label>&nbsp;Except this one</label>
  </li>
  <li>
    <input type="checkbox" class="switch" />
    <label>&nbsp;??</label>
  </li>
</ul>

<ul>
  <li>
    <input type="radio" name="test" />
    <label>&nbsp;Milk</label>
  </li>
  <li>
    <input type="radio" name="test" />
    <label>&nbsp;Eggs</label>
  </li>
  <li>
    <input type="radio" name="test" />
    <label>&nbsp;Flour</label>
  </li>
  <li>
    <input type="radio" name="test" checked />
    <label>&nbsp;Coffee</label>
  </li>
  <li>
    <input type="radio" name="test" disabled />
    <label>&nbsp;Combustible lemons</label>
  </li>
</ul>

<label>Color:</label>
<input type="color" value="#000000" />

<input type="range" max="100" value="33" id="range">
