# 1601577457 conjur-concourse-integration-bosh-ops-file

Below is an example of a OPs file for deploying Conjur /w bosh.
```yaml
# ops file
- path: /instance_groups/name=web/jobs/name=web/properties/conjur?
  type: replace
  value:
    appliance_url: https://conjur-master
    account: companyName
    tls:
      ca_cert:
        certificate: |
          <certificate contents>
    auth:
      login: host/concourse-instance
      api_key: 283y749823bf9uh23n97rh23f792h379fh2347942f
    secret_template: concourse/myTeam/{{.Secret}}
```


## Links
- [1587417961-conjur-concourse-integration-with-bosh.md](1587417961-conjur-concourse-integration-with-bosh.md)
- [1602269785-concourse-bosh-job-properties-6.3.1.md](1602269785-concourse-bosh-job-properties-6.3.1.md)
