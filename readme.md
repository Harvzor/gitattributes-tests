# .gitattributes testing

By default on Windows, if I clone a repo, it will put `crlf` line endings on the end of all files.

This is an issue if I clone an `.sh` file, followed by trying to run it with `bash`, since it doesn't allow Windows line endings.

The .gitattributes file in the root of the repo mitigates this by specifying which line endings to use.

## Clone repo without .gitattributes

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
$ od -c csharp.cs
```

## Clone repo with text set to `auto`

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
$ od -c csharp.cs
```

## Clone repo with text set to `crlf`

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
$ od -c csharp.cs
```

## Clone repo with text set to `lf`

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
> 0000000   #       S   o   m   e  \n   #       l   i   n   e   s  \n   #
> 0000020       o   f  \n   #       t   e   x   t   .  \n
> 0000034
$ od -c csharp.cs
> 0000000   /   /       S   o   m   e  \n   /   /       l   i   n   e   s
> 0000020  \n   /   /       o   f  \n   /   /       t   e   x   t   .  \n
> 0000040
```
