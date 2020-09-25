NAME
====
`Pakku::Meta` - Parse `Raku`'s `META` files

SYNOPSIS
========
```raku
use Pakku::Meta;

my $meta = Pakku::Meta.new: prefix => 'path/to/dist'.IO;

say ~$meta.identity;     # github:camelia:MyModule:0.0.1

say $meta.deps: :deps&lt;runtime&gt;;   # runtime  dependencies
say $meta.deps: :deps&lt;requires&gt;;  # required dependencies
```

DESCRIPTION
===========
`Pakku::Meta` is a module to parse `Raku` `META` files

INSTALLATION
===========
```
pakku add Pakku::Meta

# or 

zef install Pakku::Meta
```

METHODS
=======
Create a new object from `json`, `IO::Path` or `Hash`
```
multi method new ( Str:D :$json! )        { ... }
multi method new ( IO::Path:D :$prefix! ) { ... }
multi method new ( :$meta! )              { ... }
```

### identity
Returns `Identity` object that stringfies to `auth:name:ver`
```
method identity ( ) { ... }
```

### deps
Returns the dependencies (runtime, test, build, suggests, ...)

```
multi method deps (                                  ) { ... }
multi method deps ( Str:D  :$deps where 'suggests'   ) { ... }
multi method deps ( Str:D  :$deps where 'recommends' ) { ... }
multi method deps ( Str:D  :$deps where 'requires'   ) { ... }
multi method deps ( Str:D  :$deps where 'runtime'    ) { ... }
multi method deps ( Str:D  :$deps where 'test'       ) { ... }
multi method deps ( Str:D  :$deps where 'build'      ) { ... }
multi method deps ( Str:D  :$deps where 'only'       ) { ... }
multi method deps ( Bool:D :$deps where *.so         ) { ... }
multi method deps ( Bool:D :$deps where not *.so     ) { ... }
```

### to-dist
Mix in `Distribution::Locally`, and can be installed to `CompUnit::Repository::Installation`

```
method to-dist ( ::?CLASS:D: IO :$prefix! ) { ... }
```

### to-json
Returns `META` as `json`

```
method to-json  ( ) { ... }
```

AUTHOR
======
Haytham Elganiny <elganiny.haytham@gmail.com>

COPYRIGHT AND LICENSE
=====================
Copyright 2020 Haytham Elganiny

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

