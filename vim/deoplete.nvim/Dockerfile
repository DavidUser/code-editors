FROM fedora:latest

RUN dnf install -y vim

#Pathogen
RUN echo 'execute pathogen#infect() ' >> ~/.vimrc ; \
    echo 'syntax on                 ' >> ~/.vimrc ; \
    echo 'filetype plugin indent on ' >> ~/.vimrc
RUN dnf install -y curl
RUN mkdir -p ~/.vim/autoload ~/.vim/bundle; \
    curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim;

# deoplete.vim
RUN dnf install -y clang python3 python3-pip python3-neovim;
RUN yes | pip3 install neovim pynvim
RUN dnf install -y git
RUN cd ~/.vim/bundle; \
    git clone --recursive --depth=1 --branch=master https://github.com/roxma/nvim-yarp.git; \
    git clone --recursive --depth=1 --branch=master https://github.com/roxma/vim-hug-neovim-rpc.git; \
    git clone --recursive --depth=1 --branch=master https://github.com/Shougo/deoplete.nvim.git; \
    git clone --recursive --depth=1 --branch=master https://github.com/Shougo/deoplete-clangx.git
RUN echo 'let g:deoplete#enable_at_startup = 1' >> ~/.vimrc

# Run as a common user
ARG USER
RUN adduser $USER; usermod -a -G root $USER
WORKDIR /home/$USER
RUN ln -s /root/.vim
RUN ln -s /root/.vimrc
USER $USER
