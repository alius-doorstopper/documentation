# Fundamental

## Primitives

### Bool

| Name | C++ equivalent |
|------|----------------|
| bool | bool           |

### Integer

for integer, we use the [Rust style naming](https://doc.rust-lang.org/reference/types.html)

| Name | C++ equivalent |
|------|----------------|
| i8   | int8_t         |
| i16  | int16_t        |
| i32  | int32_t        |
| u8   | int8_t         |
| u16  | int16_t        |
| u32  | int32_t        |

### Floating-point

| Name  | C++ equivalent |
|-------|----------------| 
| float | float          |

We only use 32 bits floating points.

## Serialization

### Bit ordering

We only use Little-endian when communicating data between modules.

### Containers

A container is a sequence of objects. In C++, this can be represented by array, vector or string.

Since the number of elements cannot always be known in advance by the deserializer, the serializer must include the
number of elements to be deserialized.

The length of the container must be expressed by an u16 variable. This choice is based on that for our usage, it is
possible to have more than 255 elements and extremely unlikely to have more than 2^16.

