FROM fedora:27

RUN dnf update -y
RUN dnf install -y \
    ack \
    bash-completion \
    bindfs \
    @'C Development Tools and Libraries' \
    ctags \
    @'Development Tools' \
    fedpkg \
    fedora-packager \
    fzf \
    gcc-c++ \
    gnupg \
    hostname \
    hub \
    inotify-tools \
    jq \
    krb5-devel \
    koji-utils \
    man-db \
    mc \
    neovim \
    npm \
    powerline \
    quilt \
    procps-ng \
    redhat-rpm-config \
    rpm-build \
    @'RPM Development Tools' \
    rpmspectool \
    ruby-devel \
    rubygems \
    skopeo \
    sssd-client \
    sudo \
    the_silver_searcher \
    tmux \
    tmux-powerline \
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

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'
# https://jhrozek.wordpress.com/2015/03/31/authenticating-a-docker-container-against-hosts-unix-accounts/
# COPY sss_test /etc/pam.d/sss_test

COPY krb5.conf /etc/krb5.conf

# do not require password for sudo
RUN echo "miminar ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/miminar
RUN useradd -u 1000 -g users -G users,wheel miminar
USER miminar
WORKDIR /home/miminar
VOLUME /home/miminar/.gnupg
RUN mkdir -p ~/.ssh/sockets
RUN git clone git://fedorapeople.org/~miminar/rcs.git .rcs
RUN pushd .rcs; ./setup -n; git submodule update --init --recursive; popd
RUN pushd .rcs; git remote set-url origin fedorapeople.org:public_git/rcs.git; popd
RUN nvim '+GoInstallBinaries' '+qall' ||:
RUN mkdir -p .config/mc; printf '[Midnight-Commander]\nskin=darkfar\nuse_internal_edit=false\n' >.config/mc/ini
RUN printf '%s\n' \
    'export PATH="'"${WSP}"'/_output/local/bin/linux/amd64:${PATH}"' \
    'export LC_ALL=C' \
    >>~/.bash_overrides
CMD /bin/bash
