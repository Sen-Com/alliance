FROM golang:1.21-bullseye AS build

RUN apt update && apt install jq build-essential -y

WORKDIR /allianced
COPY . /allianced

RUN make build

FROM debian:bullseye AS run
COPY ./scripts/containers/build-wrapper.sh /allianced/build-wrapper.sh

VOLUME /allianced
COPY --from=build /allianced/ /allianced/
WORKDIR /allianced

EXPOSE 26656 26657
ENTRYPOINT ["/allianced/build-wrapper.sh"]
CMD ["start", "--log_format", "plain"]
STOPSIGNAL SIGTERM
