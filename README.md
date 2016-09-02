# sfm-docker
*Docker images for SFM processing*

## base / quay.io/fish/sfm-base
Base image including open source (but non-free!) base SfM components:

 - [SiftGPU](http://www.cs.unc.edu/~ccwu/siftgpu/)
 - [Multicore Bundle Adjustment(PBA)](http://grail.cs.washington.edu/projects/mcba/)
 - [CMVS-PMMVS (cmake based fork)](https://github.com/pmoulon/CMVS-PMVS)


## vsfm / quay.io/fish/vsfm
[VisualSFM](http://ccwu.me/vsfm) Docker image on top of sfm-base.
To use it interactively, run:

```
docker run \
  -v /path/to/pictures:/data \
  -v /tmp/.X11-unix:/tmp/.X11-unix
  -e DISPLAY=$DISPLAY \
  quay.io/fish/vsfm
```

Now you can open/save files from your host via /data.

## TODO
- Add cuda support
