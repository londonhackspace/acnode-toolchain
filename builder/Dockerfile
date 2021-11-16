FROM ubuntu:20.04

ENV DEBIAN_FRONTEND="noninteractive"
ENV TZ=Europe/London
ENV CTNG_VER="c55c826dc09c490fbb9463d52a5450d3635ff456"

RUN apt-get update && \
	apt-get install -y build-essential \
		git \
		libtool-bin \
		gawk \
		autoconf \
		texinfo \
		flex \
		bison \
		ncurses-dev \
		unzip \
		help2man \
		wget \
		curl \
	&& rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
	&& apt-get update \
	&& apt-get -y install gh \
	&& rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/crosstool-ng/crosstool-ng.git \
	&& cd crosstool-ng \
	&& git reset --hard $CTNG_VER \
	&& ./bootstrap \
	&& ./configure \
	&& make -j \
	&& make install \
	&& cd .. \
	&& rm -rf crosstool-ng

RUN useradd -m builder

USER builder


