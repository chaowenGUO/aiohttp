FROM python
RUN ["python", "-m", "venv", "--copies", "/usr/local/venv"]
COPY server.pyc /usr/local/venv/
WORKDIR /usr/local/venv
RUN ["bin/pip", "install", "uvloop", "asyncpg", "aredis", "aiokafka", "aiohttp"]

FROM scratch
ARG VERSION
WORKDIR /usr/local/venv
COPY --from=0 /usr/local/venv .
COPY --from=python:slim /usr/local/lib/libpython$VERSION.so.1.0 /usr/lib/x86_64-linux-gnu/
COPY --from=python:slim /usr/local/lib/python$VERSION /usr/local/lib/python$VERSION/
COPY --from=python:slim /lib/x86_64-linux-gnu /lib/x86_64-linux-gnu/
COPY --from=python:slim /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/
COPY --from=python:slim /lib64 /lib64/
ENTRYPOINT ["bin/python", "server.pyc"]
