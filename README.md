# ldump — serializer for any lua type

(description)

## TL;DR show me the code

(test here)

## Installation

## API

### ldump

```lua
ldump(value: any) -> string
```

Serialize given value to a string, that can be deserialized via `load`

### ldump.get_warnings

```lua
ldump.get_warnings() -> string[]
```

Get the list of warnings from the last ldump call.

See [`ldump.strict_mode`](#ldumpstrict_mode)

### ldump.ignore_upvalue_size

```lua
ldump.ignore_upvalue_size<T: function>(f: T) -> T
```

Mark function, causing dump to stop producing upvalue size warnings.

Upvalues can cause large modules to be serialized implicitly. Warnings allow to track that. Returns the same function.

### ldump.require_path

```lua
ldump.require_path: string
```

`require`-style path to the ldump module, used in deserialization.

Inferred from requiring the ldump itself, can be changed.

### serialize_function

```lua
type serialize_function = fun(any): (string | fun(): any)
```

Type of any serialize function, either defined in `getmetatable(x).__serialize` or passed through

### ldump.custom_serializers

```lua
ldump.custom_serializers: table<any, serialize_function> = {}
```

Custom serialization functions for the exact objects.

Key is the value that can be serialized, value is its serialization function. Takes priority over `getmetatable(x).__serialize`.

### ldump.strict_mode

```lua
ldump.strict_mode: boolean = true
```

If true (by default), `ldump` treats unserializable data as an error, if false produces a warning.
