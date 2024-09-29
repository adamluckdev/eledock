FROM debian:bookworm-slim

#Non-root user
ARG NON_ROOT_UID=1000
ARG NON_ROOT_GID=1000

RUN groupadd --gid ${NON_ROOT_GID} node && \
  useradd --uid ${NON_ROOT_UID} --gid node --shell /bin/bash --create-home node

RUN \
  set -ex && \
  apt-get update && \
  apt-get install -y ca-certificates curl wget gnupg dirmngr xz-utils libatomic1 unzip --no-install-recommends

USER node

WORKDIR /home/node

RUN \
  set -ex && \
  curl -fsSL https://fnm.vercel.app/install | bash -s -- --skip-shell && \
  # Fix shell infer https://github.com/Schniz/fnm/issues/412
  echo '# fnm' >> /home/node/.bashrc && \
  echo 'export PATH=/home/node/.local/share/fnm:$PATH' >> /home/node/.bashrc && \
  echo 'eval "$(fnm env --use-on-cd --shell bash)"' >> /home/node/.bashrc

# Keep container running
CMD ["sleep", "infinity"]
