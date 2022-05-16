# Keptn

[Keptn](https://github.com/keptn/keptn), pronounced "captain", is a tool for SLO driven deployments.

A shipyard files defines the stages to control, for example:
```
apiVersion: spec.keptn.sh/0.2.2
kind: "Shipyard"
metadata:
  name: "shipyard-test"
spec:
  stages:
    - name: dev
    - name: staging
    - name: production
```

Example SLI specification:
```
spec_version: "1.0"
indicators:
  availability_P_99_95: message_sent_success / message_sent
  availability_consecutive_failure: message_sent_total - message_sent
  latency_P_90: sum(rate(http_request_time_bucket{le="0.4"}[5m])) / sum(rate(http_request_time_count[5m]))
  latency_P_99: sum(rate(http_request_time_bucket{le="0.85"}[5m])) / sum(rate(http_request_time_count[5m]))
```

Example SLO specification:
```
spec_version: '1.0'
comparison:
  compare_with: "single_result"
  include_result_with_score: "pass"
  aggregate_function: avg
objectives:
  - sli: availability_P_99_95
    pass:
    - criteria:
      - ">=0.9995"
  - sli: availability_consecutive_failure
    pass:
      - criteria:
        - "<=2"
  - sli: latency_P_90
    pass:
      - criteria:
        - ">=0.9"
  - sli: latency_P_99
    pass:
      - criteria:
        - ">=0.99"
total_score:
  pass: "90%"
```

Keptn chart is available from https://charts-dev.keptn.sh/

GitHub Actions are available from https://github.com/keptn/gh-action-ci-prepare-keptn-cluster

GitLab CI/CD templates are available from https://gitlab.com/everyonecancontribute/keptn/keptn-templates

This project contains:
* [Dockerfile for running Keptn](Dockerfile.keptn) customized based on a [community template](https://gitlab.com/everyonecancontribute/keptn/keptn-docker/-/blob/main/Dockerfile)
