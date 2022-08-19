# Object Oriented Programming Is Bad

# Inheritance
Inheritance is to be careful with or to avoid entirely.

# Polymorphism
Polymorphism isn't exclusive to OOP. Procedural code can be just as if not more
polymorphic as OOP code.

# Encapsulation
An object is an encapsulated state. We interact with that state via a defined
set of messages to the object called Public Interface.

OOP code is a graph of messages between objects. This code violates
encapsulation, because:
1. The original idea of messages was to send copies of state, not the references
   themselves.
2. For an object A to send a message to an object B, A must have a private
   reference to the object B, which makes B part of A's private state. So by
   sending a message object A may indirectly modify state of object B.
3. If other objects send messages to object B, we have shared state, which is
   hardly any different from a single global variable being shared by multiple
   functions in procedural programming.

Sharing objects violates encapsulation. Only way to prevent that is to organize
code in a hierarchical tree, where each object in the hierarchy is responsible
for its direct children. Messages can only be send from an object to its direct
child. Nobody writes programs this way.
