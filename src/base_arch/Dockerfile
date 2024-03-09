FROM archlinux:latest

ARG USER_NAME="code"
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Update system
RUN pacman -Syyu --noconfirm

# Install basic package
RUN pacman -Sy --needed \ 
  base-devel \
  git \
  curl \
  wget \
  zsh \
  ripgrep \
  fd \
  vim \
  neovim \
  starship \
  lazygit \
  --noconfirm

# Add user
RUN groupadd --gid ${USER_GID} ${USER_NAME} && \
  useradd --uid ${USER_UID} --gid ${USER_GID} -s /usr/bin/zsh -m ${USER_NAME} && \
  echo "${USER_NAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USER_NAME} && \
  chmod 0440 /etc/sudoers.d/${USER_NAME}

# Switch user to {USER_NAME}
USER ${USER_NAME}
WORKDIR /home/${USER_NAME}

RUN git clone https://aur.archlinux.org/yay-bin.git
RUN cd yay-bin/ && \
  makepkg -si --noconfirm

RUN yay -Y --gendb && \
  yay -Syu --devel && \
  yay -Y --devel --save

# Set shell environment
RUN git clone https://github.com/Ccccraz/.dotfiles.git
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/zsh-syntax-highlighting

RUN ln -s ~/.dotfiles/shell/zsh/.zshrc ~/.zshrc
RUN ln -s ~/.dotfiles/shell/starship.toml ~/.config/starship.toml