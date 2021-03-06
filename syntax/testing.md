# Tacit ideas / Syntax / Testing

Testing files are named `*.test.tacit` and all get automatically run.

Inside a test file, all identifiers from the "base" (non-test) module are imported directly, including hidden identifiers. (The testing package also gets imported directly.)

Tests are optionally named using a comment from the preceding line:

```
-- [sqrt]
test:
  -- Four
  test:
    4 sqrt  2  eq assert

  -- Other numbers
  arr:
    :
      input < 16
      output < 4
    :
      input < 9
      output < 3
  test-cases: input output >
    input sqrt  output  eq assert
```

Because Tacit modules can't have side effects, it's easy to tell exactly which tests need to run when code changes, and Tacit will only run the minimal set of tests again during continuous testing mode.

When showing progress, only test files are enumerated. Details are shown using a lattice, with double-line intersections coloured green for pass and single-line intersections showing red for fail. Details and context are only shown for the first failing test. Hierarchy is used to help navigation. A summary footer is also shown with test counts, with the "todo" line animated as ocean waves or a zigzag spark.
```
╭╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╮
╎ parse/parse.test.tacit                  ╎
╎ ╭╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╮ ╎
╎ ╎ parse-number                        ╎ ╎
╎ ╎ ╭╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╮ ╎ ╎
╎ ╎ ╎ Valid input                     ╎ ╎ ╎
╎ ╎ ╎ ╔╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╗ ╎ ╎ ╎
╎ ╎ ╎ ╠╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╣ ╎ ╎ ╎
╎ ╎ ╎ ╠╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╩╩╩╝ ╎ ╎ ╎
╎ ╎ ╎ ╚╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╝     ╎ ╎ ╎
╎ ╎ ╰╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╯ ╎ ╎
╎ ╎ ╭╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╮ ╎ ╎
╎ ╎ ╎ Invalid input                   ╎ ╎ ╎
╎ ╎ ╎ ╔╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦┬╦╦╦╦╦╗ ╎ ╎ ╎
╎ ╎ ╎ ╠╬┼╬╬╬╬╬╬╬╬╬╬┼┼╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╣ ╎ ╎ ╎
╎ ╎ ╎ ╠╬╬╬╬╬╬╬╬╬╬╬┼┼┼┼╬╬╬╬╬╬╬╬╬╬╬╩╩╩╝ ╎ ╎ ╎
╎ ╎ ╎ ╚╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩┴┴╩╩╩╩╩╝     ╎ ╎ ╎
╎ ╎ ╰╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╯ ╎ ╎
╎ ╰╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╯ ╎
╰╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╯

⡏⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⠉⢹
⡇ todo                                100 ⢸
⡇ ⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛ ⢸
⡇ pass                                100 ⢸
⡇ ⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛ ⢸
⡇ fail                                 21 ⢸
⡇ ⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛ ⢸
⠧⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠤⠼
```

Test results are fully interactive, so after the first failure, other tests can also be run, navigated to, etc.

Tests can be filtered using using any letters included in the test path or description. When a test fails, an exclusive-matching filter will also be printed.

Each test run has its own random seed, and each test applies a fixed transform to that seed using the test path and description. This way, when a test fails, the run's random seed can be printed and the test can be reproduced exactly.
