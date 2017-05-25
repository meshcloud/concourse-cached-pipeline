# concourse-cached-pipeline
This is a demo setup to explore flexible caching of build artifacts (e.g. npm node_module folders or maven repositories) in a concourse pipeline. A detailed description of the approach used in this repo and how it works is available on [our blog](https://www.meshcloud.io/en/2017/05/25/caching-directories-in-concourse-ci-pipelines/). 

In short:
We use a Task instead of a Resource to 
 - find last parent commit id that changed package file (e.g. packages.json, pom.xml)
 - check cache for package tarball (http file server, but can swap in a different one)
 - if package tarball has not been built yet, invoke package manager to fetch packages and generate tarball
 - download and extract package tarball

The scripts should run in any standard docker image with a proper bash and curl, so you can easily incorporate them in your existing CI pipelines.

## Update pipeline
`fly -t ci set-pipeline -c ci/pipeline.yml  --load-vars-from ci/credentials.yml -p concourse-cached-pipeline`

## Execute task with local inputs
`fly -t ci execute --config ci/cache-a.yml --input repo=. --exclude-ignore`
