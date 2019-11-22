# UWGDA2020 JupyterHub Image Builder

This repository builds a [JupyterHub](https://jupyter.org/hub) environment with [Repo2Docker](https://repo2docker.readthedocs.io/en/latest/) and [GitHub Actions CI](https://help.github.com/en/actions/automating-your-workflow-with-github-actions) 

[![Action Status](https://github.com/uw-cryo/uwgda2020/workflows/Repo2Docker/badge.svg)](https://github.com/uw-cryo/uwgda2020/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/uwcryo/uwgda2020)](https://hub.docker.com/r/uwcryo/uwgda2020/tags)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/uw-cryo/uwgda2020/master?urlpath=lab)

https://hub.docker.com/r/uwcryo/uwgda2020/tags

### How to use

build with GitHub Actions simply by pushing to GitHub

* pull requests trigger image building without pushing to DockerHub

* commits to master branch (except readme.md changes) trigger re-building image 
* successfully built image is tagged by github commit short sha and 'latest'
```
git commit -a -m "modified binder/environment to my liking"
git push
```
* pushing a tag results in a docker image with the same tag:
```
git tag -am "tag version 2.3.2" 2.3.2
git push --tags
```

### Pull your image to run a local JupyterLab session
```
export IMAGE=uwcryo/uwgda2020
export TAG=latest
docker pull docker.pkg.github.com/$IMAGE:$TAG
docker run -it --name repo2docker -p 8888:8888 $IMAGE:$TAG jupyter lab --ip 0.0.0.0
docker stop repo2docker
docker rm repo2docker
```

### Point to a specific tagged image in JupyterHub config
(image: uwcryo/uwgda:0.1)
https://zero-to-jupyterhub.readthedocs.io/en/latest/reference/reference.html?highlight=profile_list#singleuser-profilelist

