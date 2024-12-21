# Developing with Python - `pip` VS `uv`

This repo is meant to serve as both an optimized example and comparison of Python projects using [pip](https://pypi.org/project/pip/) vs [uv](https://docs.astral.sh/uv/) for project setup and development.

The comparison here is primarily to weigh the pros and cons of the development experience, including build speeds.

In conclusion, I don't think I'll be starting any new projects _without_ `uv`, and will additionally strive to move existing projects to `uv` where possible.

## Docker

This section looks at build speeds and sizes for optimized Docker images using both tools.

### pip

For pip, I used the following command

```sh
multitime -n 10 -v docker build . -t pipexample --no-c
ache
```

with this result

```sh
===> multitime results
1: docker build . -t pipexample --no-cache
            Mean        Std.Dev.    Min         Median      Max
real        84.876      8.565       68.982      83.104      98.847      
user        0.327       0.025       0.277       0.328       0.372       
sys         0.182       0.020       0.145       0.185       0.214  
```

### uv

For uv, I used the following command

```sh
multitime -n 10 -v docker build . -t uvexample --no-cache
```

with this result

```sh
===> multitime results
1: docker build . -t uvexample --no-cache
            Mean        Std.Dev.    Min         Median      Max
real        25.323      6.883       18.393      22.478      41.407      
user        0.106       0.022       0.080       0.102       0.154       
sys         0.063       0.012       0.044       0.063       0.083  
```

### Conclusion

As can be seen from the results above, `uv` performs significantly better even on a "trivial" example. 84 seconds compared to 25 seconds is _significant_ in the amount of CI time that would be saved, and the enhancement that brings to the speed of the development feedback loop.

## Developer Experience

This section looks at the differences in how dependencies are managed between the two tools.

### pip

Well...`pip` is `pip`! If you use Python, you should already be familiar with it. It allows a lot of flexibility, but lacks many features that make modern developer experiences more ergonomic.

### uv

`uv` Strives to be a [cargo](https://github.com/rust-lang/cargo) for Python. Unlike `pip`, which depends on Python already being installed, `uv` will also manage Python versions as well as virtual environments on a per-project basis. This makes it a developer experience much more akin to `node` or `rust`, allowing you to fearlessly hop between projects without having to remember to switch virtual/conda environments.

While it is similar to `conda` in that `conda` can also manage Python versions on a per-environment basis, `uv` is the next logical step in toolchain ergonomics.
