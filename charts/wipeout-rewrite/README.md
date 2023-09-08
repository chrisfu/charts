# wipEout-rewrite... in Kubernetes

This chart installs [wipEout-Rewrite](https://github.com/phoboslab/wipeout-rewrite), leveraging my Dockerfile build that you can find [here](https://hub.docker.com/repository/docker/chrisfu/docker-wipeout-rewrite) (source [here](https://github.com/chrisfu/docker-wipeout-rewrite)).

## Configuration

Please see the default `values.yaml` for more information on what is configurable. This chart supports Ingresses, and also Service annotations if you want to use something like [ExternalDNS](https://github.com/kubernetes-sigs/external-dns) in combination with NodePorts to reach the application.

## Usage

Generally, you'll want to install this with an Ingress enabled, but of course how you expose the service is entirely up to you. Either way, you'll want to customise a `values.yaml` for your own use case and run something like the following command.

```console
helm repo add chrisfu https://chrisfu.github.io/charts
helm install my-wipeout-app chrisfu/wipeout-rewrite -n my-namespace -f values-customised.yaml
```

Once installed, you can access the application by following the instructions output by the Helm chart installation process.

## More Info

Check out my [GitHub Pages](https://chrisfu.github.io/) for more information on my available charts.