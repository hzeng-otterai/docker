#
# Miniconda plus gRPC based on debian
#
FROM continuumio/miniconda:4.6.14

# grpc need to be installed from source to enable SO_REUSEADDR, see https://github.com/grpc/grpc/issues/10755
# protobuf is with cpp implementation in manylinux wheel package
RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential python-dev && \
    rm -rf /var/lib/apt/lists/* && \
	git clone -b v1.21.1 https://github.com/grpc/grpc grpc && \
	cd grpc && \
	git submodule update --init && \
	pip install --no-cache-dir -r requirements.txt && \
	GRPC_PYTHON_BUILD_WITH_CYTHON=1 pip install --no-cache-dir . && \
	cd / && \
	rm -r /grpc && \
	apt-get purge -y --auto-remove build-essential python-dev