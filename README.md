# Rust (Cheat Sheet)

## Installation

Official instructions: [rust-lang.org/tools/install](https://www.rust-lang.org/tools/install).

From [exercism](https://exercism.org/docs/tracks/rust/installation):

> To get the recommended installation instructions for your platform, head over
> to [the official Rust website](https://www.rust-lang.org/tools/install).
>
> Having the toolchain installed is not everything! IDE support is a huge productivity boost that
> most developers have come to expect. If you are using Visual Studio Code, check out
> its [documentation for Rust support](https://code.visualstudio.com/docs/languages/rust). We also
> recommend you whole-heartedly to
> enable [linting with clippy](https://code.visualstudio.com/docs/languages/rust#_linting)!

```sh
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /Users/arthur/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory is located at:

  /Users/arthur/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /Users/arthur/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /Users/arthur/.profile
  /Users/arthur/.zshenv

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.
```

### Check version

Source: [VS Code docs](https://code.visualstudio.com/docs/languages/rust#_check-your-installation)

After installing Rust, you can check that everything is installed correctly by opening a new
terminal/Command Prompt, and typing:

```sh
$ rustc --version
rustc 1.78.0 (9b00956e5 2024-04-29)
```

### Update version

Source: [VS Code docs](https://code.visualstudio.com/docs/languages/rust#_check-your-installation)

You can keep your Rust installation up to date with the latest version by running:

```sh
$ rustup update
```

There are new stable versions of Rust published every 6 weeks so this is a good habit.

### Local docs

Source: [VS Code docs](https://code.visualstudio.com/docs/languages/rust#_local-rust-documentation)

```sh
$ rustup doc
```

When you install Rust, you also get the full Rust documentation set locally installed on your
machine, which you can review by typing `rustup doc`. The Rust documentation,
including [The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html) and [The Cargo Book](https://doc.rust-lang.org/stable/cargo/),
will open in your local browser so you can continue your Rust journey while offline.

## Cargo

When you install Rust with rustup, the toolset includes the rustc compiler, the rustfmt source code
formatter, and the clippy Rust linter. You also get [Cargo](https://doc.rust-lang.org/cargo), the
Rust package manager, to help download Rust dependencies and build and run Rust programs. You'll
find that you end up using `cargo` for just about everything when working with Rust.

### `cargo new`

Source: [VS Code codes > `cargo new`](https://code.visualstudio.com/docs/languages/rust#_cargo-new)

A good way to create your first Rust program is to use Cargo to scaffold a new project by
typing `cargo new`. This will create a simple Hello World program along with a
default `Cargo.toml` dependency file. You pass `cargo new` the folder where you'd like to create the
project.

Let's create Hello World. Navigate to a folder where you'd like to create your project and type:

```sh
cargo new hello_world
```

To open your new project in VS Code, navigate into the new folder and launch VS Code via `code .`:

```sh
cd hello_world
code .
```

`cargo new` creates a simple Hello World project with a `main.rs` source code file
and `Cargo.toml` [Cargo manifest](https://doc.rust-lang.org/cargo/reference/manifest.html) file.

```
src\
    main.rs
.gitignore
Cargo.toml
```

`main.rs` has the program's entry function `main()` and prints "Hello, world!" to the console
using `println!`.

```sh
fnmain() {
  println!("Hello, world!");
}
```

This simple Hello World program doesn't have any dependencies but you would add Rust package (crate)
references under `[dependencies]`.

### `cargo build`

Source:
[VS Code codes > `cargo build`](https://code.visualstudio.com/docs/languages/rust#_cargo-build)

Cargo can be used to build your Rust project. Open a new terminal, navigate to your project, and
type `cargo build`.

```sh
cargo build
```

You will now have `target\debug` folder with build output include an executable
called `hello_world.exe`.

### `cargo run`

Source:
[VS Code codes > Running Hello World](https://code.visualstudio.com/docs/languages/rust#_running-hello-world)

Cargo can also be used to run your Rust project via `cargo run`.

```sh
cargo run
```

You can also run `hello_world.exe` manually in the terminal by typing `.\target\debug\hello_world`.

## rust-analyzer

### Bug: "rust-analyzer failed to discover workspace"

Source:
[stackoverflow.com](https://stackoverflow.com/questions/72062935/rust-analyzer-failed-to-discover-workspace-in-vscode)

The rust-analyzer needs a `Cargo.toml` to detect the workspace.

Solutions:

1.  Add a `Cargo.toml` in root directory with

    ```toml
    [workspace]

    members = [
        "{{root_directory}}/{{directory}}",
    ]
    ```

2.  Specify `rust-analyzer.linkedProjects` in VS Code.

    ```json
    "rust-analyzer.linkedProjects": [ "{absolute_path}/Cargo.toml" ]
    ```

3.  Open the rust project instead of the parent directory.
