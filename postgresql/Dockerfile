ARG POSTGRES_VERSION

FROM postgres:$POSTGRES_VERSION

ARG PG_PERIODS_VERSION
ARG PG_IS_JSON_VALID_VERSION
ARG PG_TEMPORAL_TABLES_VERSION
ARG PG_JOBMON_VERSION

RUN POSTGRES_VERSION="$POSTGRES_VERSION"  && \
    apt-get update && \
    apt-get install -y \
        git make gcc $(for i in $POSTGRES_VERSION; do printf "postgresql-server-dev-$i "; done) && \   
        \  
    git clone -b ${PG_TEMPORAL_TABLES_VERSION}  https://github.com/arkhipov/temporal_tables.git --depth 1 && \
    cd temporal_tables && \
    for i in $POSTGRES_VERSION; do \
      if [ "$i" -le 11 ]; then \
        ln -fs  /usr/lib/postgresql/$i/bin/pg_config /usr/bin/pg_config && \
        make clean && \
        make install; \
      fi \
    done && \
    cd ../ && rm -rf temporal_tables && \
    \  
    git clone -b ${PG_IS_JSON_VALID_VERSION} https://github.com/furstenheim/is_jsonb_valid.git --depth 1 && \
    cd is_jsonb_valid && \
    for i in $POSTGRES_VERSION; do \
      ln -fs  /usr/lib/postgresql/$i/bin/pg_config /usr/bin/pg_config && \
      make clean && \
      make install; \
    done && \
    cd ../ && rm -rf is_jsonb_valid && \
    \ 
    git clone -b ${PG_PERIODS_VERSION} https://github.com/xocolatl/periods.git --depth 1 && \
    cd periods && \
    for i in $POSTGRES_VERSION; do \
      if [ "$i" -ge 13 ]; then \
        ln -fs  /usr/lib/postgresql/$i/bin/pg_config /usr/bin/pg_config && \
        make clean && \
        make install; \
      fi \
    done && \
    cd ../ && rm -rf periods && \
    \
    git clone -b ${PG_JOBMON_VERSION} https://github.com/omniti-labs/pg_jobmon.git --depth 1 && \
    cd pg_jobmon && \
    for i in $POSTGRES_VERSION; do \
      ln -fs  /usr/lib/postgresql/$i/bin/pg_config /usr/bin/pg_config && \
      make clean && \
      make install; \
    done && \
    cd ../ && rm -rf pg_jobmon && \
    \
    apt-get remove -y git make gcc $(for i in $POSTGRES_VERSION; do printf "postgresql-server-dev-$i "; done) && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

