FROM --platform=linux/amd64 mcr.microsoft.com/devcontainers/base:ubuntu

COPY .devcontainer/apt-packages.txt /tmp/apt-packages.txt

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && grep -v '^#' /tmp/apt-packages.txt | grep -v '^$' | xargs apt-get -y install --no-install-recommends \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/* \
    && rm /tmp/apt-packages.txt

RUN ln -s /usr/bin/python3 /usr/local/bin/python

RUN rm -f /usr/lib/python*/EXTERNALLY-MANAGED

# Copy requirements.txt if it exists and install dependencies
COPY requirements.txt* /tmp/pip-tmp/
RUN if [ -f /tmp/pip-tmp/requirements.txt ] && [ -s /tmp/pip-tmp/requirements.txt ]; then \
        python3 -m pip --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt; \
    fi \
    && rm -rf /tmp/pip-tmp

ENV PYTHONPATH=/workspaces
ENV PYTHONUNBUFFERED=1
ENV PATH="/usr/local/bin:${PATH}"

RUN echo '# Custom prompt and aliases' >> /etc/bash.bashrc && \
    echo 'git_prompt() { git rev-parse --is-inside-work-tree >/dev/null 2>&1 || return 0; local branch; branch=$(git symbolic-ref --short HEAD 2>/dev/null || git rev-parse --short HEAD 2>/dev/null); local dirty=""; if ! git diff --no-ext-diff --quiet --exit-code 2>/dev/null || [ -n "$(git ls-files --others --exclude-standard 2>/dev/null)" ]; then dirty=" \e[97mx\e[0m"; fi; printf "\e[0;31m—\e[0;31m[\e[0;33m%s\e[0m%s\e[0;31m]\e[0m" "$branch" "$dirty"; }' >> /etc/bash.bashrc && \
    echo 'export PS1="\[\e[0;31m\]┌─[\[\e[0;31m\]\u\[\e[0;33m\]@\[\e[0;36m\]\h\[\e[0;31m\]]─[\[\e[2;32m\]\w\[\e[0;31m\]]\$(git_prompt)\[\e[0;31m\]—\[\e[0;31m\][\[\e[36m\]\$(date -u +\"%a %b %d\")\[\e[0;31m\]]\[\e[0;31m\]—\[\e[0;31m\][\[\e[36m\]\$(date -u +\"%I:%M:%S %p UTC\")\[\e[0;31m\]]\[\e[0;31m\]—\[\e[0;31m\][\[\e[36m\]\$(date -u +\"%Y\")\[\e[0;31m\]]\n\[\e[0;31m\]└─[\[\e[0;33m\]>\[\e[0;31m\]]\[\e[0m\] "' >> /etc/bash.bashrc && \
    echo 'if command -v dircolors >/dev/null 2>&1; then eval "$(dircolors -b)"; fi' >> /etc/bash.bashrc && \
    echo 'alias update="sudo apt update && sudo apt upgrade -y"' >> /etc/bash.bashrc && \
    echo 'alias ls="ls -ap"' >> /etc/bash.bashrc && \
    echo 'alias ll="ls -alF --group-directories-first -h --color=auto"' >> /etc/bash.bashrc && \
    echo 'alias la="ls -A --group-directories-first -h --color=auto"' >> /etc/bash.bashrc && \
    echo 'alias lt="ls -alF --sort=time --group-directories-first -h --color=auto"' >> /etc/bash.bashrc && \
    echo 'alias lS="ls -alF --sort=size --group-directories-first -h --color=auto"' >> /etc/bash.bashrc && \
    echo 'alias lx="ls -alF --sort=extension --group-directories-first -h --color=auto"' >> /etc/bash.bashrc && \
    echo 'function cd { builtin cd "$@" && ls -ap; }' >> /etc/bash.bashrc && \
    echo 'force_color_prompt=yes' >> /etc/bash.bashrc

USER vscode

RUN echo '# Custom prompt and aliases' >> ~/.bashrc && \
    echo 'git_prompt() { git rev-parse --is-inside-work-tree >/dev/null 2>&1 || return 0; local branch; branch=$(git symbolic-ref --short HEAD 2>/dev/null || git rev-parse --short HEAD 2>/dev/null); local dirty=""; if ! git diff --no-ext-diff --quiet --exit-code 2>/dev/null || [ -n "$(git ls-files --others --exclude-standard 2>/dev/null)" ]; then dirty=" \e[97mx\e[0m"; fi; printf "\e[0;31m—\e[0;31m[\e[0;33m%s\e[0m%s\e[0;31m]\e[0m" "$branch" "$dirty"; }' >> ~/.bashrc && \
    echo 'export PS1="\[\e[0;31m\]┌─[\[\e[0;31m\]\u\[\e[0;33m\]@\[\e[0;36m\]\h\[\e[0;31m\]]─[\[\e[2;32m\]\w\[\e[0;31m\]]\$(git_prompt)\[\e[0;31m\]—\[\e[0;31m\][\[\e[36m\]\$(date -u +\"%a %b %d\")\[\e[0;31m\]]\[\e[0;31m\]—\[\e[0;31m\][\[\e[36m\]\$(date -u +\"%I:%M:%S %p UTC\")\[\e[0;31m\]]\[\e[0;31m\]—\[\e[0;31m\][\[\e[36m\]\$(date -u +\"%Y\")\[\e[0;31m\]]\n\[\e[0;31m\]└─[\[\e[0;33m\]>\[\e[0;31m\]]\[\e[0m\] "' >> ~/.bashrc && \
    echo 'if command -v dircolors >/dev/null 2>&1; then eval "$(dircolors -b)"; fi' >> ~/.bashrc && \
    echo 'alias update="sudo apt update && sudo apt upgrade -y"' >> ~/.bashrc && \
    echo 'alias ls="ls -ap"' >> ~/.bashrc && \
    echo 'alias ll="ls -alF --group-directories-first -h --color=auto"' >> ~/.bashrc && \
    echo 'alias la="ls -A --group-directories-first -h --color=auto"' >> ~/.bashrc && \
    echo 'alias lt="ls -alF --sort=time --group-directories-first -h --color=auto"' >> ~/.bashrc && \
    echo 'alias lS="ls -alF --sort=size --group-directories-first -h --color=auto"' >> ~/.bashrc && \
    echo 'alias lx="ls -alF --sort=extension --group-directories-first -h --color=auto"' >> ~/.bashrc && \
    echo 'function cd { builtin cd "$@" && ls -ap; }' >> ~/.bashrc && \
    echo 'force_color_prompt=yes' >> ~/.bashrc