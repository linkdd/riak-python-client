RIAK_CONF = ${RIAK_DIR}/etc/riak.conf
# ADVANCED_CONF = ${RIAK_DIR}/etc/advanced.config
# RIAK = ${RIAK_DIR}/bin/riak
RIAK_ADMIN = ${RIAK_DIR}/bin/riak-admin
# CERTS_DIR = $(shell pwd)/../src/test/resources

preconfigure:
	echo "storage_backend = leveldb" >> ${RIAK_CONF}
	echo "search = on" >> ${RIAK_CONF}
	echo "listener.protobuf.internal = 127.0.0.1:8087" >> ${RIAK_CONF}
	echo "listener.http.internal = 127.0.0.1:8098" >> ${RIAK_CONF}

configure:
	@../setup.py create_bucket_types --riak-admin=${RIAK_ADMIN}

compile:
	@yes y | pip uninstall riak-pb protobuf
	@../setup.py develop

lint:
	@pip install --upgrade pep8 pyflakes
	@cd ..; pep8 riak *.py
	@cd ..; pyflakes riak *.py

test:
	@RUN_YZ=1 SKIP_INDEXES=0 ../setup.py test