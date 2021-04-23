# use_framework!

## OC 
默认使用 use_framework!
- #use_framework!    
    - OC 库、swift 库都静态库的形式链接进主二进制
    - 需要创建 bridge-header，没有 bridge-header 会报错 Undefined symbol

- use_framework!
    - OC 库、swift 库都动态库的形式链拷贝到 Frameworks 文件夹，在运行时链接
    - 不需要创建 bridge-header
    - 添加了 `[CP] Embed Pods Frameworks` phase


## swift
- #use_framework!  
    - OC 库、swift 库都静态库的形式链接进主二进制
    - 需要创建 bridge-header，没有 bridge-header 会导致 OC 库无法使用

- use_framework!
    - OC 库、swift 库都动态库的形式链拷贝到 Frameworks 文件夹，在运行时链接
    - 不需要创建 bridge-header
    - 添加了 `[CP] Embed Pods Frameworks` phase




use_framework决定了使用 framework 而不是静态库，use_framework! 的 :linkage 参数决定了 framework 是动态库还是静态库， 默认值是 :dynamic

use_framework! 会为 OC 库生成 modulemap 和 umbrella.h 文件 因此不用创建 bridge-header

# use_modular_headers!

为 cocoapods 静态库创建 modulemap 和 umbrella.h。

一种使用场景是 swift 工程使用静态库的方式使用一个 OC 库。要使用这个 OC 库，一般是创建一个 bridge-header.h，在该文件中 #import, 然后在 swift 中使用。

还可以使用 use_modular_headers! 或 :modular_header => true 来为 OC 库创建 modulemap 和 umbrella.h。从而避免创建 bridge-header.h
```rb
    pod 'Alamofire'
    pod 'AFNetworking', :modular_headers => true
```
