FROM ubuntu:24.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update -y &&  \
DEBIAN_FRONTEND=noninteractive apt-get install -q -y \
build-essential  cmake texinfo automake autoconf libtool git vim ssh zsh bash curl
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
