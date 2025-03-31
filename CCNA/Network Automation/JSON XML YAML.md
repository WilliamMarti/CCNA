
##### Data Serialization

Process of converting data into a standardized format/structure that can be stored (in a file) or transmitted (over a network) and reconstructed later (by a different application)
	Allows data to be communicated between applications in a way both applications understand

Data serialization languages allow us to represent variables with text

JSON (JavaScript Object Notation) is an open standard file format and data interchange format that uses human-readable text to store and transmit data object

RFC8259

Derived from javascript, but language independent
	- REST APIs often use JSON

Whitespace is insignificant

JSON can represent for "primitive" data types
- string
- boolean
- number
- null

JSON also has two "structured" data types
- object
- array

##### JSON Primitive

String - Text value
Number - numeric value
Boolean - True/False
Null - No value, nothing

Object - unordered list of key-value pairs (variables)
objects are surrounded by curly brances {}
key is a string
value is any valid JSON data types (string/boolean/number/null/object/arrary)

If there are multiple key-value pairs, each pair is separated by a comma

Array - series of values separated by commas
Not key-value pairs
Don't have to be the same data type



