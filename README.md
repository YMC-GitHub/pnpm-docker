The Docker images of [pnpm](https://pnpm.io).

## Supported tags

- tags format 1: `{pnpm-info}-{node-info}-{os-info}`
- tags format for default os: `{pnpm-info}-{node-info}`
- tags format for default node: `{pnpm-info}-{os-info}`
- tags format for default pnpm: `{node-info}-{os-info}`
- tags format for default os and node: `{pnpm-info}`
- tags format for default pnpm and node: `{os-info}`
- tags format for default pnpm and os: `{node-info}`

- pnpm-info: 9.4.0,9.4,9.0
- node-info: node18,node20,node21,node22
- os-info: bullseye,alpine

- `9.4.0-node22-bullseye`, `9.4-node22-bullseye`, `9-node22-bullseye`, `node22-bullseye`, `9.4.0-node22`, `9.4-node22`, `9-node22`, `node22`, `9.4.0-bullseye`, `9.4-bullseye`, `9-bullseye`, `bullseye`, `9.4.0`, `9.4`, `9`
- `9.4.0-node21-bullseye`, `9.4-node21-bullseye`, `9-node21-bullseye`, `node21-bullseye`, `9.4.0-node21`, `9.4-node21`, `9-node21`, `node21`
- `9.4.0-node20-bullseye`, `9.4-node20-bullseye`, `9-node20-bullseye`, `node20-bullseye`, `9.4.0-node20`, `9.4-node20`, `9-node20`, `node20`
- `9.4.0-node18-bullseye`, `9.4-node18-bullseye`, `9-node19-bullseye`, `node19-bullseye`, `9.4.0-node18`, `9.4-node18`, `9-node18`, `node18`
- `9.4.0-node22-alpine`, `9.4-node22-alpine`, `9-node22-alpine`, `node22-alpine`, `9.4.0-alpine`, `9.4-alpine`, `9-alpine`, `alpine`
- `9.4.0-node21-alpine`, `9.4-node21-alpine`, `9-node21-alpine`, `node21-alpine`
- `9.4.0-node20-alpine`, `9.4-node20-alpine`, `9-node20-alpine`, `node20-alpine`
- `9.4.0-node18-alpine`, `9.4-node18-alpine`, `9-node18-alpine`, `node18-alpine`

## License

MIT License

Copyright (c) 2024-present Ye Miancheng <ymc.github@gmail.com>

## Refer

[g-plane/pnpm-docker](https://github.com/g-plane/pnpm-docker)

## Idea

- use base image from node with args when docker build
- install pnpm with npm

get detials in [Dockerfile](./Dockerfile)

## Build From Source In Local (Bash)

```bash
# info env or var
cat .env/node-alpine.env
# node=22
# os=alpine

cat .env/pnpm.env
# pnpm_patch=9.4.0
# pnpm_minor=9.4
# pnpm_major=9

# import env or var
. .env/node-alpine.env
. .env/pnpm.env

# ns=yemiancheng

docker build --build-arg base=$node-$os --build-arg pnpm=$pnpm_patch \
  -t $ns/pnpm:$pnpm_patch-node$node-$os \
  -t $ns/pnpm:$pnpm_minor-node$node-$os \
  -t $ns/pnpm:$pnpm_major-node$node-$os \
  -t $ns/pnpm:node$node-$os .

# build for default os
. .env/default.env
docker build --build-arg base=$node-$default_os --build-arg pnpm=$pnpm_patch \
  -t $ns/pnpm:$pnpm_patch-node$node \
  -t $ns/pnpm:$pnpm_minor-node$node \
  -t $ns/pnpm:$pnpm_major-node$node \
  -t $ns/pnpm:node$node .

# build for default node
docker build --build-arg base=$default_node-$os --build-arg pnpm=$pnpm_patch \
  -t $ns/pnpm:$pnpm_patch-$os \
  -t $ns/pnpm:$pnpm_minor-$os \
  -t $ns/pnpm:$pnpm_major-$os \
  -t $ns/pnpm:$os .

# build for default os and node
docker build --build-arg base=$default_node-$default_os --build-arg pnpm=$pnpm_patch \
  -t $ns/pnpm:$pnpm_patch \
  -t $ns/pnpm:$pnpm_minor \
  -t $ns/pnpm:$pnpm_major \
  -t $ns/pnpm .

docker run $ns/pnpm:$pnpm_patch-node$node-$os -v
docker run $ns/pnpm:$pnpm_minor-node$node-$os -v
docker run $ns/pnpm:$pnpm_major-node$node-$os -v
docker run $ns/pnpm:node$node-$os -v

# test for default os
docker run $ns/pnpm:$pnpm_patch-node$node -v
docker run $ns/pnpm:$pnpm_minor-node$node -v
docker run $ns/pnpm:$pnpm_major-node$node -v
docker run $ns/pnpm:node$node -v

# test for default node
docker run $ns/pnpm:$pnpm_patch-$os -v
docker run $ns/pnpm:$pnpm_minor-$os -v
docker run $ns/pnpm:$pnpm_major-$os -v
docker run $ns/pnpm:$os -v

# test for default os and node

docker run $ns/pnpm:$pnpm_patch -v
docker run $ns/pnpm:$pnpm_minor -v
docker run $ns/pnpm:$pnpm_major -v
docker run $ns/pnpm -v

# login docker registry
# ...


docker push $ns/pnpm:$pnpm_patch-node$node-$os
docker push $ns/pnpm:$pnpm_minor-node$node-$os
docker push $ns/pnpm:$pnpm_major-node$node-$os
docker push $ns/pnpm:node$node-$os

# publish fro default os
docker push $ns/pnpm:$pnpm_patch-node$node
docker push $ns/pnpm:$pnpm_minor-node$node
docker push $ns/pnpm:$pnpm_major-node$node
docker push $ns/pnpm:node$node

# publish fro default node
docker push $ns/pnpm:$pnpm_patch-$os
docker push $ns/pnpm:$pnpm_minor-$os
docker push $ns/pnpm:$pnpm_major-$os
docker push $ns/pnpm:$os

# publish fro default os and node
docker push $ns/pnpm:$pnpm_patch
docker push $ns/pnpm:$pnpm_minor
docker push $ns/pnpm:$pnpm_major
docker push $ns/pnpm

```

## Build From Source In Github workflow

get detials in [.github/workflows/build.yml](./.github/workflows/build.yml)
