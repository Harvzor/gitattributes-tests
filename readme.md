# .gitattributes testing

By default on Windows, if I clone a repo, it will put `crlf` line endings on the end of all files.

This is an issue if I clone an `.sh` file, followed by trying to run it with `bash`, since it doesn't allow Windows line endings.

The .gitattributes file in the root of the repo mitigates this by specifying which line endings to use.

## Clone or re-checkout

Switching between branches of this repo won't re-create the files with the correct line endings.

https://stackoverflow.com/questions/48642692/how-to-make-change-to-gitattributes-take-effect

Either you have to clone the repo with the `.gitattributes` set:

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
```

Or you can re-init the repo:

```
$ git rm -r :/ && git checkout HEAD -- :/`
```

## No `.gitattributes`

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
$ od -c csharp.cs
```

## Text set to `auto`

### On Windows

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
> 0000000   /   /       S   o   m   e  \r  \n   /   /       l   i   n   e
> 0000020   s  \r  \n   /   /       o   f  \r  \n   /   /       t   e   x
> 0000040   t   .  \r  \n
> 0000044
$ od -c csharp.cs
>0000000   #       S   o   m   e  \r  \n   #       l   i   n   e   s  \r
> 0000020  \n   #       o   f  \r  \n   #       t   e   x   t   .  \r  \n
> 0000040
```

### On Linux

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

## Text set to `crlf`

```
$ git clone --branch lf https://github.com/Harvzor/gitattributes-tests
$ od -c bash.sh
> 0000000   #       S   o   m   e  \r  \n   #       l   i   n   e   s  \r
> 0000020  \n   #       o   f  \r  \n   #       t   e   x   t   .  \r  \n
> 0000040
$ od -c csharp.cs
> 0000000   /   /       S   o   m   e  \r  \n   /   /       l   i   n   e
> 0000020   s  \r  \n   /   /       o   f  \r  \n   /   /       t   e   x
> 0000040   t   .  \r  \n
> 0000044
```

## Text set to `lf`

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
