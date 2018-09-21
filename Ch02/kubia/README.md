# kubia

For this chapter I want to build the `kubia` image locally and start it from
within `minikube` instead of having to push the built image to a public
repository and have `minikube` download it from there. To do this we will need
to point the docker client to the docker service that is running within
`minikube` by executing:

```shell
minikube start
eval $(minikube docker-env)
```

From there we can build the image and it will be stored within `minikube`'s
local image repository.

```shell
docker build -t kubia .
```

We can then use `kubectl` to start a container from that image and check that
it is running. Note that we set the switch `--image-pull-policy=Never` so that
kubernetes doe snot try to pull the image from a public repository.

```
kubectl run kubia --image-pull-policy=Never --image=kubia:latest --port=8080 --generator=run/v1
kubectl get pods
```
