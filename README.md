# Dockerfile Library
## Helpful Commands
```
docker build -t <ORGANIZATION>/<REPO>:<IMAGE_TAG> .
docker push <ORGANIZATION>/<REPO>:<IMAGE_TAG>
```
### Examples
**No SSH Key Args**
```
docker build -t waltzhorn/foundation:latest .
docker push waltzhorn/foundation:latest
```

**With SSH Key Args**
```
docker build -t waltzhorn/foundation:latest --build-arg SSH_PUBLIC_KEY="$(cat ~/.ssh/waltzhorn.pub)" --build-arg SSH_PRIVATE_KEY="$(cat ~/.ssh/waltzhorn)" .
docker push waltzhorn/foundation:latest
```
