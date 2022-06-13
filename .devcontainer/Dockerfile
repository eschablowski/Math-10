# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.202.5/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version (use hirsuite or bionic on local arm64/Apple Silicon): hirsute, focal, bionic
ARG VARIANT="hirsute"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN mkdir /texlive && chown vscode /texlive

USER vscode
COPY texlive.profile /tmp/texlive-profile
# [Optional] Uncomment this section to install additional OS packages.
RUN cd /tmp && sudo apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && sudo apt-get -y install --no-install-recommends wget libyaml-tiny-perl libfile-homedir-perl libunicode-linebreak-perl \
    && wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
    && tar -xf install-tl-unx.tar.gz \
    && cd install-tl-* \
    && ./install-tl --profile=/tmp/texlive-profile

COPY texlive-paths.sh /etc/profile.d/texlive.sh
RUN /texlive/bin/x86_64-linux/tlmgr update --self && /texlive/bin/x86_64-linux/tlmgr install fancyhdr zref comment environ mdframed needspace enumitem latexmk latexindent exam babel asymptote
