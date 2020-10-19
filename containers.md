## Skopeo
```
skopeo inspect --raw docker://docker.io/ubuntu | jq .
skopeo inspect --override-os linux docker://docker.io/ubuntu | jq .
skopeo inspect docker://docker.io/ubuntu@sha256:d5a6519d9f048100123c568eb83f7ef5bfcad69b01424f420f17c932b00dea76

skopeo --override-os linux --insecure-policy copy docker://docker.io/ubuntu oci:ubuntu2 --dest-shared-blob-dir blobs
```
