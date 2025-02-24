# Phillip's dotfiles

Initially copied from [Andre Azzolini](https://github.com/apazzolini/dotfiles) who copied his from [Zach Holman](https://github.com/holman/dotfiles), but 
substantially stripped down for my particular tastes. This used to also 
utilize oh-my-zsh, but I've found that I'd rather manage my entire 
configuration by myself, so this no longer requires that.

## Setup a new machine

- Install [iTerm](https://iterm2.com/)
- Install [Homebrew](https://brew.sh/)
- Install a JVM from https://adoptopenjdk.net/ (last 3 LTS versions)
- `brew install autojump autoconf awscli bzip2 ca-certificates cffi cmake coreutils curl gcc gettext git git-lfs glib gnu-time grc grep hub jq libgpg-error libtool libuv lz4 mongosh ncdu nvm pinentry pinentry-mac poetry pyenv rbenv ruby-build rsync tfenv tree uv vim wget yq zsh`
- `chsh -s /bin/zsh`
- Copy SSH key from Bitwarden to ~/.ssh/id_rsa and set correct chmod permissions `chmod 600 ~/.ssh/id_rsa`
- `git clone git@github.com:phillipuniverse/dotfiles ~/.dotfiles`
- `cd ~/.dotfiles`
- `rake install`
- Add the iTerm2 shell integration `curl -L https://iterm2.com/shell_integration/zsh -o ~/.iterm2_shell_integration.zsh`
- Copy in zsh_history from known location `#TODO: decide on long term storage` to `~/.zsh_history`

The install rake task will symlink the appropriate files in `.dotfiles` to your
home directory. Everything is configured and tweaked within `~/.dotfiles`,
though.

You should also go and modify `~/.dotfiles/git/gitconfig.symlink` and change that to your own information and not mine.

### Automatic git GPG Signing

Original instructions [here](https://gist.github.com/bmhatfield/cc21ec0a3a2df963bffa3c1f884b676b#file-setup-gpg), some modifications made to work with this setup. 

1. Install reqs
  ```console
  brew install gnupg pinentry-mac
  ```

2. Create `~/.gnupg/gpg-agent.conf` with `mkdir ~/.gnupg && vim gpg-agent.conf`:

```
# Enables GPG to find gpg-agent
use-standard-socket

# Connects gpg-agent to the OSX keychain via the brew-installed
# pinentry program from GPGtools. This is the OSX 'magic sauce',
# allowing the gpg key's passphrase to be stored in the login
# keychain, enabling automatic key signing.
pinentry-program /usr/local/bin/pinentry-mac
```

3. Create `~/.gnupg/gpg.conf`:

```
use-agent

# This silences the "you need a passphrase" message once the passphrase handling is all set.
# Use at your own discretion - may prevent the successful interactive use of some operations.
# It is working fine for my use cases though.
batch
```

4. Install GPG Suite from https://gpgtools.org
5. Open GPG Suite, find the GPG private key from the secure location and copy to clipboard. GPG Suite will prompt to automatically import the key

## Items of note <Section blatantly ripped off>

There's a few special files in the hierarchy.

- **bin/**: Anything in `bin/` will get added to your `$PATH` and be made
  available everywhere.
- **topic/\*.zsh**: Any files ending in `.zsh` get loaded into your
  environment.
- **topic/\*.symlink**: Any files ending in `*.symlink` get symlinked into
  your `$HOME`. This is so you can keep all of those versioned in your dotfiles
  but still keep those autoloaded files in your home directory. These get
  symlinked in when you run `rake install`.
- **topic/\*.completion.sh**: Any files ending in `completion.sh` get loaded
  last so that they get loaded after we set up zsh autocomplete functions.

## Cool things these let you do

See current status when you're in a Git repository (* indicates uncommitted changes):
![gitline](http://f.cl.ly/items/302c0v3j0v0N2D0l2v44/Screen%20Shot%202015-01-28%20at%209.56.16%20PM.png)

Git aliases like `gist` for `git status` and `git hist` to replace `git log`:
![gitalias](http://cl.ly/image/2t2j0t0T3r3z/Screen%20Shot%202015-01-28%20at%209.59.15%20PM.png)

Quickly switch between versions of Java (auto-selects the latest minor version of 1.6, 1.7 and 1.8) with `usejava6`, `usejava7`, `usejava8`:
![java](http://cl.ly/image/3L0M0m1V3B2r/Screen%20Shot%202015-01-28%20at%2010.07.47%20PM.png)

[Jump around with `j`](https://github.com/joelthelion/autojump)

## Private items

Items that are in `private/` will not get committed into git should you choose to share your repo.
Files inside that end in .zsh or .symlink will still function however.

Also, `git/gitconfig.symlink` is set to be ignored as well, and I recommend you move your private
`~/.gitconfig` into `git/gitconfig.symlink` for consistency.

## Credit

Thanks to [Zach Holman](http://github.com/holman/dotfiles) and the [corresponding blog post](http://zachholman.com/2010/08/dotfiles-are-meant-to-be-forked/). Seriously, go check
out his repository and theory on dotfiles. I agree with all of it, and would
never have created this without seeing his first.
