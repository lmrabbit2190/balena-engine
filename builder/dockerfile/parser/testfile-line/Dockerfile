# ESCAPE=\



FROM brimstone/ubuntu:14.04


# TORUN -v /var/run/balena-engine.sock:/var/run/balena-engine.sock


ENV GOPATH \
/go



# Install the packages we need, clean up after them and us
RUN apt-get update \
	&& dpkg -l | awk '/^ii/ {print $2}' > /tmp/dpkg.clean \


    && apt-get install -y --no-install-recommends git golang ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists \

	&& go get -v github.com/brimstone/consuldock \
    && mv $GOPATH/bin/consuldock /usr/local/bin/consuldock \

	&& dpkg -l | awk '/^ii/ {print $2}' > /tmp/dpkg.dirty \
	&& apt-get remove --purge -y $(diff /tmp/dpkg.clean /tmp/dpkg.dirty | awk '/^>/ {print $2}') \
	&& rm /tmp/dpkg.* \
	&& rm -rf $GOPATH




