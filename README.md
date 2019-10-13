Setup Mac OS X
==============

This gist is just a personal reference in case I need to do it all over again.

Setup
-----

### 1. Run software update

Make sure everything is up to date.

### 2. Install Xcode and/or "Command Line Tools"

```sh
xcode-select --install
```

 > NOTE: homebrew now automatically installs command line tools, so you can skip this step.

### 3. Install homebrew and other CLI tools


```sh
# install homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

brew install git
brew install git-lfs
brew install git-flow

brew install postgresql
brew install sqlite
brew install mysql
brew install redis
brew install mongodb

brew install asdf
brew install ruby-build
brew install php
brew install python

brew install tree
brew install awscli
brew install heroku
brew install yarn
brew install dnsmasq
brew install httpd
brew install zsh-syntax-highlighting
brew install httpie
```


### 4. Install softwares

#### homebrew-cask

Many softwares can be installed through
[homebrew-cask](https://github.com/phinze/homebrew-cask) which makes the
process way simpler:

```sh
# browsers
brew cask install firefox-developer-edition
brew cask install google-chrome-canary
brew cask install google-chrome
brew cask install opera

# editors
brew cask install atom-beta
brew cask install visual-studio-code-insiders
brew cask install sublime-text-dev

# dev
brew cask install unity-hub
brew cask install robo-3t
brew cask install sequel-pro
brew cask install psequel
brew cask install docker
brew cask install dotnet
brew cask install rowanj-gitx
brew cask install sourcetree
brew cask install imageoptim
brew cask install insomnia
brew cask install iterm2

# utilities
brew cask install alfred
brew cask install appcleaner
brew cask install spectacle
brew cask install quicklook-csv
brew cask install quicklook-json
brew cask install webpquicklook
brew cask install the-unarchiver
brew cask install google-backup-and-sync
brew cask install grammarly
brew cask install transmission

# general
brew cask install spotify
brew cask install steam
brew cask install vlc

# messengers
brew cask install discord
brew cask install telegram
brew cask install skype
brew cask install slack
brew cask install whatsapp

# fonts
brew cask install font-hack
brew cask install font-lato
brew cask install font-noto-sans
brew cask install font-open-sans
brew cask install font-pt-sans
brew cask install font-pt-serif
brew cask install font-roboto
brew cask install font-roboto-condensed
brew cask install font-roboto-mono
brew cask install font-roboto-slab
brew cask install font-source-sans-pro
```

### 5. Borrow a few OSX settings from [mathiasbynens dotfiles](https://github.com/mathiasbynens/dotfiles)


```sh
###############################################################################
# General UI/UX                                                               #
###############################################################################

# Disable the sound effects on boot
sudo nvram SystemAudioVolume=" "

# Menu bar: show remaining battery time (on pre-10.8); hide percentage
defaults write com.apple.menuextra.battery ShowPercent -string "NO"
defaults write com.apple.menuextra.battery ShowTime -string "YES"


###############################################################################
# Finder                                                                      #
###############################################################################

# Finder: show hidden files by default
defaults write com.apple.finder AppleShowAllFiles -bool true

# Finder: show all filename extensions
defaults write NSGlobalDomain AppleShowAllExtensions -bool true

# Finder: show status bar
defaults write com.apple.finder ShowStatusBar -bool true

# Finder: allow text selection in Quick Look
defaults write com.apple.finder QLEnableTextSelection -bool true

# Disable the warning when changing a file extension
defaults write com.apple.finder FXEnableExtensionChangeWarning -bool false

# Enable snap-to-grid for icons on the desktop and in other icon views
/usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:arrangeBy grid" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:arrangeBy grid" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:arrangeBy grid" ~/Library/Preferences/com.apple.finder.plist


###############################################################################
# Screen                                                                      #
###############################################################################

# Save screenshots to the desktop
defaults write com.apple.screencapture location -string "$HOME/Desktop"

# Save screenshots in PNG format (other options: BMP, GIF, JPG, PDF, TIFF)
defaults write com.apple.screencapture type -string "png"

# Disable shadow in screenshots
defaults write com.apple.screencapture disable-shadow -bool true


###############################################################################
# Address Book, Dashboard, iCal, TextEdit, and Disk Utility                   #
###############################################################################

# Use plain text mode for new TextEdit documents
defaults write com.apple.TextEdit RichText -int 0
# Open and save files as UTF-8 in TextEdit
defaults write com.apple.TextEdit PlainTextEncoding -int 4
defaults write com.apple.TextEdit PlainTextEncodingForWrite -int 4

###############################################################################
# Spotlight                                                                   #
###############################################################################

# Hide Spotlight tray-icon (and subsequent helper)
#sudo chmod 600 /System/Library/CoreServices/Search.bundle/Contents/MacOS/Search
# Disable Spotlight indexing for any volume that gets mounted and has not yet
# been indexed before.
# Use `sudo mdutil -i off "/Volumes/foo"` to stop indexing any volume.
sudo defaults write /.Spotlight-V100/VolumeConfiguration Exclusions -array "/Volumes"
# Change indexing order and disable some file types
defaults write com.apple.spotlight orderedItems -array \
  '{"enabled" = 1;"name" = "APPLICATIONS";}' \
  '{"enabled" = 1;"name" = "SYSTEM_PREFS";}' \
  '{"enabled" = 1;"name" = "DIRECTORIES";}' \
  '{"enabled" = 0;"name" = "PDF";}' \
  '{"enabled" = 0;"name" = "FONTS";}' \
  '{"enabled" = 0;"name" = "DOCUMENTS";}' \
  '{"enabled" = 0;"name" = "MESSAGES";}' \
  '{"enabled" = 0;"name" = "CONTACT";}' \
  '{"enabled" = 0;"name" = "EVENT_TODO";}' \
  '{"enabled" = 0;"name" = "IMAGES";}' \
  '{"enabled" = 0;"name" = "BOOKMARKS";}' \
  '{"enabled" = 0;"name" = "MUSIC";}' \
  '{"enabled" = 0;"name" = "MOVIES";}' \
  '{"enabled" = 0;"name" = "PRESENTATIONS";}' \
  '{"enabled" = 0;"name" = "SPREADSHEETS";}' \
  '{"enabled" = 0;"name" = "SOURCE";}'
# Load new settings before rebuilding the index
killall mds
# Make sure indexing is enabled for the main volume
sudo mdutil -i on /
# Rebuild the index from scratch
sudo mdutil -E /
```

source: https://github.com/mathiasbynens/dotfiles/blob/master/.macos

###  7. Create/Update `~/.gitconfig`

```gitconfig
; I removed the [user] block on purpose so other people don't copy it by mistake
; you will need to set these values
[apply]
    whitespace = fix
[color]
    ui = auto
[color "branch"]
    current = yellow reverse
    local = yellow
    remote = green
[color "diff"]
    meta = yellow bold
    frag = magenta bold
    old = red bold
    new = green bold
[color "status"]
    added = yellow
    changed = green
    untracked = cyan
[merge]
    log = true
[push]
    ; "simple" avoid headaches, specially if you use `--force` w/o specifying branch
    ; see: http://stackoverflow.com/questions/13148066/warning-push-default-is-unset-its-implicit-value-is-changing-in-git-2-0
    default = simple
[url "git://github.com/"]
    insteadOf = "github:"
[url "git@github.com:"]
    insteadOf = "gh:"
    pushInsteadOf = "github:"
    pushInsteadOf = "git://github.com/"
[url "git@github.com:millermedeiros/"]
    insteadOf = "mm:"
[url "git@github.com:mout/"]
    insteadOf = "mout:"
[core]
    excludesfile = ~/.gitignore_global
    ; setting the editor fixes git commit bug http://tooky.co.uk/2010/04/08/there-was-a-problem-with-the-editor-vi-git-on-mac-os-x.html
    editor = /usr/bin/vim
[alias]
    ; show merge tree + commits info
    graph = log --graph --date-order -C -M --pretty=format:\"<%h> %ad [%an] %Cgreen%d%Creset %s\" --all --date=short
    lg = log --graph --pretty=format:'%Cred%h%Creset %C(yellow)%an%d%Creset %s %Cgreen(%cr)%Creset' --date=relative
    ; basic logging for quick browsing
    ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cgreen\\ [%cn]" --decorate
    ll = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cgreen\\ [%cn]" --decorate --numstat
    ; log + file diff
    fl = log -u
    ; find paths that matches the string
    f = "!git ls-files | grep -i"
    ; delete all merged branches
    ; dm = !git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
    ; shortcuts
    cp = cherry-pick
    st = status -s
    cl = clone
    ci = commit
    co = checkout
    br = branch
    dc = diff --cached
```

You will need to set the user name and email (removed from .gitconfig to avoid
errors):

```sh
git config --global user.name "Your Name Here"
git config --global user.email youremail@example.com
```


### 8. Config vim

[my .vimrc is on this gist](https://gist.github.com/millermedeiros/1262085).

```sh
# create symlink to my vimrc file
ln -s ~/Dropbox/dotfiles/vimrc ~/.vimrc
# install Vundle to manage my plugins (https://github.com/VundleVim/Vundle.vim)
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```