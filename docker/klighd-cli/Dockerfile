FROM node:24-alpine AS builder
WORKDIR /app
COPY . .
RUN yarn install --frozen-lockfile
RUN yarn run lerna run build --scope @kieler/klighd-cli && \
    yarn run lerna run package --scope @kieler/klighd-cli

FROM debian:trixie-slim AS production
COPY --from=builder /app/applications/klighd-cli/bin/klighd-linux /usr/local/bin/klighd-cli
CMD ["klighd-cli"]