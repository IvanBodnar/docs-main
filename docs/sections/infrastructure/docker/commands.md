# Commands
<hr>
<br>

[Commands docs](https://docs.docker.com/engine/reference/commandline/docker/)

### Remove
- All containers
```bash
docker container stop $(docker container ls -aq)
docker container rm $(docker container ls -aq)
```

- Filter
```bash
docker container prune --filter "until=12h"
```
