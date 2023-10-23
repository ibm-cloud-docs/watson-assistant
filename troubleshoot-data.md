---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-23"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting known issues for {{site.data.keyword.icp4dfull_notm}}
{: #troubleshoot-data}

[{{site.data.keyword.icp4dfull_notm}}]{: tag-cp4d}

Get help with solving issues that you might encounter with {{site.data.keyword.assistant_classic_short}} on {{site.data.keyword.icp4dfull_notm}}.
{: shortdesc}

## 4.5.x
{: #troubleshoot-45x}

### Pod `RESTARTS` count stays at 0 after a 4.5.x upgrade even though a few assistant pods are restarting
{: #troubleshoot-453-restarts-zero}

- Problem: After you upgrade {{site.data.keyword.assistant_classic_short}}, the pod `RESTARTS` count stays at 0 even though certain assistant pods are restarting.
- Cause: During the upgrade, custom resources that are owned by {{site.data.keyword.assistant_classic_short}} for the `certificates.certmanager.k8s.io` CRD are deleted by using a script that runs in the background. Sometimes the CR deletion script completes before the assistant operator gets upgraded. In that case, the old assistant operator might re-create custom resources for the `certificates.certmanager.k8s.io` CRD. Leftover CRs might cause the certificate manager to continuously regenerate some certificate secrets, causing some assistant pods to restart recursively.
- Solution: Run the following script to delete leftover custom resources for the `certificates.certmanager.k8s.io` CRD after you set INSTANCE (normally `wa`) and PROJECT_CPD_INSTANCE variables:

   ```bash
   for i in `oc get certificates.certmanager.k8s.io -l icpdsupport/addOnId=assistant --namespace ${PROJECT_CPD_INSTANCE} | grep "${INSTANCE}-"| awk '{print $1}'`; do oc delete certificates.certmanager.k8s.io $i --namespace ${PROJECT_CPD_INSTANCE}; done
   ```
   {: codeblock}

## 4.5.0
{: #troubleshoot-450}

### Data Governor not healthy after installation
{: #troubleshoot-450-data-governor-not-healthy}

After {{site.data.keyword.assistant_classic_short}} is installed, the `dataexhausttenant` custom resource that is named `wa-data-governor-ibm-data-governor-data-exhaust-internal` gets stuck in the `Topics` phase. When this happens, errors in the Data Governor pods report that the service does not exist.

1. Get the status of the `wa-data-governor` custom resource:

    ```bash
    oc get DataExhaust
    ```
    {: codeblock}

1. Wait for the `wa-data-governor` custom resource to be in the `Completed` phase:

    ```bash
    NAME               STATUS      VERSION   COMPLETED
    wa-data-governor   Completed   master    1s
    ```
    {: codeblock}

1. Pause the reconciliation of the `wa-data-governor` custom resource:

    ```bash
    oc patch dataexhaust wa-data-governor -p '{"metadata":{"annotations":{"pause-reconciliation":"true"}}}' --type merge
    ```
    {: codeblock}

1. Apply the fix to the `dataexhausttenant` custom resource:

    ```bash
    oc patch dataexhausttenant wa-data-governor-ibm-data-governor-data-exhaust-internal  -p '{"spec":{"topics":{"data":{"replicas": 1}}}}' --type merge
    ```
    {: codeblock}

1. Wait for the Data Governor pods to stop failing. You can restart the admin pods to speed up this process.

1. Continue the reconciliation of the `wa-data-governor` custom resource:

    ```bash
    oc patch dataexhaust wa-data-governor --type=json -p='[{"op": "remove", "path": "/metadata/annotations/pause-reconciliation"}]'
    ```
    {: codeblock}

### RabbitMQ gets stuck in a loop after several installation attempts
{: #troubleshoot-450-rabbitmq-stuck}

After an initial installation or upgrade failure and repeated attempts to retry, the common services RabbitMQ operator pod can get into a `CrashLoopBackOff` state. For example, the log might include the following types of messages:

```text
"error":"failed to upgrade release: post-upgrade hooks failed: warning:
Hook post-upgrade ibm-rabbitmq/templates/rabbitmq-backup-labeling-job.yaml
failed: jobs.batch "{%name}-ibm-rabbitmq-backup-label" already exists"
```
{: screen}

Resources for the `ibm-rabbitmq-operator.v1.0.11` component must be removed before a new installation or upgrade is started. If too many attempts occur in succession, remaining resources can cause new installations to fail.

1. Delete the RabbitMQ backup label job from the previous installation or upgrade attempt. Look for the name of the job in the logs. The name ends in `-ibm-rabbitmq-backup-label`:

    ```bash
    oc delete job {%name}-ibm-rabbitmq-backup-label -n ${PROJECT_CPD_INSTANCE}
    ```
    {: codeblock}

1. Check that the pod returns a `Ready` state:

    ```bash
    oc get pods -n ibm-common-services | grep ibm-rabbitmq
    ```
    {: codeblock}

### Preparing to install a size large deployment
{: #troubleshoot-450-prepare-large-install}

If you specify `large` for the `watson_assistant_size` option when you install {{site.data.keyword.assistant_classic_short}}, the installation fails to complete successfully.

Before you install a size large deployment of {{site.data.keyword.assistant_classic_short}}, apply the following fix. The following fix uses `wa` as the name of the Watson Assistant instance and `cpd` as the namespace where Watson Assistant is installed. These values are set in environment variables. Before you run the command, update the `INSTANCE` variable with the name of your instance, and update the `NAMESPACE` variable with the namespace where your instance in installed:

```bash
INSTANCE=wa ; \
NAMESPACE=cpd ; \
#DRY_RUN="--dry-run=client --output=yaml"     # To apply the changes, change to an empty string
DRY_RUN=""
cat <<EOF | tee wa-network-policy-base.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  annotations:
    oppy.ibm.com/internal-name: infra.networkpolicy
  labels:
    app: ${INSTANCE}-network-policy
    app.kubernetes.io/instance: ${INSTANCE}
    app.kubernetes.io/managed-by: Ansible
    app.kubernetes.io/name: watson-assistant
    component: network-policy
    icpdsupport/addOnId: assistant
    icpdsupport/app: ${INSTANCE}-network-policy
    icpdsupport/ignore-on-nd-backup: "true"
    icpdsupport/serviceInstanceId: inst-1
    service: conversation
    slot: ${INSTANCE}
    tenant: PRIVATE
    velero.io/exclude-from-backup: "true"
  name: ${INSTANCE}-network-policy
  namespace: ${NAMESPACE}
spec:
  ingress:
  - from:
    - podSelector:
        matchLabels:
          service: conversation
          slot: ${INSTANCE}
    - podSelector:
        matchLabels:
          slot: global
    - podSelector:
        matchLabels:
          component: watson-gateway
    - podSelector:
        matchLabels:
          component: dvt
    - podSelector:
        matchLabels:
          dwf_service: ${INSTANCE}-clu
          network-policy: allow-egress
    - podSelector:
        matchLabels:
          app: 0020-zen-base
    - namespaceSelector:
        matchLabels:
          ns: ${NAMESPACE}
      podSelector:
        matchLabels:
          app: 0020-zen-base
    - podSelector:
        matchLabels:
          component: ibm-nginx
    - namespaceSelector:
        matchLabels:
          ns: ${NAMESPACE}
      podSelector:
        matchLabels:
          component: ibm-nginx
    - namespaceSelector:
        matchLabels:
          assistant.watson.ibm.com/role: operator
      podSelector:
        matchLabels:
          release: assistant-operator
    - namespaceSelector:
        matchLabels:
          assistant.watson.ibm.com/role: operator
      podSelector:
        matchLabels:
          app: watson-assistant-operator
    - namespaceSelector:
        matchLabels:
          assistant.watson.ibm.com/role: operator
      podSelector:
        matchLabels:
          app.kubernetes.io/instance: watson-assistant-operator
    - namespaceSelector:
        matchLabels:
          assistant.watson.ibm.com/role: operator
      podSelector:
        matchLabels:
          app.kubernetes.io/instance: ibm-etcd-operator-release
    - namespaceSelector:
        matchLabels:
          assistant.watson.ibm.com/role: operator
      podSelector:
        matchLabels:
          app.kubernetes.io/instance: ibm-etcd-operator
  podSelector:
    matchLabels:
      service: conversation
      slot: ${INSTANCE}
  policyTypes:
  - Ingress
EOF
for MICROSERVICE in analytics clu-embedding clu-serving clu-training create-slot-job data-governor dialog dragonfly-clu-mm ed es-store etcd integrations master nlu recommends sireg-ubi-ja-tok-20160902 sireg-ubi-ko-tok-20181109 spellchecker-mm store store-admin store-cronjob store-sync store_db_creator store_db_schema_updater system-entities tfmm ui ${INSTANCE}-redis webhooks-connector
do
  # Change name and add component to selector
  # Apply to the cluster
  cat wa-network-policy-base.yaml | \
    oc patch --dry-run=client --output=yaml -f - --type=merge --patch "{
        \"metadata\": {\"name\": \"${INSTANCE}-network-policy-$( echo $MICROSERVICE | tr _ -)\"},
        \"spec\": {\"podSelector\":{\"matchLabels\":{\"component\": \"${MICROSERVICE}\"}}}
      }" |
    oc apply -f - ${DRY_RUN}
done
```
{: codeblock}

### Fixing a size large installation
{: #troubleshoot-450-fix-large-install}

Apply this fix if you installed a size `large` deployment, and your installation fails to complete successfully. In some cases, pods aren't able to communicate with other pods, and the Transmission Control Protocol (TCP) connections can't be established.

To confirm whether you are affected by this issue, run the following command:

```bash
oc logs --selector app=sdn --namespace openshift-sdn --container sdn | grep "Ignoring NetworkPolicy"
```
{: codeblock}

If you are affected, you see output similar to the following example:

```text
W0624 12:58:21.407901    2480 networkpolicy.go:484] Ignoring NetworkPolicy cpd/wa-network-policy because it generates
```
{: screen}

If you encounter this error, apply the following fix to resolve the issue. The following fix uses `wa` as the name of the Watson Assistant instance. This value is set in an environment variable. Before you run the command, update the `INSTANCE` variable with the name of your instance:

```bash
INSTANCE=wa ; \
#DRY_RUN="--dry-run=client --output=yaml"     # To apply the changes, change to an empty string
DRY_RUN=""
for MICROSERVICE in analytics clu-embedding clu-serving clu-training create-slot-job data-governor dialog dragonfly-clu-mm ed es-store etcd integrations master nlu recommends sireg-ubi-ja-tok-20160902 sireg-ubi-ko-tok-20181109 spellchecker-mm store store-admin store-cronjob store-sync store_db_creator store_db_schema_updater system-entities tfmm ui ${INSTANCE}-redis webhooks-connector
do
  # Get original networking policy
  # Clean up metadata fields to get the resource applied by Watson Assistant
  # Change name and add component to selector
  # Apply to the cluster
  oc get networkpolicy $INSTANCE-network-policy --output yaml | \
  oc patch --dry-run=client --output=yaml -f - --type=json --patch='[
      {"op":"remove", "path":"/metadata/creationTimestamp"},
      {"op":"remove", "path":"/metadata/generation"},
      {"op":"remove", "path":"/metadata/resourceVersion"},
      {"op":"remove", "path":"/metadata/uid"},
      {"op":"remove", "path":"/metadata/annotations/kubectl.kubernetes.io~1last-applied-configuration"},
      {"op":"remove", "path":"/metadata/ownerReferences"}
    ]' | \
    oc patch --dry-run=client --output=yaml -f - --type=merge --patch "{
        \"metadata\": {\"name\": \"${INSTANCE}-network-policy-$( echo $MICROSERVICE | tr _ -)\"},
        \"spec\": {\"podSelector\":{\"matchLabels\":{\"component\": \"${MICROSERVICE}\"}}}
      }" |
    oc apply -f - ${DRY_RUN}
done
```
{: codeblock}

### Unable to scale the size of Redis pods
{: #troubleshoot-450-scale-redis}

When you scale the deployment size of {{site.data.keyword.assistant_classic_short}}, the Redis pods do not scale correctly and don't match the new size of the deployment (`small`, `medium`, or `large`). This problem is a known issue in Redis operator v1.5.1.

When you scale the size of your deployment, you must delete the Redis custom resource. Redis automatically re-creates the custom resource with the correct size and pods.

To delete and re-create the Redis custom resource:

1. Source the environment variables from the script:

    ```bash
    source ./cpd_vars.sh
    ```
    {: codeblock}

    If you don't have the script that defines the environment variables, see [Setting up installation environment variables](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=information-setting-up-installation-environment-variables){: external}.

1. Export the name of the Redis custom resource to an environment variable:

    ```bash
    export REDIS_CR_NAME=`oc get redissentinels.redis.databases.cloud.ibm.com -l icpdsupport/addOnId=assistant -n ${PROJECT_CPD_INSTANCE} | grep -v NAME| awk '{print $1}'`
    ```
    {: codeblock}

1. Delete the Redis custom resource:

    ```bash
    oc delete redissentinels.redis.databases.cloud.ibm.com ${REDIS_CR_NAME} -n ${PROJECT_CPD_INSTANCE}
    ```
    {: codeblock}

    It might take approximately 5 minutes for the custom resource to be re-created.

1. Verify that Redis is running:

    ```bash
    oc get redissentinels.redis.databases.cloud.ibm.com -n ${PROJECT_CPD_INSTANCE}
    ```
    {: codeblock}

1. Export the name of your instance as an environment variable:

    ```bash
    export INSTANCE=`oc get wa -n ${PROJECT_CPD_INSTANCE} |grep -v NAME| awk '{print $1}'`
    ```
    {: codeblock}

1. Delete the Redis analytics secret:

    ```bash
    oc delete secrets ${INSTANCE}-analytics-redis
    ```
    {: codeblock}

1. Delete the `${INSTANCE}-analytics` deployment pods.

## 4.0.x
{: #troubleshoot-40x}

### Data Governor error causes deployment failure
{: #troubleshoot-40x-data-governor-deployment-fail}

The following fix applies to 4.0.0 through 4.0.8. In some cases, the deployment is stuck and pods are not coming up because of an issue with the interaction between the Events operator and the Data Governor custom resource (CR).  

Complete the following steps to determine whether you are impacted by this issue and, if necessary, apply the patch to resolve it:

1. To determine whether you are impacted, run the following command to see whether the CR was applied successfully:

    ```bash
    oc get dataexhaust wa-data-governor -n $OPERAND_NS -o yaml
    ```
    {: codeblock}

    If you do not receive any error, then you do not need to apply the patch. If you receive an error similar to the following example, complete the next step to apply the patch:

    ```text
    message: 'Failed to create object: b''{"kind":"Status","apiVersion":"v1","metadata":{},"status":"Failure","message":"Internal
          error occurred: replace operation does not apply: doc is missing path: /metadata/labels/icpdsupport/serviceInstanceId:
          missing value","reason":"InternalError","details":{"causes":[{"message":"replace
          operation does not apply: doc is missing path: /metadata/labels/icpdsupport/serviceInstanceId:
          missing value"}]},"code":500}\n'''
        reason: Failed
        status: "True"
        type: Failure
      ibmDataGovernorService: InProgress
    ```
    {: screen}

1. From your operand namespace, run the following command to apply the patch. In the command, `wa` is used as the name of the instance. Replace this value with the name of your instance:

    ```bash
    cat <<EOF | oc apply -f -
    apiVersion: assistant.watson.ibm.com/v1
    kind: TemporaryPatch
    metadata:
      name: wa-data-governor
    spec:
        apiVersion: assistant.watson.ibm.com/v1
        kind: WatsonAssistant
        name: wa     # Replace wa with the name of your Watson Assistant instance
        patch:
          data-governor:
            dataexhaust:
              spec:
                additionalLabels:
                  icpdsupport/serviceInstanceId: inst-1
          kafkauser:
            metadata:
              labels:
                icpdsupport/serviceInstanceId: inst-1
    patchType: patchStrategicMerge
    EOF
    ```
    {: codeblock}

    Wait about 15 minutes for the changes to take effect.

1. Validate that the patch was applied successfully:

    ```bash
    oc get dataexhaust wa-data-governor -n $OPERAND_NS -o yaml
    ```
    {: codeblock}

    The patch was applied successfully when the value of `serviceInstanceId` is `inst-1`:

    ```text
    spec:
      additionalLabels:
        icpdsupport/serviceInstanceId: inst-1
    ```
    {: screen}

### Security context constraint permission errors
{: #troubleshoot-40x-scc-permission-error}

The following fix applies to 4.0.0 through 4.0.5. If a cluster has a security context constraint (SCC) that takes precedence over **restricted** SCCs and has different permissions than **restricted** SCCs, then 4.0.0 through 4.0.5 installations might fail with permission errors. For example, the `update-schema-store-db-job` job reports errors similar to the following example:

```text
oc logs wa-4.0.2-update-schema-store-db-job-bpsdr postgres-is-prepared
Waiting until postgres is running and responding
psql: error: could not read root certificate file "/tls/ca.crt": Permission denied
    - The basic command to postgres failed (retry in 5 sec)
psql: error: could not read root certificate file "/tls/ca.crt": Permission denied
    - The basic command to postgres failed (retry in 5 sec)
psql: error: could not read root certificate file "/tls/ca.crt": Permission denied
    - The basic command to postgres failed (retry in 5 sec)
..
..
```
{: screen}

Other pods might have similar permission errors. If you look at the SCCs of the pods, you can see they are not restricted. For example, if you run the `oc describe pod wa-etcd-0 |grep scc` command, you get an output similar to the following example:

```text
openshift.io/scc: fsgroup-scc
```
{: screen}

To fix this issue, raise the priority of the **restricted** SCC so that it takes precedence:

1. Run the following command:

    ```bash
    oc edit scc restricted
    ```
    {: codeblock}

1. Change the `priority` from `null` to `1`.

Now, new pods default back to the expected **restricted** SCC. When you run the `oc describe pod wa-etcd-0 |grep scc` command, you get an output similar to the following example:

```text
openshift.io/scc: restricted
```
{: screen}

### Unable to collect logs with a webhook
{: #troubleshoot-40x-collect-logs-webhook}

The following fix applies to all versions of {{site.data.keyword.assistant_classic_short}} 4.0.x. If you're unable to collect logs with a webhook, it might be because you are using a webhook that connects to a server that is using a self-signed certificate. If so, complete the following steps to import the certificate into the keystore so that you can collect logs with a webhook:

1. Log in to cluster and `oc project cpd-instance`, which is the namespace where the instance is located.

1. Run the following command. In the following command, replace `INSTANCE_NAME` with the name of your instance and replace `CUSTOM_CERTIFICATE` with your Base64 encoded custom certificate key:

    ```bash
    INSTANCE="INSTANCE_NAME"     # Replace INSTANCE_NAME with the name of the Watson Assistant instance
    CERT="CUSTOM_CERTIFICATE"     # Replace CUSTOM_CERTIFICATE with the custom certificate key

    cat <<EOF | oc apply -f -
    apiVersion: v1
    data:
      ca_cert: ${CERT}
    kind: Secret
    metadata:
      name: ${INSTANCE}-custom-webhooks-cert
    type: Opaque
    ---
    apiVersion: assistant.watson.ibm.com/v1
    kind: TemporaryPatch
    metadata:
      name: ${INSTANCE}-add-custom-webhooks-cert
    spec:
      apiVersion: assistant.watson.ibm.com/v1
      kind: WatsonAssistantStore
      name: ${INSTANCE}
      patchType: patchStrategicMerge
      patch:
        webhooks-connector:
          deployment:
            spec:
              template:
                spec:
                  containers:
                  - name: webhooks-connector
                    env:
                    - name: CERTIFICATES_IMPORT_LIST
                      value: /etc/secrets/kafka/ca.pem:kafka_ca,/etc/secrets/custom/ca.pem:custom_ca
                    volumeMounts:
                    - mountPath: /etc/secrets/custom
                      name: custom-cert
                      readOnly: true
                  volumes:
                  - name: custom-cert
                    secret:
                      defaultMode: 420
                      items:
                      - key: ca_cert
                        path: ca.pem
                      secretName: ${INSTANCE}-custom-webhooks-cert
    EOF
    ```
    {: codeblock}

1. Wait approximately 10 minutes for the `wa-webhooks-connector` pod to restart. This pod restarts automatically.

1. After the pod restarts, check the logs by running the following command. In the command, replace `XXXX` with the suffix of the `wa-webhooks-connector` pod:

    ```bash
    oc logs wa-webhooks-connector-XXXX     // Replace XXXX with the suffix of the wa-webhooks-connector pod
    ```
    {: codeblock}

    After you run this command, you should see two lines similar to the following example at the beginning of the log:

    ```text
    Certificate was added to keystore
    Certificate was added to keystore
    ```
    {: screen}

    When you see these two lines, then the custom certificate was properly imported into the keystore.

## 4.0.5
{: #troubleshoot-405}

### Install Redis if foundational services version is higher than 3.14.1
{: #troubleshoot-405-install-redis-foundational-services}

If you are installing the Redis operator with an IBM Cloud Pak foundational services version higher than 3.14.1, the Redis operator might get stuck in `Pending` status. If you have an air-gapped cluster, complete the steps in the [Air-gapped cluster](#troubleshoot-405-install-redis-foundational-services-air-gapped) section to resolve this issue. If you are using the IBM Entitled Registry, complete the steps in the [IBM Entitled Registry](#troubleshoot-405-install-redis-foundational-services-entitled-registry) section to resolve this issue.

#### Air-gapped cluster
{: #troubleshoot-405-install-redis-foundational-services-air-gapped}

1. Check the status of the Redis operator:

    ```bash
    oc get opreq common-service-redis -n ibm-common-services -o jsonpath='{.status.phase}  {"\n"}'
    ```
    {: codeblock}

1. If the Redis operand request is stuck in `Pending` status, delete the operand request:

    ```bash
    oc delete opreq watson-assistant-redis -n ibm-common-services
    ```
    {: codeblock}

1. Set up your environment to download the CASE packages.

   1. Create the directories where you want to store the CASE packages:

      ```bash
      mkdir -p $HOME/offline/cpd  
      mkdir -p $HOME/offline/cpfs  
      ```
      {: codeblock}

   1. Set the following environment variables:

       ```bash
       export CASE_REPO_PATH=https://github.com/IBM/cloud-pak/raw/master/repo/case  
       export OFFLINEDIR=$HOME/offline/cpd  
       export OFFLINEDIR_CPFS=$HOME/offline/cpfs  
       ```
       {: codeblock}

1. Download the Redis operator and {{site.data.keyword.icp4dfull}} platform operator CASE packages:

    ```bash
    cloudctl case save \
    --repo ${CASE_REPO_PATH} \
    --case ibm-cloud-databases-redis \
    --version  1.4.5  \
    --outputdir $OFFLINEDIR

    cloudctl case save \
    --repo ${CASE_REPO_PATH} \
    --case ibm-cp-datacore \
    --version 2.0.10 \
    --outputdir ${OFFLINEDIR} \
    --no-dependency
    ```
    {: codeblock}

1. Create the Redis catalog source:

    ```bash
    cloudctl case launch \
    --case ${OFFLINEDIR}/ibm-cloud-databases-redis-1.4.5.tgz \
    --inventory redisOperator \
    --action install-catalog \
    --namespace openshift-marketplace \
    --args "--registry icr.io --inputDir ${OFFLINEDIR} --recursive"
    ```
    {: codeblock}

1. Set the environment variables for your registry credentials:

    ```bash
    export PRIVATE_REGISTRY_USER=username  
    export PRIVATE_REGISTRY_PASSWORD=password  
    export PRIVATE_REGISTRY={registry-info}  
    ```
    {: codeblock}

1. Run the following command to store the credentials:

    ```bash
    cloudctl case launch \
    --case ${OFFLINEDIR}/ibm-cp-datacore-2.0.10.tgz \
    --inventory cpdPlatformOperator \
    --action configure-creds-airgap \
    --args "--registry ${PRIVATE_REGISTRY} --user ${PRIVATE_REGISTRY_USER} --pass ${PRIVATE_REGISTRY_PASSWORD}"
    ```
    {: codeblock}

1. Mirror the images:

    ```bash
    export USE_SKOPEO=true  
    cloudctl case launch \
    --case ${OFFLINEDIR}/ibm-cp-datacore-2.0.10.tgz \
    --inventory cpdPlatformOperator \
    --action mirror-images \
    --args "--registry ${PRIVATE_REGISTRY} --user ${PRIVATE_REGISTRY_USER} --pass ${PRIVATE_REGISTRY_PASSWORD} --inputDir ${OFFLINEDIR}"
    ```
    {: codeblock}

1. Create the Redis subscription.

    1. Export the project that contains the {{site.data.keyword.icp4dfull}} operator:

       ```bash
       export OPERATOR_NS=ibm-common-services|cpd-operators     # Select the project that contains the Cloud Pak for Data operator
       ```
       {: codeblock}

    1. Create the subscription:

       ```bash
       cat <<EOF | oc apply --namespace $OPERATOR_NS -f -
       apiVersion: operators.coreos.com/v1alpha1
       kind: Subscription
       metadata:
         name: ibm-cloud-databases-redis-operator
       spec:
         name: ibm-cloud-databases-redis-operator
         source: ibm-cloud-databases-redis-operator-catalog
         sourceNamespace: openshift-marketplace
       EOF
       ```
       {: codeblock}

#### IBM Entitled Registry
{: #troubleshoot-405-install-redis-foundational-services-entitled-registry}

1. Check the status of the Redis operator:

    ```bash
    oc get opreq common-service-redis -n ibm-common-services -o jsonpath='{.status.phase}  {"\n"}'

    ```
    {: codeblock}

1. If the Redis operand request is stuck in `Pending` status, delete the operand request:

    ```bash
    oc delete opreq watson-assistant-redis -n ibm-common-services
    ```
    {: codeblock}

1. Create the Redis subscription. Create one of the following two subscriptions, depending on whether you are using.

    1. Export the project that contains the {{site.data.keyword.icp4dfull}} operator:

       ```bash
       export OPERATOR_NS=ibm-common-services|cpd-operators     # Select the project that contains the Cloud Pak for Data operator
       ```
       {: codeblock}

    1. Create the subscription. Choose one of the following two subscriptions, depending on how you are using the IBM Entitled Registry:

       - IBM Entitled Registry from the `ibm-operator-catalog`:
       
          ```bash
          cat <<EOF | oc apply --namespace  $OPERATOR_NS -f -
          apiVersion: operators.coreos.com/v1alpha1
          kind: Subscription
          metadata:
             name: ibm-cloud-databases-redis-operator
          spec:
             name: ibm-cloud-databases-redis-operator
             source: ibm-operator-catalog
             sourceNamespace: openshift-marketplace
          EOF
          ```
          {: codeblock}

       - IBM Entitled Registry with catalog sources that pull specific versions of the images:
    
          ```bash
          cat <<EOF | oc apply --namespace $OPERATOR_NS -f -
          apiVersion: operators.coreos.com/v1alpha1
          kind: Subscription
          metadata:
             name: ibm-cloud-databases-redis-operator
          spec:
             name: ibm-cloud-databases-redis-operator
             source: ibm-cloud-databases-redis-operator-catalog
             sourceNamespace: openshift-marketplace
          EOF
          ```
          {: codeblock}

1. Validate that the operator was successfully created.

   1. Run the following command to confirm that the subscription was applied:
   
      ```bash
      oc get sub -n $OPERATOR_NS  ibm-cloud-databases-redis-operator -o jsonpath='{.status.installedCSV} {"\n"}'
      ```
      {: codeblock}
      
   1. Run the following command to confirm that the operator is installed:
   
      ```bash
      oc get pod -n $OPERATOR_NS -l app.kubernetes.io/name=ibm-cloud-databases-redis-operator \
      -o jsonpath='{.items[0].status.phase} {"\n"}'
      ```
      {: codeblock}

## 4.0.4
{: #troubleshoot-404}

### Integrations image problem on air-gapped installations
{: #troubleshoot-404-integrations-image-air-gapped}

If your installation is air-gapped, your integrations image fails to properly start.

If the installation uses the IBM Entitled Registry to pull images, complete the steps in the **IBM Entitled Registry** section. If the installation uses a private Docker registry to pull images, complete the steps in the **Private Docker registry** section.

#### IBM Entitled Registry
{: #troubleshoot-404-entitled-registry}

If your installation uses the IBM Entitled Registry to pull images, complete the following steps to add an override entry to the CR:

1. Get the name of your instance by running the following command:

   ```bash
   oc get wa
   ```
   {: codeblock}

1. Edit and save the CR.

   1. Run the following command to edit the CR. In the command, replace `INSTANCE_NAME` with the name of the instance:
   
      ```bash
      oc edit wa INSTANCE_NAME
      ```
      {: codeblock}
       
   1. Edit the CR by adding the following lines:
   
      ```bash
      appConfigOverrides:
         container_images:
         integrations:
            image: cp.icr.io/cp/watson-assistant/servicedesk-integration
            tag: 20220106-143142-0ea3fbf7-wa_icp_4.0.5-signed@sha256:7078fdba4ab0b69dbb93f47836fd9fcb7cfb12f103662fef0d9d1058d2553910
      ```
      {: codeblock}

1. Wait for the operator to pick up the change and start a new integrations pod. This might take up to 10 minutes.

1. After the new integrations pod starts, the old pod terminates. When the new pod starts, the server starts locally and the log looks similar to the following example:

    ```text
    oc logs -f ${INTEGRATIONS_POD}
    [2022-01-07T01:33:13.609] [OPTIMIZED] db.redis.RedisManager - Redis trying to connect. counter# 1
    [2022-01-07T01:33:13.628] [OPTIMIZED] db.redis.RedisManager - Redis connected
    [2022-01-07T01:33:13.629] [OPTIMIZED] db.redis.RedisManager - Redis is ready to serve!
    [2022-01-07T01:33:14.614] [OPTIMIZED] Server - Server started at: https://localhost:9449
    ```
    {: screen}

#### Private Docker registry
{: #troubleshoot-404-private-docker}

If your installation uses a private Docker registry to pull images, complete the following steps to download and push the new integrations image to your private Docker registry and add an override entry to the CR:

1. Edit the CSV file to add the new integrations image.

   1. Run the following command to open the CSV file:
    
      ```bash
      vi $OFFLINEDIR/ibm-watson-assistant-4.0.4-images.csv
      ```
      {: codeblock}

   1. Add the following line to the CSV file immediately after the existing integrations image:
   
      ```bash
      cp.icr.io,cp/watson-assistant/servicedesk-integration,20220106-143142-0ea3fbf7-wa_icp_4.0.5-signed,sha256:7078fdba4ab0b69dbb93f47836fd9fcb7cfb12f103662fef0d9d1058d2553910,IMAGE,linux,x86_64,"",0,CASE,"",ibm_wa_4_0_0;ibm_wa_4_0_2;ibm_wa_4_0_4;vLatest
      ```
      {: codeblock}

1. Mirror the image again by using the commands that you used to download and push all the images, for example:

    ```bash
    cloudctl case launch \
      --case ${OFFLINEDIR}/ibm-cp-datacore-2.0.9.tgz \
      --inventory cpdPlatformOperator \
      --action configure-creds-airgap \
      --args "--registry cp.icr.io --user cp --pass $PRD_ENTITLED_REGISTRY_APIKEY --inputDir ${OFFLINEDIR}"
    ```
    {: codeblock}

1. Get the name of your instance by running the following command:

    ```bash
    oc get wa
    ```
    {: codeblock}

1. Edit and save the CR.

   1. Run the following command to edit the CR. In the command, replace `INSTANCE_NAME` with the name of the instance:
   
      ```bash
      oc edit wa INSTANCE_NAME
      ```
      {: codeblock}

   1. Edit the CR by adding the following lines:
   
      ```bash
      appConfigOverrides:
         container_images:
         integrations:
            image: cp.icr.io/cp/watson-assistant/servicedesk-integration
            tag: 20220106-143142-0ea3fbf7-wa_icp_4.0.5-signed@sha256:7078fdba4ab0b69dbb93f47836fd9fcb7cfb12f103662fef0d9d1058d2553910
      ```
      {: codeblock}

1. Wait for the operator to pick up the change and start a new integrations pod. This might take up to 10 minutes.

1. After the new integrations pod starts, the old pod terminates. When the new pod starts, the server starts locally and the log looks similar to the following example:

    ```bash
    oc logs -f ${INTEGRATIONS_POD}
    [2022-01-07T01:33:13.609] [OPTIMIZED] db.redis.RedisManager - Redis trying to connect. counter# 1
    [2022-01-07T01:33:13.628] [OPTIMIZED] db.redis.RedisManager - Redis connected
    [2022-01-07T01:33:13.629] [OPTIMIZED] db.redis.RedisManager - Redis is ready to serve!
    [2022-01-07T01:33:14.614] [OPTIMIZED] Server - Server started at: https://localhost:9449
    ```
    {: codeblock}

## 4.0.0
{: #troubleshoot-400}

### Install {{site.data.keyword.assistant_classic_short}} 4.0.0 with EDB version 1.8
{: #troubleshoot-400-install-edb18}

Complete this task only if you need a fresh installation of {{site.data.keyword.assistant_classic_short}} 4.0.0. Do not complete this task on existing clusters with data. Completing this task on an existing cluster with data results in data loss.
{: important}

If you upgraded to EDB version 1.8 and need a new installation of {{site.data.keyword.assistant_classic_short}} 4.0.0, complete the following steps. In the following steps, `wa` is used as the name of the custom resource. Replace this value with the name of your custom resource:

1. First, apply the following patch:

    ```bash
    cat <<EOF | oc apply -f -
    apiVersion: assistant.watson.ibm.com/v1
    kind: TemporaryPatch
    metadata:
      name: wa-postgres-180-hotfix
    spec:
      apiVersion: assistant.watson.ibm.com/v1
      kind: WatsonAssistantStore
      name: wa     # Specify the name of your custom resource
      patchType: patchStrategicMerge
      patch:
        postgres:
          postgres:
            spec:
              bootstrap:
                initdb:
                  options:
                   - "--encoding=UTF8"
                   - "--locale=en_US.UTF-8"
                   - "--auth-host=scram-sha-256"
    EOF
    ```
    {: codeblock}

1. Run the following command to check that the temporary patch is applied to the `WatsonAssistantStore` custom resource. It might take up to 10 minutes after the store custom resource is updated:

    ```bash
    oc get WatsonAssistantStore wa -o jsonpath='{.metadata.annotations.oppy\.ibm\.com/temporary-patches}' ; echo
    ```
    {: codeblock}

    If the patch is applied, the command returns output similar to the following example:

    ```bash
    {"wa-postgres-180-hotfix": {"timestamp": "2021-09-23T15:48:12.071497", "api_version": "assistant.watson.ibm.com/v1"}}`
    ```
    {: screen}

1. Run the following command to delete the Postgres instance:

    ```bash
    oc delete clusters.postgresql.k8s.enterprisedb.io wa-postgres
    ```
    {: codeblock}

1. Wait 10 minutes. Then, run the following command to check the Postgres instance:

    ```bash
    oc get pods | grep wa-postgres
    ```
    {: codeblock}

    When the Postgres instance is running properly, the command returns output similar to the following example:

    ```text
    wa-postgres-1                                                     1/1     Running     0          37m
    wa-postgres-2                                                     1/1     Running     0          36m
    wa-postgres-3                                                     1/1     Running     0          36m
    ```
    {: screen}

1. Run the following command to check that the jobs that initialize the Postgres database completed successfully:

    ```bash
    oc get jobs wa-create-slot-store-db-job wa-4.0.0-update-schema-store-db-job
    ```
    {: codeblock}

    When the jobs complete successfully, the command returns output similar to the following example:

    ``` text
    NAME                                  COMPLETIONS   DURATION   AGE
    wa-create-slot-store-db-job           1/1           3s         31m
    wa-4.0.0-update-schema-store-db-job   1/1           13s        31m
    ```
    {: screen}

    If the jobs don't complete successfully, then they timed out and need to be re-created. Delete the jobs by running the `oc delete jobs wa-create-slot-store-db-job wa-4.0.0-update-schema-store-db-job` command. The jobs are re-created after 10 minutes by the operator.

For information about upgrading from {{site.data.keyword.assistant_classic_short}} 4.0.0 to {{site.data.keyword.assistant_classic_short}} 4.0.2, see [Upgrading {{site.data.keyword.assistant_classic_short}} to a newer 4.0 refresh](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=assistant-upgrading-watson-version-40){: external}.

## 1.5.0
{: #troubleshoot-150}

### Search skill not working because of custom certificate
{: #troubleshoot-150-search-skill}

The search skill, which is the integration with the {{site.data.keyword.discoveryfull}} service, might not work if you [configured a custom TLS certificate](https://www.ibm.com/docs/en/cloud-paks/cp-data/3.5.0?topic=client-using-custom-tls-certificate){: external} in {{site.data.keyword.icp4dfull}}. If the custom certificate is not signed by a well-known certificate authority (CA), the search skill does not work as expected. You might also see errors in the **Try out** section of the search skill.

#### Validate the issue
{: #troubleshoot-150-search-skill-validate}

First, check the logs of the search skill pods to confirm whether this issue applies to you.

1. Run the following command to list the search skill pods:

    ```bash
    oc get pods -l component=skill-search
    ```
    {: codeblock}

1. Run the following command to check the logs for the following exception:

    ```bash
    oc logs -l component=skill-search | grep "IBMCertPathBuilderException"
    ```
    {: codeblock}

    The error looks similar to the following example:

    ```text
    {"level":"ERROR","logger":"wa-skills","message":"Search skill exception","exception":[{"message":"com.ibm.jsse2.util.h: PKIX path building failed: com.ibm.security.cert.IBMCertPathBuilderException: unable to find valid certification path to requested target","name":"SSLHandshakeException"}]}
    ```
    {: screen}

    If you see this error, continue to follow the steps to apply the fix.

#### Apply the fix
{: #troubleshoot-150-search-skill-fix}

To fix the search skill, you inject the CA that signed your TLS certificate into the Java truststore that is used by the search skill. The search skill pods are then able to validate your certificate and communicate with the {{site.data.keyword.discoveryfull}} service.

1. First, get your certificate. You might have this certificate, but in these steps you can retrieve the certificate directly from the cluster.

    1. Run the following command to check that the secret exists:
    
       ```bash
       oc get secret external-tls-secret
       ```
       {: codeblock}

    1. Run the following command to retrieve the certificate chain from the secret:
    
       ```bash
       oc get secret external-tls-secret --output jsonpath='{.data.cert\.crt}' | base64 -d | tee ingress_cert_chain.crt
       ```
       {: codeblock}

    1. Extract the CA certificate. 
    
       The `ingress_cert_chain.crt` file typically contains multiple certificates. The last certificate in the file is usually your CA certificate. 
    
    1. Copy the last certificate block that begins with `-----BEGIN CERTIFICATE-----` and ends with `-----END CERTIFICATE-----`. 
    
    1. Save this certificate in the `ingress_ca.crt` file. When you save the `ingress_ca.crt` file, the `-----BEGIN CERTIFICATE-----` line must be the first line of the file, and the `-----END CERTIFICATE-----` line must be the last line of the file.

1. Retrieve the truststore that is used by the search skill pods.

   1. Run the following command to list the search skill pods:
   
      ```bash
      oc get pods -l component=skill-search
      ```
      {: codeblock}

   1. Run the following command to set the `SEARCH_SKILL_POD` environment variable with the search skill pod name:
    
      ```bash
      SEARCH_SKILL_POD="$(oc get pods -l component=skill-search --output custom-columns=NAME:.metadata.name --no-headers | head -n 1
      ```
      {: codeblock}

   1. Run the following command to see the selected pod:
   
      ```bash
      echo "Selected search skill pod: ${SEARCH_SKILL_POD}"
      ```
      {: codeblock}

   1. Retrieve the truststore file. The `cacerts` file is the default truststore that is used by Java. It contains the list of the certificate authorities that Java trusts by default. Run the following command to copy the binary `cacerts` file from the pod into your current directory:
   
      ```bash
      oc cp ${SEARCH_SKILL_POD}:/opt/ibm/java/jre/lib/security/cacerts cacerts
      ```
      {: codeblock}

1. Run the following command to inject the `ingress_ca.crt` file into the `cacerts` file:

      ```bash
      keytool -import -trustcacerts -keystore cacerts -storepass changeit -alias customer_ca -file ingress_ca.crt
      ```
      {: codeblock}
      
      You can run the `keytool -list -keystore cacerts -storepass changeit | grep customer_ca -A 1` command to check that your CA certificate is included in the `cacerts` file.
      {: tip}

1. Run the following command to create the configmap that contains the updated `cacerts` file:

   ```bash
   oc create configmap watson-assistant-skill-cacerts --from-file=cacerts
   ```
   {: codeblock}
   
   Because the `cacerts` file is binary, the output of the `oc describe configmap watson-assistant-skill-cacerts` command shows an empty data section. To check whether the updated `cacerts` file is present in the configmap, run the `oc get configmap watson-assistant-skill-cacerts --output yaml` command.

1. Override the `cacerts` file in the search skill pods. In this step, you configure the operator to override the `cacerts` file in the search skill pods with the updated `cacerts` file. In the following example file, the instance is called `watson-assistant---wa`. Replace this value with the name of your instance:

   ```bash
   cat <<EOF | oc apply -f -
   kind: TemporaryPatch
   apiVersion: com.ibm.oppy/v1
   metadata:
      name: watson-assistant---wa-skill-cert
   spec:
      apiVersion: com.ibm.watson.watson-assistant/v1
      kind: WatsonAssistantSkillSearch
      name: "watson-assistant---wa"    # Replace this with the name of your Watson Assistance instance
      patchType: patchStrategicMerge
      patch:
          "skill-search":
            deployment:
               spec:
                  template:
                     spec:
                        volumes:
                           - name: updated-cacerts
                              configMap:
                                 name: watson-assistant-skill-cacerts
                                 defaultMode: 420
                        containers:
                        - name: skill-search
                           volumeMounts:
                           - name: updated-cacerts
                              mountPath: /opt/ibm/java/jre/lib/security/cacerts
                              subPath: cacerts
   EOF
   ```  
   {: codeblock}

1. Wait until new search skill pods are created. It might take up to 10 minutes before the updates take effect.

1. Check that the search skill feature is working as expected.

### Disable Horizontal Pod Autoscaling and set a maximum number of master pods
{: #troubleshoot-150-disable-hpa}

Horizontal Pod Autoscaling (HPA) is enabled automatically. As a result, the number of replicas changes dynamically in the range of 1 to 10 replicas. You can disable HPA if you want to limit the maximum number of master pods or if you're concerned about master pods being created and deleted too frequently.

1. Disable HPA for the `master` microservice by running the following command. In these steps, substitute your instance name for the `INSTANCE_NAME` variable:

    ```bash
    oc patch wa ${INSTANCE_NAME} --type='json' --patch='[{"op": "add", "path": "/appConfigOverrides/clu", "value":{"master":{"autoscaling":{"enabled":false}}}}]'
    ```
    {: codeblock}

1. Wait until the information propagates into the operator:

    ```text
    sleep 600
    ```
    {: screen}

1. Run the following command to remove HPA for the `master` microservice:

    ```bash
    oc delete hpa ${INSTANCE_NAME}-master
    ```
    {: codeblock}

1. Wait for about 30 seconds:

    ```text
    sleep 30
    ```
    {: screen}

1. Scale down the `master` microservice to the number of replicas that you want. In the following example, the `master` microservice is scaled down to two replicas:

    ```bash
    oc scale deploy ${INSTANCE_NAME}-master --replicas=2
    ```
    {: codeblock}

### cpd-watson-assistant-1.5.0-patch-1
{: #troubleshoot-150-patch}

[cpd-watson-assistant-1.5.0-patch-1](https://www.ibm.com/support/pages/node/6240164){: external} is available for installations of version 1.5.0.

This patch includes:

- Configuration changes for FIPS compatibility
- A fix for a blank screen issue that occurred when selecting multiple items in the UI
- An update to resolve a localStorage issue when developing in Google Chrome
- A fix for a scrolling issue

#### Resizing the Redis statefulset memory and cpu values after applying patch 1 for 1.5.0
{: #troubleshoot-150-patch-resize-redis}

Here are steps to resize Redis statefulset memory and cpu values after applying [cpd-watson-assistant-1.5.0-patch-1](https://www.ibm.com/support/pages/node/6240164){: external}.

1. Use `oc get wa` to see your instance name:

    ```bash
    oc get wa
    NAME                       VERSION   READY   READYREASON   UPDATING   UPDATINGREASON   DEPLOYED   VERIFIED   AGE
    watson-assistant---wa-qa   1.5.0     True    Stable        False      Stable           18/18      18/18      11h
    ```
    {: codeblock}

1. Export your instance name as a variable that you can use in each step, for example:

    ```bash
    export INSTANCENAME=watson-assistant---wa-qa
    ```
    {: codeblock}

1. Change the `updateStrategy` in both Redis statefulsets to type `RollingUpdate`:

    ```bash
    oc patch statefulset c-$INSTANCENAME-redis-m -p '{"spec":{"updateStrategy":{"type":"RollingUpdate"}}}'
    oc patch statefulset c-$INSTANCENAME-redis-s -p '{"spec":{"updateStrategy":{"type":"RollingUpdate"}}}'
    ```
    {: codeblock}

1. Update the Redis statefulsets with the resized cpu and memory values:

   - Member CPU

      ```bash
      oc patch statefulset c-$INSTANCENAME-redis-m --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/resources/requests/cpu", "value":"50m"},{"op": "replace", "path": "/spec/template/spec/containers/1/resources/requests/cpu", "value":"50m"},{"op": "replace", "path": "/spec/template/spec/containers/2/resources/requests/cpu", "value":"50m"},{"op": "replace", "path": "/spec/template/spec/containers/3/resources/requests/cpu", "value":"50m"}]'
      ```
      {: codeblock}

   - Member memory
   
      ```bash
      oc patch statefulset c-$INSTANCENAME-redis-m --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/1/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/2/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/3/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/0/resources/requests/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/1/resources/requests/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/2/resources/requests/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/3/resources/requests/memory", "value":"256Mi"}]'
      ```
      {: codeblock}
      
   - Sentinel CPU
   
      ```bash
      oc patch statefulset c-$INSTANCENAME-redis-s --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/resources/requests/cpu", "value":"50m"},{"op": "replace", "path": "/spec/template/spec/containers/1/resources/requests/cpu", "value":"50m"},{"op": "replace", "path": "/spec/template/spec/containers/2/resources/requests/cpu", "value":"50m"},{"op": "replace", "path": "/spec/template/spec/containers/3/resources/requests/cpu", "value":"50m"}]'
      ```
      {: codeblock}

   - Sentinel memory
   
      ```bash
      oc patch statefulset c-$INSTANCENAME-redis-s --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/1/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/2/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/3/resources/limits/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/0/resources/requests/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/1/resources/requests/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/2/resources/requests/memory", "value":"256Mi"},{"op": "replace", "path": "/spec/template/spec/containers/3/resources/requests/memory", "value":"256Mi"}]'
      ```
      {: codeblock}

1. Confirm that the Redis member and sentinel pods have the new memory and cpu values, for example:

   ```      
   oc describe pod c-$INSTANCENAME-redis-m-0 |grep cpu
   oc describe pod c-$INSTANCENAME-redis-m-0 |grep memory
   oc describe pod c-$INSTANCENAME-redis-s-0 |grep cpu
   oc describe pod c-$INSTANCENAME-redis-s-0 |grep memory
   ```
   {: codeblock}

1. The results should look like these examples:

      ```text
      oc describe sts c-$INSTANCENAME-redis-m |grep cpu
                            {"m":{"db":{"limits":{"cpu":"4","memory":"256Mi"},"requests":{"cpu":"25m","memory":"256Mi"}},"mgmt":{"limits":{"cpu":"2","memory":"100Mi"}...
            cpu:     4
            cpu:     50m
            cpu:     2
            cpu:     50m
            cpu:     2
            cpu:      50m
            cpu:     2
            cpu:     50m
      ```
      {: screen}

      ```text
      oc describe sts c-$INSTANCENAME-redis-m |grep memory
                            {"m":{"db":{"limits":{"cpu":"4","memory":"256Mi"},"requests":{"cpu":"25m","memory":"256Mi"}},"mgmt":{"limits":{"cpu":"2","memory":"100Mi"}...
            memory:  256Mi
            memory:  256Mi
            memory:  256Mi
            memory:  256Mi
            memory:  256Mi
            memory:   256Mi
            memory:  256Mi
            memory:  256Mi
      ```
      {: screen}

      ```text
      oc describe pod c-$INSTANCENAME-redis-s-0 |grep cpu
                      {"m":{"db":{"limits":{"cpu":"4","memory":"256Mi"},"requests":{"cpu":"25m","memory":"256Mi"}},"mgmt":{"limits":{"cpu":"2","memory":"100Mi"}...
            cpu:     2
            cpu:     50m
            cpu:     2
            cpu:     50m
            cpu:     2
            cpu:      50m
            cpu:     2
            cpu:     50m
      ```
      {: screen}

      ```text
      oc describe pod c-$INSTANCENAME-redis-s-0 |grep memory
                      {"m":{"db":{"limits":{"cpu":"4","memory":"256Mi"},"requests":{"cpu":"25m","memory":"256Mi"}},"mgmt":{"limits":{"cpu":"2","memory":"100Mi"}...
            memory:  256Mi
            memory:  256Mi
            memory:  256Mi
            memory:  256Mi
            memory:  256Mi
            memory:   256Mi
            memory:  256Mi
            memory:  256Mi
      ```
      {: screen}

1. Change the `updateStrategy` in both Redis statefulsets back to type `OnDelete`:

    ```bash
    oc patch statefulset c-$INSTANCENAME-redis-m -p '{"spec":{"updateStrategy":{"type":"OnDelete"}}}'
    oc patch statefulset c-$INSTANCENAME-redis-s -p '{"spec":{"updateStrategy":{"type":"OnDelete"}}}'
    ```
    {: codeblock}

### Delete the pdb (poddisruptionbudgets) when changing the deployment from medium to small
{: #troubleshoot-delete-pdb}

Whenever the deployment size is changed from medium to small. A manual step is required to delete the `poddisruptionbudgets` that are created for medium instances.

Run the following command, replacing `<instance-name>` with the name of your CR instance and replacing `<namespace-name>` with the name of the namespace where the instance resides.

```bash
oc delete pdb  -l icpdsupport/addOnId=assistant,component!=etcd,ibmevents.ibm.com/kind!=Kafka,app.kubernetes.io/instance=<instance-name> -n <namespace-name>
```
{: codeblock}
