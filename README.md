reference-nozzle-release
========================

This is a Bosh release of refnozzle, a nozzle used with Cloud Foundry's
Loggregator.

## Bosh Director Requirements
The reference nozzle uses [bosh-dns](https://bosh.io/docs/dns.html).
Therefore, the minimum version of the bosh director is v263.

## Deploy Steps

CF-Deployment
```
bosh create-release --force
bosh upload-release --rebase
bosh -d reference-nozzle deploy manifests/reference-nozzle.yml \
  --vars-file ~/<your-env-vars>.yml \
  -v reference-nozzle-destination=<HTTP POST endpoint> \
  -v reference-nozzle-shard-id=reference-nozzle-id \
  --vars-store=vars.yml -n
```

Bosh Lite Example (with pre-deployed CF-Deployment)
```
bosh create-release --force
bosh -e lite upload-release --rebase
bosh -e lite -d reference-nozzle deploy manifests/reference-nozzle.yml \
  --vars-file ~/workspace/cf-deployment/deployment-vars.yml \
  -v reference-nozzle-destination=postprinter.bosh-lite.com \
  -v reference-nozzle-shard-id=reference-nozzle-id \
  --vars-store=vars.yml -n
```
