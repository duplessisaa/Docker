from ubuntu:latest

RUN apt update && apt install wget ca-certificates -y --no-install-recommends

RUN apt install perl -y --no-install-recommends

RUN cpan Pod::Usage

RUN wget -qO- "https://yihui.name/gh/tinytex/tools/install-unx.sh" | sh

ENV PATH="/root/.TinyTeX/bin/x86_64-linux/:$PATH"

RUN tlmgr install beamer translator enumitem makecell type1cm fp adjustbox collectbox subfig wrapfig multirow

RUN tlmgr install babel-english

WORKDIR /data
VOLUME ["/data"]
