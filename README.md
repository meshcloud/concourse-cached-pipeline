# concourse-cached-pipeline
This is a demo setup to explore flexible caching of build artifacts (e.g. npm node_module folders or maven repositories) in a concourse pipeline.

## Update pipeline
`fly -t ci set-pipeline -c ci/pipeline.yml  --load-vars-from ci/credentials.yml -p concourse-cached-pipeline`

## Execute task with local inputs
fly -t ci execute --config ci/cache-a.yml --input repo=. --exclude-ignored
