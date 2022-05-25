issue using helm


innitial running helm install:


                #  helm install nmpostgresql bitnami/postgresql --version 11.2.6  -f postgresql-values.yaml --debug




output:

            create Pod nmpostgresql-0 in StatefulSet nmpostgresql failed error: pods "nmpostgresql-0" is forbidden: unable to validate against any security context constraint: [provider "anyuid": Forbidden: not usable by user or serviceaccount, provider restricted: .spec.securityContext.fsGroup: Invalid value: []int64{1001}: 1001 is not an allowed group, spec.containers[0].securityContext.runAsUser: Invalid value: 1001: must be in the ranges: [1000580000, 1000589999], provider "nonroot": Forbidden: not usable by user or serviceaccount, provider "hostmount-anyuid": Forbidden: not usable by user or serviceaccount, provider "machine-api-termination-handler": Forbidden: not usable by user or serviceaccount, provider "hostnetwork": Forbidden: not usable by user or serviceaccount, provider "hostaccess": Forbidden: not usable by user or serviceaccount, provider "privileged": Forbidden: not usable by user or serviceaccount]


for OpenShift should security should be disabled:



            primary.podSecurityContext.enabled = false



debug default values:

            helm show values bitnami/postgresql --version 11.2.6 | sed 's/\s*#.*$//' > chart_values.yaml
