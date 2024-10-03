FROM debian:bookworm-slim

#Non-root user
ARG NON_ROOT_UID=1000
ARG NON_ROOT_GID=1000

RUN \
  set -ex && \
  if [ ! $(getent group $NON_ROOT_GID) ] ; then groupadd --gid ${NON_ROOT_GID} node ; fi && \
  useradd --uid ${NON_ROOT_UID} --gid ${NON_ROOT_GID} --shell /bin/bash --create-home node && \
  apt-get update && \
  # Cypress dependencies included
  apt-get install -y ca-certificates curl wget gnupg dirmngr xz-utils libatomic1 unzip libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libnss3 libxss1 libasound2 libxtst6 xauth xvfb --no-install-recommends

USER node

WORKDIR /home/node

RUN \
  set -ex && \
  mkdir www && \
  curl -fsSL https://fnm.vercel.app/install | bash -s -- --skip-shell && \
  # Fix shell infer https://github.com/Schniz/fnm/issues/412
  echo '# fnm' >> /home/node/.bashrc && \
  echo 'export PATH=/home/node/.local/share/fnm:$PATH' >> /home/node/.bashrc && \
  echo 'eval "$(fnm env --use-on-cd --shell bash)"' >> /home/node/.bashrc

WORKDIR /home/node/www

# Keep container running
CMD ["sleep", "infinity"]
