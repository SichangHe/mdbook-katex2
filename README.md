# Important Notice

Use [`mdbook-katex`](https://github.com/lzanini/mdbook-katex) instead.

This is because I am now maintaining the original `mdbook-katex` and it is more convenient for users to use that original crate.

# README

`mdbook-katex2` aims to be a maintained version of `mdbook-katex`, providing equivalent functionality.

`mdbook-katex` is a preprocessor for [mdBook](https://github.com/rust-lang/mdBook), pre-rendering LaTex equations to HTML at build time. It allows for very fast page loading, compared to rendering equations in the browser.

This preprocessor uses the [katex](https://github.com/xu-cheng/katex-rs) crate; see [this page](https://katex.org/docs/supported.html) for the list of supported LaTex functions.

<p align="center">
  <img width="75%" height="75%" src="https://user-images.githubusercontent.com/71221149/107123378-84acbf80-689d-11eb-811d-26f20e32556c.gif">
</p>

## Getting Started

First, install `mdbook-katex2`

```shell
cargo install mdbook-katex2
```

Then, add the following lines to your `book.toml` file

```toml
[output.katex2]

[preprocessor.katex2]
```

You can now use `$` and `$$` delimiters for inline and display equations within your `.md` files. If you need a regular dollar symbol, you can escape delimiters with a backslash `\$`.

```
# Chapter 1

Here is an inline example, $ \pi(\theta) $, 

an equation,

$$ \nabla f(x) \in \mathbb{R}^n, $$

and a regular \$ symbol.
```

LaTex equations will be rendered as HTML when running `mdbook build` or `mdbook serve` as usual.

## Coming from `mdbook-katex`

In terms of using the preprocessor, there will be no difference except you add a `2` after `katex` as specified above in [Getting Started](#getting-started).

## Katex options

The preprocessor supports passing options to the katex-rs crate in order
to configure its behaviour. These options are specified under the
`[preprocessor.katex2]` directive.

The currently spported arguments are:
| Argument | Type |
| :- | :- |
| [`leqno`](https://katex.org/docs/options.html#:~:text=default-,leqno,-boolean) | `boolean` |
| [`fleqn`](https://katex.org/docs/options.html#:~:text=LaTeX-,fleqn,-boolean) | `boolean` |
| [`throw-on-error`](https://katex.org/docs/options.html#:~:text=package-,throwonerror,-boolean) | `boolean` |
| [`error-color`](https://katex.org/docs/options.html#:~:text=errorColor-,errorcolor,-string) | `string` |
| [`min-rule-thickness`](https://katex.org/docs/options.html#:~:text=state-,minrulethickness,-number) | `number` |
| [`max-size`](https://katex.org/docs/options.html#:~:text=true-,maxsize,-number) | `number` |
| [`max-expand`](https://katex.org/docs/options.html#:~:text=maxexpand) | `number` |
| [`trust`](https://katex.org/docs/options.html#:~:text=LaTeX-,trust,-boolean) | `boolean` |

There are also options to configure the behaviour of the preprocessor:
| Option | Default | Description |
| :- | :- | :- |
| `static-css` | `false` | Generates fully static html pages with katex styling |
| `macros` | `None` | Path to macros file (see [Custom macros](#custom-macros)) |

## Custom macros

Custom LaTex macros must be defined in a `.txt` file, according to the following pattern

```txt
\grad:{\nabla}
\R:{\mathbb{R}^{#1 \times #2}}
```

You need to specify the path of this file in your `book.toml` as follows

```toml
[preprocessor.katex2]
macros = "path/to/macros.txt"
```

These macros can then be used in your `.md` files

```
# Chapter 1

$$ \grad f(x) \in \R{n}{p} $$
```

## Caveats

The build artifact of the book will be in a folder named `html` inside the directory you specify instead of being directly there.
This is the same behaviour `mdbook_katex` has. Consider this when you use `mdbook_katex2` in your CIs.

`$\backslash$` does not work, but you can use `$\setminus$` instead.

## Acknowledgements

[`mdbook-katex`](https://github.com/lzanini/mdbook-katex) was developed by [Lucas Zanini](https://github.com/lzanini) et. al., see the original repository for all the individual contributions.
