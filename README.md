# Handmade Hero Makefiles

Some Makefiles that automate the building process of Handmade Hero in
Linux (they probably work for Windows or macOS with minor modifications).

A git worktree is created for each tagged day in the sdl repository,
then some operations are applied to facilitate the compilation
process.

# Requirements
- Handmade Hero sdl and cpp repositories.
- Handmade Hero assets (to be able to run Handmade Hero).
- SDL2.The provided library is broken for days earlier than ~200.
  - It has some hard coded paths.

# Usage

Organize all the repositories in the same directory as the Makefile.

- cpp 
- sdl 
- sources 
- Makefile

Then just call make and the desired day (only some of the days are
tagged in the sdl repository and thus available for compilation). 

``` console
make day657
```

To delete a day.

``` console
make rm day=657
```

A guix manifest is included with the basic requirements for
compilation (SDL and GCC). To use it just call guix shell.

```console
guix shell 
```
