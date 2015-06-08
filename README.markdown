# Phillip's dotfiles

Initially copied from [Andre Azzolini](https://github.com/apazzolini/dotfiles) who copied his from [Zach Holman](https://github.com/holman/dotfiles), but 
substantially stripped down for my particular tastes. This used to also 
utilize oh-my-zsh, but I've found that I'd rather manage my entire 
configuration by myself, so this no longer requires that.

## Usage

Similar steps as Holman's:

- `git clone git://github.com/phillipuniverse/dotfiles ~/.dotfiles`
- `brew install rbenv`
- `brew install autojump`
- `brew install coreutils`
- `brew install hub`
- `cd ~/.dotfiles`
- `rake install`
- `brew install grc` (optional, will add color to a few utilities)
- `chsh -s /bin/zsh` (make sure this path exists on your machine or you're gonna have a bad time)

The install rake task will symlink the appropriate files in `.dotfiles` to your
home directory. Everything is configured and tweaked within `~/.dotfiles`,
though.

You should also go and modify `~/.dotfiles/git/gitconfig.symlink` and change that to your own information and not mine.

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
