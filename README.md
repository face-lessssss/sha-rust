# sha-rust

A high-performance Rust library for hash verification and file pattern matching.

## Features

- 🔍 **Pattern Matching**: Efficient hash name pattern matching with flexible wildcard support
- ✅ **Hash Verification**: Verify file hashes against remote API endpoints
- 🚀 **Async Support**: Built with modern Rust async/await patterns
- 🔒 **Type Safe**: Leverages Rust's type system for safety and performance

## Installation

Add this to your `Cargo.toml`:

```toml
[dependencies]
sha-rust = "0.1.0"
```

Or use it directly from git:

```toml
[dependencies]
sha-rust = { git = "https://github.com/radioman/sha-rust" }
```

# Translation Overview

The translation task is fully parallelized. Given a topological sort on the dependency order of crates, the remainder may be solved (roughly) with the following algorithm:

```rust

workspace.compile()?;

let topo_sorted_crates = workspace.crates().topo_sort();

for crate in topo_sorted_crates.iter() {

  let dep_interfaces: Vec<InterfaceText> = crate.dependencies().iter().map(|dep| dep.interface_text()).collect();

  for source_file in crate.source_files() {
    for func in source_file.untranslated_functions() {
      translate_function_given_interfaces(func,dep_interfaces)?;
      workspace.compile()?;
      create_git_commit_for_function(func.name())?;
    }
  }
  create_git_commit_for_crate(crate.name())?;
  crate.run_tests()?;
}
// now we can patch until we reach the C++ head, etc.
```

The [Chomper transpiler](https://github.com/radioman/sha-rust) is used to help expedite the general task of C++ to Rust translation.

The `translate_function_given_interfaces` step seems best done with AI in the loop, given the fact that the function body logic itself has already been developed.

It is a good idea to allow the models to scale to solve this specific translation problem downstream with more computer power.
Go to where the bottleneck is.

This codebase is currently available for experimentation, education, and development collaboration.

Here are some things which are helpful:
- pull requests completing (and testing) the translation of one or more of these crates.
- requests to distribute one or more crates in this workspace. 

If there are developers out there who are interested in collaborating in the meantime as the AI scales, support will be provided.

Best,

- radioman