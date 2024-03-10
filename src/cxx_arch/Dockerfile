FROM ccccr/container:basearch

RUN yay -Sy --needed \
    xmake \
    cmake \
    llvm \
    clang \
    --noconfirm

RUN xrepo install -y fmt \
    boost