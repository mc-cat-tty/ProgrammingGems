# Data Classes

## dataclass vs NamedTuple

|`dataclasses.dataclass` | `typing.NamedTuple`|
|------------------------|--------------------|
| Mutable unless frozen | Immutable |
| Inheritance | No inheritance from classes oter than NamedTuple |
| Uncomparable | Comparable |
| Unhashable | Hashable |


But... dataclass(frozen=True) can be partially overlapping.
