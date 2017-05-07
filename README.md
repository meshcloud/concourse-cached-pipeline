# concourse-cached-pipeline

## Update pipeline
`fly -t ci set-pipeline -c ci/pipeline.yml  --load-vars-from ci/credentials.yml -p concourse-cached-pipeline`

## Execute task with local inputs
fly -t ci execute --config ci/cache-a.yml --input repo=. --exclude-ignored