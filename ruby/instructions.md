# Ruby installation

This guide installs **rbenv** with common plugins, system libraries needed to build Ruby from source, and **Rust** (for **YJIT**). It matches how this dotfiles repo expects Ruby to be set up: `PATH` includes `~/.rbenv` from `zshenv`, and interactive shells run `rbenv init` from `zshrc`.

## 1. System packages (Debian / Ubuntu)

Build tools and libraries Ruby and gems often need:

```bash
sudo apt update
sudo apt -y install \
  autoconf automake patch \
  libbz2-dev libffi-dev libgdbm-dev libjemalloc-dev libncurses-dev \
  libpq-dev libreadline-dev libsqlite3-dev libssl-dev libvips-dev \
  libxml2-dev libyaml-dev zlib1g-dev
```

## 2. Rust (YJIT)

YJIT is enabled below via `RUBY_CONFIGURE_OPTS=--enable-yjit`. Install Rust with the official installer (or your preferred method); a new shell will pick up `~/.cargo/bin` if you use this repo’s `zshenv`.

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## 3. rbenv and plugins

Clone rbenv and plugins into fixed paths so this works even before `rbenv` is on your `PATH`:

```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
mkdir -p ~/.rbenv/plugins
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
git clone https://github.com/rbenv/rbenv-vars.git ~/.rbenv/plugins/rbenv-vars
git clone https://github.com/rkh/rbenv-update.git ~/.rbenv/plugins/rbenv-update
```

Ensure your shell loads rbenv (this repo already does via `~/.zshenv` and `~/.zshrc`). In a new terminal:

```bash
command -v rbenv   # should print a path under ~/.rbenv/bin
rbenv doctor       # optional sanity check
```

Refresh the list of installable Ruby versions after cloning or updating `ruby-build`:

```bash
rbenv update
```

## 4. Install Ruby

Pick a version (see `rbenv install -l`). Example with **jemalloc** and **YJIT**:

```bash
RUBY_CONFIGURE_OPTS="--with-jemalloc --enable-yjit" rbenv install 4.0.2
rbenv global 4.0.2   # or rbenv local 4.0.2 per project
```

## 5. Verify

```bash
ruby -v
which ruby   # should be under ~/.rbenv/shims
```

---

If `rbenv install` fails, install any extra packages the error mentions, run `rbenv update`, and try again.
