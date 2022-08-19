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

# How procedural programs should be written (example)
- State modules (may contain internal state, may reach out for external state)
  State modules should protect their private states, and should only touch each
  other's private interfaces.
- Logic modules (may not contain internal state, may not reach out for external
  state). Logic modules generate data and mutate its imputs, and should have
  private and public functions as well.
- Data types. Stand on their own and don't belong to any state or logic module.

State modules can call logic modules, but never the other way around. State code
should be minimized in favor of logic code as much as possible.

# How to split modules
- Split modules to divide and conquer state menagement
- By features (feature A belongs to module A...)
- By team, for collaboration (group A works on module A...)
