# propeller-documentation

**propeller**  is an implementation of the Push programming language and the PushGP genetic programming system in Clojure.

For more information on Push and PushGP see http://pushlanguage.org.

# Overview

**propeller** is a Push-based genetic programming system in Clojure.

## What can you do with propeller?

You can evolve a Push program to solve a problem.

### How do you do that?

If you have installed [leiningen](https://leiningen.org), which is a tool
for running Clojure programs, then you can run Propeller on a genetic
programming problem that is defined within this project from the command
line with the command `lein run -m <namespace>`, replacing `<namespace>`
with the actual namespace that you will find at the top of the problem file.


### What is the general format of a valid command-line argument?

Each problem in propeller comes with default arguments for the `argmap`.

| Key           | Description                                                                                                                            | Argument                          |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
| `:instructions` | possible Push instructions in a plushy                                                                                                 |                                   |
| `:error-function`    | the error function used to evaluate individuals                                                                                        |                                   |
| `:training-data`   | pairs of selected inputs and desired outputs used to evaluate individuals                                                              |                                   |
| `:testing-data`      | pairs of selected inputs and desired outputs not in the training-data to test generalizability of a program that fits the training-data |                                   |
| `:max-generations`    | max number of generations                                                                                                              | integer                           |
| `:population-size`    | size of population                                                                                                                     | integer                           |
| `:max-initial-plushy-size`    | tk                                                                                                                                     | integer                           |
| `:step-limit`    | tk                                                                                                                                     | integer                           |
| `:parent-selection`    | method of parent selection                                                                                                             | :lexicase or :tournament          |
| `:tournament-size`    | if using a tournament method, the size of the tournament                                                                               | integer less than population-size |
| `:umad-rate`     | Text                                                                                                                                   |                                   |
| `:variation`     | Text                                                                                                                                   |                                   |
| `:elitism`      | Text                                                                                                                                   | true or false                     |

When running problems through the command-line, you'll only want to specify the following:
- `:max-generations`
- `:population-size`
- `:max-initial-plushy-size`
- `:step-limit`
- `:parent-selection`
- `:tournament-size`
- `:umad-rate`
- `:variation`
- `:elitism`

General format to run a problem with specifications:
```
lein run -m [path of the problem file you want to test] [key and argument] [key and argument]...
```

#### An Example

For example, you can run the simple-regression genetic programming problem with:

```
lein run -m propeller.problems.simple-regression
```

Additional command-line arguments may
be provided to override the default key/value pairs specified in the
problem file, for example:


```
lein run -m propeller.problems.simple-regression :population-size 100
```

On Unix operating systems, including MacOS, you can use something
like the following to send output both to the terminal
and to a text file (called `outfile` in this example):

```
lein run -m propeller.problems.simple-regression | tee outfile
```

If you want to provide command line arguments that include
characters that may be interpreted by your command line shell
before they get to Clojure, then enclose those in double
quotes, like in this example that provides a non-default
value for the `:variation` argument, which is a clojure map
containing curly brackets that may confuse your shell:

```
lein run -m propeller.problems.simple-regression :variation "{:umad 1.0}"
```

{:instructions            instructions
:error-function          error-function
:training-data           (:train train-and-test-data)
:testing-data            (:test train-and-test-data)
:max-generations         300
:population-size         1000
:max-initial-plushy-size 250
:step-limit              2000
:parent-selection        :lexicase
:tournament-size         5
:umad-rate               0.1
:variation               {:umad 1.0 :crossover 0.0}
:elitism                 false}

### Can you use a REPL?

Yes!

To run a genetic programming problem from a REPL, start
your REPL for the project (e.g. with `lein repl` at the
command line when in the project directory, or through your
IDE) and then do something like the following (which in
this case runs the simple-regression problem with
`:population-size` 100):

```
(require 'propeller.problems.simple-regression)
(in-ns 'propeller.problems.simple-regression)
(-main :population-size 100 :variation {:umad 1.0})
```

If you want to run the problem with the default parameters,
then you should call `-main` without arguments, as `(-main).

# Tutorials

- Adding Genetic Operators
- Adding selection methods
- Adding a new problem

# Contributing