FROM ccccr/dev_container_base_arch:latest

RUN yay -Sy --needed \
    xmake \
    cmake \
    llvm \
    clang \
    --noconfirm

RUN xrepo install -y fmt \
    boost