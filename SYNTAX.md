# New Syntax

## Functions
Functions now follow brace based ( { } ) scoping rather than indentation.
Tab count/indentation is not important.
```gdscript
func _process(delta: float) -> void {
  # whatever
}
```

## Conditionals and loops
If, for and while now follow brace based scoping rather than indentation.
Tab count/indentation is not important.
```gdscript
if 5 > 2 {
  print("5 is greater than 2.")
}

for i in range(10) {
  print(i)
}

var i := 0
while i < 10 {
  print(i)
  i += 1
}
```

### Match cases
The match operation works a little differently. Before, gdscript used indentation
level to figure out if something is a case expression or part of the statement block.
This cannot be used as indentation is no longer a factor.

Instead of introducing a new case keyword I decided to borrow from the [ML language family](https://en.wikipedia.org/wiki/OCaml)
and use the pipe operator ('|') to specify a new case expression followed by a colon.

This should make it that you can inline your entire match statement (probably don't do that.)
```gdscript
match state {
| State.IDLE:
  print("I am idle!")
| var walking when state == State.WALKING:
  print("Is walking? ", walking)
| _:
  print("Not idle or walking.")
}
```

## Variable declaration
Variable declaration is unchanged **except** for setters and getters. To add setters and getters
you add a brace scope after your variable declaration.
```gdscript
var damage {
  set = set_damage,
  get = get_damage
}

var health: int {
  set(value) {
    health = value
  }
  get {
    return health
  }
}

var armor: int = 10 { set(value) { armor = value; } get { return armor; } }

```

## Inline Class declaration
Inline class declarations now use brace scoping rather than indentation.

```gdscript
class Player {
  const MAX_HEALTH: int = 100

  var health: int
  var damage: int

  func _init(p_damage: int, p_health: int = MAX_HEALTH) {
    health = p_health
    damage = p_damage
  }
}
```
