FROM sourcelevel/erllambda:24.2

ARG ELIXIR_VERSION=1.12.3

ENV LANG=en_US.UTF-8 \
        LANGUAGE=en_US.UTF-8 \
        LC_ALL=en_US.UTF-8

ENV MIX_REBAR3=/usr/local/bin/rebar3
ENV MIX_REBAR=/usr/local/bin/rebar

RUN set -xe \
        && ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/v${ELIXIR_VERSION}.tar.gz" \
        && ELIXIR_DOWNLOAD_SHA256=c5affa97defafa1fd89c81656464d61da8f76ccfec2ea80c8a528decd5cb04ad \
        && curl -fsSL $ELIXIR_DOWNLOAD_URL -o elixir-src.tar.gz \
        && echo "$ELIXIR_DOWNLOAD_SHA256 elixir-src.tar.gz" | sha256sum -c - \
        && mkdir -p /usr/src/elixir-src \
        && tar -xzf elixir-src.tar.gz -C /usr/src/elixir-src --strip-components=1 \
        && rm elixir-src.tar.gz \
        && cd /usr/src/elixir-src \
        && make -j$(nproc) \
        && make install \
        && rm -rf /usr/src/elixir-src \
        && cd $HOME \
        && mix local.hex --force \
        && mix hex.info

CMD ["iex"]

