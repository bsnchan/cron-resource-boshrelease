# Cron Resource BOSH release

This BOSH release packages the [crontab resource](https://github.com/pivotal-cf-experimental/croncourse-resource) for Concourse.

## Add to your Concourse deployment

Upload this BOSH release to your BOSH director that is running Concourse:

```
bosh upload release releases/cron-resource/cron-resource-<RELEASE NUMBER>.yml
```

Update your Concourse deployment manifest to include this release:

```yaml
releases:
  - name: concourse
    version: latest
  - name: garden-linux
    version: latest
  - name: cron-resource
    version: latest
```

Add the cron-resource release and job to your "worker" job:

```yaml
jobs:
- name: worker
  templates:
    ...
    - {release: cron-resource, name: install_cron_resource_package}
```

Add the cron-resource package path to your worker's property:

```yaml
jobs:
- name: worker
  ...
  properties:
    groundcrew:
      resource_types:
      - type: archive
        image: /var/vcap/packages/archive_resource
      - type: cf
        image: /var/vcap/packages/cf_resource
      - type: docker-image
        image: /var/vcap/packages/docker_image_resource
      - type: git
        image: /var/vcap/packages/git_resource
      - type: s3
        image: /var/vcap/packages/s3_resource
      - type: semver
        image: /var/vcap/packages/semver_resource
      - type: time
        image: /var/vcap/packages/time_resource
      - type: tracker
        image: /var/vcap/packages/tracker_resource
      - type: pool
        image: /var/vcap/packages/pool_resource
      - type: vagrant-cloud
        image: /var/vcap/packages/vagrant_cloud_resource
      - type: github-release
        image: /var/vcap/packages/github_release_resource
      - type: bosh-io-release
        image: /var/vcap/packages/bosh_io_release_resource
      - type: bosh-io-stemcell
        image: /var/vcap/packages/bosh_io_stemcell_resource
      - type: bosh-deployment
        image: /var/vcap/packages/bosh_deployment_resource
      - type: cron
        image: /var/vcap/packages/cron-resource
```

