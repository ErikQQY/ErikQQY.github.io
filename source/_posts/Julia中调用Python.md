---
tags: Julia
---
# Julia中调用Python  
Julia在作为一个科学计算语言的同时，也吸取了其它语言的优点，具备胶水语言的能力  
首先
```julia
julia> using Pkg
julia> Pkg.add("PyCall")
```
把调用Python的包PyCall下载下来  
在编译```Pkg.build("PyCall")```之前，我们需要指定Julia调用的是电脑上的那个Python  
在REPL中：
```julia
julia> ENV["PYTHON"]="Python的路径"
julia> Pkg.build("PyCall")#设置完后一定要build一下
```
然后就可以在Julia中愉快地继续做**调包侠**了😄