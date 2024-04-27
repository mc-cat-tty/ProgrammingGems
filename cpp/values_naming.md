# Value naming
According to https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2010/n3055.pdf, Cpp values are now named:
 - glvalue: Generalized Left Value
	- lvalue: Left Value
	- xvalue: eXpiring Value
 - rvalue: Right Value
	- xvalue: eXpiring Value
	- prvalue: Pure Right Value

Rvalue references where introduced to capture rvalue temporary, allowing modifications. This scenario was previously managed through lvalue const references, which didn't allow to edit the parameter value.
Every expression belongs to exactly one of the three classifications of the taxonomy; this property is called its _value category_.

The conversion rules are described from page 5 to page 20 in the document linked above.
