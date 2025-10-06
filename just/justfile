### BOOTC
bootc-upgrade:
    #!/bin/bash
    bootc upgrade --quiet

bootc-upgrade-reboot:
    #!/bin/bash
    bootc upgrade --apply --quiet

### FLATPAK
flatpak-setup:
    #!/bin/bash
    flatpak remote-delete --force fedora
    flatpak remote-delete --force fedora-testing
    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

flatpak-update:
    #!/bin/bash
    flatpak update -y --noninteractive
    flatpak remove -y --noninteractive --unused

flatpak-packages:
    #!/bin/bash
    pwd
    FLATPAK_LIST="$(curl https://github.com/emblem-66/Linux-Stuff/blob/main/flatpak/packages | tr '\n' ' ')"
    flatpak --system -y --noninteractive install ${FLATPAK_LIST}
    FLATPAK_LIST="$(cat ~/.flatpak-packages | tr '\n' ' ')"
    flatpak --system -y --noninteractive install ${FLATPAK_LIST}

### HOMEBREW
homebrew-setup:
    #!/bin/bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    #curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh | bash
    [[ -d /home/linuxbrew/.linuxbrew && $- == *i* ]] && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
    # Universal Blue workaround
    # https://www.ypsidanger.com/homebrew-is-great-on-linux/
    # https://github.com/ublue-os/config/blob/main/build/ublue-os-just/etc-profile.d/brew.sh?ref=ypsidanger.com
    #[[ -d /home/linuxbrew/.linuxbrew && $- == *i* ]] && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

homebrew-update:
    #!/bin/bash
    brew update
    brew upgrade

homebrew-packages:
    #!/bin/bash
    BREW_LIST="$(curl https://github.com/emblem-66/Linux-Stuff/blob/main/brew/packages | tr '\n' ' ')"
    brew install ${BREW_LIST}
    BREW_LIST="$(cat ~/.brew-packages | tr '\n' ' ')"
    brew install ${BREW_LIST}
