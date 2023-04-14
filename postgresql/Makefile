POSTGRES_VERSION=15.2

all:
	docker build . --tag octaspace/postgresql:${POSTGRES_VERSION} \
		--build-arg POSTGRES_VERSION=${POSTGRES_VERSION} \
		--build-arg PG_PERIODS_VERSION=v1.2.2 \
		--build-arg PG_IS_JSON_VALID_VERSION=master \
		--build-arg PG_TEMPORAL_TABLES_VERSION=v1.2.1 \
		--build-arg PG_JOBMON_VERSION=v1.4.1
