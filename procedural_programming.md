# Procedural Programming

# Prioritize plain functions
Create classes only when the exclusive association between data and behavior is
not in doubt (queues, lists, vectors, etc.). Don't attempt to encapsulate state.

# Principles to follow
1. When in doubt, parametrize. Rather than passing data to functions through
   global variables, explicitly pass data through parameters.
2. Group globals into structs/classes
3. Favor pure functions (functions that don't modify state)
4. *Losely* encapsulate code at the level of namespaces/modules/packages (e.g.
   modules with private state and an interface)
5. Long functions are fine. Nesting functions is fine when some abstraction is
   needed.
6. In long functions, constrain the scope of local variables (curly brace blocks
   in most languages).
