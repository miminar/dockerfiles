FROM fedora:25

RUN dnf update -y
RUN dnf install -y \
    ack \
    @'C Development Tools and Libraries' \
    ctags \
    @'Development Tools' \
    fedpkg \
    fedora-packager \
    gcc-c++ \
    koji-utils \
    man-db \
    mc \
    powerline \
    redhat-rpm-config \
    rpm-build \
    @'RPM Development Tools' \
    rpmspectool \
    ruby-devel \
    rubygems \
    sssd-client \
    sudo \
    tmux \
    tmux-powerline \
    vim-enhanced \
    xz

# wt build dependencies
RUN dnf install -y \
    GraphicsMagick-devel \
    boost-devel \
    cmake \
    fcgi-devel \
    glew-devel \
    libharu-devel \
    mysql-devel \
    openssl-devel \
    pango-devel \
    postgresql-devel \
    qt-devel \
    sqlite-devel \
    zlib-devel

# https://jhrozek.wordpress.com/2015/03/31/authenticating-a-docker-container-against-hosts-unix-accounts/
COPY sss_test /etc/pam.d/sss_test

# do not require password for sudo
RUN echo "miminar ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/miminar
RUN useradd miminar
USER miminar
WORKDIR /home/miminar
RUN git clone git://fedorapeople.org/~miminar/rcs.git .rcs
RUN git clone git://fedorapeople.org/~miminar/vim.git .vim
RUN pushd .rcs; ./make-links -n; git submodule update --init --recursive; popd; pushd .vim; ./update-plugins; popd
RUN mkdir -p .config/mc; printf '[Midnight-Commander]\nskin=darkfar\nuse_internal_edit=false\n' >.config/mc/ini
CMD /bin/bash
