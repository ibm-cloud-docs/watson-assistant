---

copyright:
  years: 2015, 2025
lastupdated: "2025-11-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data for {{site.data.keyword.IBM_notm}} On-premises
{: #backup-data}

[{{site.data.keyword.icp4dfull_notm}}]{: tag-cp4d} [{{site.data.keyword.IBM_notm}} Software Hub]{: tag-teal}

You can back up and restore the data that is associated with your installation in {{site.data.keyword.IBM_notm}} On-premises.
{: shortdesc}

The following table lists the upgrade paths that are supported by the scripts.


| Version in use | Version that you can upgrade to |
|------|-----|
| 5.0.x | 5.1.x |
| 4.8.x | 5.0.x or 5.1.x|
| 4.7.x | 4.8.x or 5.0.x |
| 4.6.x | 4.7.x or 4.8.x |
| 4.5.x | 4.6.x or 4.7.x |
| 4.0.x | 4.5.x or 4.6.x
{: caption="Upgrade paths supported by scripts" caption-side="top"}

Simpler ways to complete the upgrade is described in the following topics:

- [Upgrading {{site.data.keyword.conversationshort}} to Version 5.1.x](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=assistant-upgrading){: external}
- [Upgrading {{site.data.keyword.conversationshort}} to Version 5.0.x](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=assistant-upgrading){: external}
- [Upgrading {{site.data.keyword.conversationshort}} to Version 4.8.x](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x?topic=assistant-upgrading){: external}
- [Upgrading {{site.data.keyword.conversationshort}} to Version 4.7.x](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=assistant-upgrading){: external}
- [Upgrading {{site.data.keyword.conversationshort}} to Version 4.6.x](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=assistant-upgrading){: external}

If you are upgrading from 4.6.4 or earlier to the latest version, you must upgrade to 4.6.5 before you upgrade to the latest release.{: important}

The primary data storage is a {{site.data.keyword.postgresql}} database.


Choose one of the following ways to manage the back up of data:

- **[Kubernetes CronJob](#backup-cronjob)**: Use the `$INSTANCE-store-cronjob` cron job that is provided for you.
- **[backupPG.sh script](#backup-os)**: Use the `backupPG.sh` bash script.
- **[pg_dump tool](#backup-cp4d)**: Run the `pg_dump` tool on each cluster directly. This is a manual option that gives you control over the process.

When you back up data with one of these procedures before you upgrade from one version to another, the workspace IDs of your skills are preserved, but the service instance IDs and credentials change.
{: note}

## Before you begin
{: #backup-begin}

- When you create a backup by using this procedure, the backup includes all of the assistants and skills from all of the service instances. It can include skills and assistants to which you do not have access.
- The access permissions information of the original service instances is not stored in the backup. Meaning original access rights, which determine who can see a service instance and who cannot, are not preserved.
- You cannot use this procedure to back up the data that is returned by the search integration. Data that is retrieved by the search integration comes from a data collection in a {{site.data.keyword.discoveryshort}} instance. See the [{{site.data.keyword.discoveryshort}} documentation](/docs/discovery-data?topic=discovery-data-backup-restore){: external} to find out how to back up its data.
- If you back up and restore or otherwise change the {{site.data.keyword.discoveryshort}} service that your search integration connects to, then you cannot restore the search integration, but must re-create it. When you set up a search integration, you map sections of the assistant's response to fields in a data collection that is hosted by an instance of {{site.data.keyword.discoveryshort}} on the same cluster. If the {{site.data.keyword.discoveryshort}} instance changes, your mapping to it is broken. If your {{site.data.keyword.discoveryshort}} service does not change, then the search integration can continue to connect to the data collection.
- The tool that restores the data clears the current database before it restores the backup. Therefore, if you might need to revert to the current database, create a backup of it first.
- The target {{site.data.keyword.icp4dfull_notm}} cluster where you restore the data must have the same number of provisioned service instances as the environment from which you back up the database. To verify in the {{site.data.keyword.icp4dfull_notm}} web client, select **Services** from the main navigation menu, select **Instances**, and then open the **Provisioned instances** tab. If more than one user created instances, then ask the other users who created instances to log in and check the number that they created. You can then add up the total sum of instances for your deployment. Not even an administrative user can see instances that were created by others from the web client user interface.

## Backing up data by using the CronJob
{: #backup-cronjob}

A CronJob named `$INSTANCE-store-cronjob` is created and enabled for you automatically when you deploy the service. A CronJob is a type of Kubernetes controller. A CronJob creates Jobs on a repeating schedule. For more information, see [CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/){: external} in the Kubernetes documentation.


The store CronJob creates the `$INSTANCE-backup-job-$TIMESTAMP` jobs. Each `$INSTANCE-backup-job-$TIMESTAMP` job deletes old logs and runs a backup of the store {{site.data.keyword.postgresql}} database. {{site.data.keyword.postgresql}} provides a `pg_dump` tool that creates a backup. To create a backup, the `pg_dump` tool sends the database contents to `stdout`, which you can then write to a file. The` pg_dump` tool creates the backups with the `pg_dump` command and stores them in a persistent volume claim (PVC) named `$INSTANCE-store-db-backup-pvc`.


You are responsible for moving the backup to a more secure location after its initial creation, preferably a location that can be accessed outside of the cluster where the backups cannot be deleted easily. Ensure this happens for all environments, especially for Production clusters.
{: note}

The following table lists the configuration values that control the backup cron job. You can edit these settings by editing the cron job after the service is deployed by using the `oc edit cronjob $INSTANCE-store-cronjob` command.

| Variable | Description | Default value |
|----------|-------------|---------------|
| store.backup.suspend | If True, the cron job does not create any backup jobs. | `False` |
| store.backup.schedule | Specifies the time of day at which to run the backup jobs. Specify the schedule by using a cron expression. For example, `{minute} {hour} {day} {month} {day-of-week}` where `{day-of-week}` is specified as `0`=Sunday, `1`=Monday, and so on. The default schedule is to run every day at 11 PM. | `0 23 * * *` |
| store.backup.history.jobs.success | The number of successful jobs to keep. | `30` |
| store.backup.history.jobs.failed | The number of failed jobs to keep in the job logs. | `10` |
| store.backup.history.files.weekly_backup_day | A day of the week is designated as the weekly backup day. 0=Sunday, 1=Monday, and so on. | `0` |
| store.backup.history.files.keep_weekly | The number of backups to keep that were taken on weekly_backup_day. | `4`  |
| store.backup.history.files.keep_daily | The number of backups to keep that were taken on all the other days of the week. | `6`  |
{: caption="Cron job variables" caption-side="top"}

### Accessing backed-up files from Portworx
{: #backup-access-portworx}

To access the backup files from Portworx, complete the following steps:


1.  Get the name of the persistent volume that is used for the {{site.data.keyword.postgresql}} backup:


    ```bash
    oc get pv |grep $INSTANCE-store
    ```
    {: codeblock}

    This command returns the name of the persistent volume claim where the store backup is located, such as `pvc-d2b7aa93-3602-4617-acea-e05baba94de3`. The name is referred to later in this procedure as the `$pv_name`.

1.  Find nodes where Portworx is running:

    ```bash
    oc get pods -n kube-system -o wide -l name=portworx-api
    ```
    {: codeblock}

1.  Log in as the core user to one of the nodes where Portworx is running:

    ```bash
    ssh core@<node hostname>
    sudo su -
    ```
    {: codeblock}

1.  Make sure that the persistent volume is in a detached state and that no store backups are scheduled to occur during the time you plan to transfer the backup files.

    Remember, backups occur daily at 11 PM (in the time zone that is configured for the nodes) unless you change the schedule by editing the value of the `postgres.backup.schedule` configuration parameter. You can run the `oc get cronjobs` command to check the current schedule for the `$RELEASE-backup-cronjob` job. In the following command, `$pvc_node` is the name of the node that you discovered in the first step of this task:

    ```bash
    pxctl volume inspect $pv_name |head -40
    ```
    {: codeblock}

1.  Attach the persistent volume to the host:

    ```bash
    pxctl host attach $pv_name
    ```
    {: codeblock}

1.  Create a folder where you want to mount the node:

    ```bash
    mkdir /var/lib/osd/mounts/voldir
    ```
    {: codeblock}

1.  Mount the node:

    ```bash
    pxctl host mount $pv_name --path /var/lib/osd/mounts/voldir
    ```
    {: codeblock}

1.  Change the directory to `/var/lib/osd/mounts/voldir`. Transfer backup files to a secure location. Afterward, exit the directory. Unmount the volume:

    ```bash
    pxctl host unmount --path /var/lib/osd/mounts/voldir $pv_name
    ```
    {: codeblock}

1.  Detach the volume from the host:

    ```bash
    pxctl host detach $pv_name
    ```
    {: codeblock}

1.  Make sure that the volume is in the detached state. Otherwise, subsequent backups fail:

    ```bash
    pxctl volume inspect $pv_name |head -40
    ```
    {: codeblock}

### Accessing backed-up files from Red Hat OpenShift Container Storage
{: #backup-access-ocs}

To access the backup files from Red Hat OpenShift Container Storage (OCS), complete the following steps:


1.  Create a volume snapshot of the persistent volume claim that is used for the {{site.data.keyword.postgresql}} backup:


    ```yaml
    cat <<EOF | oc apply -f -
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshot
    metadata:
      name: wa-backup-snapshot
    spec:
      source:
      

        persistentVolumeClaimName: ${INSTANCE_NAME}-store-db-backup-pvc

      
      volumeSnapshotClassName: ocs-storagecluster-rbdplugin-snapclass
    EOF
    ```
    {: codeblock}

1.  Create a persistent volume claim from the volume snapshot:

    ```yaml
    cat <<EOF | oc apply -f -
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: wa-backup-snapshot-pvc
    spec:
      storageClassName: ocs-storagecluster-ceph-rbd
      accessModes:
      - ReadWriteOnce
      volumeMode: Filesystem
      dataSource:
        apiGroup: snapshot.storage.k8s.io
        kind: VolumeSnapshot
        name: wa-backup-snapshot
      resources:
        requests:
          storage: 1Gi     
    EOF
    ```
    {: codeblock}

1.  Create a pod to access the persistent volume claim:

    ```yaml
    cat <<EOF | oc apply -f -
    kind: Pod
    apiVersion: v1
    metadata:
      name: wa-retrieve-backup
    spec:
      volumes:
        - name: backup-snapshot-pvc
          persistentVolumeClaim:
           claimName: wa-backup-snapshot-pvc
      containers:
        - name: retrieve-backup-container
          image: cp.icr.io/cp/watson-assistant/conan-tools:20210630-0901-signed@sha256:e6bee20736bd88116f8dac96d3417afdfad477af21702217f8e6321a99190278
          command: ['sh', '-c', 'echo The pod is running && sleep 360000']
          volumeMounts:
            - mountPath: "/watson_data"
              name: backup-snapshot-pvc
    EOF
    ```
    {: codeblock}

1.  If you do not know the name of the backup file that you want to extract and are unable to check the most recent backup cron job, run the following command:

    ```bash
    oc exec -it wa-retrieve-backup -- ls /watson_data
    ```
    {: codeblock}

1.  Transfer the backup files to a secure location:

    ```bash
    kubectl cp wa-retrieve-backup:/watson_data/${FILENAME} ${SECURE_LOCAL_DIRECTORY}/${FILENAME}
    ```
    {: codeblock}

1.  Run the following commands to clean up the resources that you created to retrieve the files:

    ```bash
    oc delete pod wa-retrieve-backup
    oc delete pvc wa-backup-snapshot-pvc
    oc delete volumesnapshot wa-backup-snapshot
    ```
    {: codeblock}
   
   
 

### Extracting {{site.data.keyword.postgresql}} backup by using a debug pod
{: #backup-extract-postgres}

To extract {{site.data.keyword.postgresql}} backup using a debug pod, complete the following steps:

1. Get the name of the store cronjob pod:
   ```bash 
   export STORE_CRONJOB_POD=`oc get pods -l component=store-cronjob --no-headers | awk 'NR==1{print $1}'`
   ```
   {: codeblock}

1. View the list of available store backups to identify the most recent backup:

   ```bash
   oc debug ${STORE_CRONJOB_POD}
   ls /store-backups/
   ```
   {: codeblock}

  In the list of store backups, you can find the latest backup with the help of the timestamps.{: tip}

1. While the debug pod listed in Step 2 remains active, in a separate terminal session, set the `STORE_CRONJOB_POD` variable to match the name of the store cronjob pod returned in Step 1:

   ```bash 
   export STORE_CRONJOB_POD=`oc get pods -l component=store-cronjob --no-headers | awk 'NR==1{print $1}'`
   ```
   {: codeblock}

1. Export and save the `STORE_DUMP_FILE` variable to the name of the most recent `store.dump_YYYYMMDD-TIME` file from `Step 2`:

   ```bash 
   export STORE_DUMP_FILE=store.dump_YYYYMMDD-TIME
   ```
   {: codeblock}

1. Copy the `store.dump_YYYYMMDD-TIME` file to a directory in a secure location on your system:

   ```bash
   `oc cp ${STORE_CRONJOB_POD}-debug:/store-backups/${STORE_DUMP_FILE} ${STORE_DUMP_FILE}`
   ```
   {: codeblock}

   You must verify that you copied the `store.dump_YYYYMMDD-TIME` file to the right directory by running the `ls` command.{: important}


## Backing up data by using the script
{: #backup-os}

You cannot backup data by using script in {{site.data.keyword.conversationshort}} for {{site.data.keyword.icp4dfull}} 4.6.3 or later.{ .note}

The `backupPG.sh` script gathers the pod name and credentials for one of your {{site.data.keyword.postgresql}} pods. Then, the `backupPG.sh` script uses the {{site.data.keyword.postgresql}} pod to run the `pg_dump` command.

To back up data by using the provided script, complete the following steps:

1.  Download the `backupPG.sh` script.

    Go to [GitHub](https://github.com/watson-developer-cloud/community/tree/master/watson-assistant/data){: external}, and find the directory for your version to find the file.

    If the `backupPG.sh` script doesn't exist in the directory of your version, backup your data by using [KubernetesCronJob](#backup-cronjob) or [pg_dump tool](#backup-cp4d).
    {: note}

1.  Log in to the Red Hat OpenShift project namespace where you installed the product.

1.  Run the script:

    ```bash
    ./backupPG.sh --instance ${INSTANCE} > ${BACKUP_DIR}
    ```
    {: codeblock}

    Replace the following values in the command:

    - `${BACKUP_DIR}`: Specify a file where you want to write the downloaded data. Be sure to specify a backup directory in which to store the file. For example, `/bu/backup-file-name.dump` creates a backup directory named `bu`.
    - `--instance ${INSTANCE}`: Select the specific instance to be backed up.


If you prefer to back up data by using the {{site.data.keyword.postgresql}} tool directly, you can complete the procedure to back up data manually.


## Backing up data manually
{: #backup-cp4d}

Complete the steps in this procedure to back up your data by using the {{site.data.keyword.postgresql}} tool directly.

To back up your data, complete these steps:

1.  Fetch a running {{site.data.keyword.postgresql}} pod:

    **Only for version 4.8.8, 5.1.0, and all future versions:**

    ```bash
       oc get pods -l app=${INSTANCE}-postgres-16 -o jsonpath="{.items[0].metadata.name}"
    ```
    {: codeblock}

    **For other versions, use:**

    ```bash
     oc get pods -l app=${INSTANCE}-postgres -o jsonpath="{.items[0].metadata.name}"
    ```
    {: codeblock}

    Replace ${INSTANCE} with the instance of the deployment that you want to back up.

2. Perform the following two steps only if you have **version 5.0.0 or 4.8.5 and before**:

   a. Fetch the store VCAP secret name:

    ```bash
     oc get secrets -l component=store,app.kubernetes.io/instance=${INSTANCE} -o=custom-columns=NAME:.metadata.name | grep store-vcap
    ```
    {: codeblock} 
    
   b. Fetch the {{site.data.keyword.postgresql}} connection values. You will pass these values to the command that you run in the next step. You must have `jq` installed.

    - To get the database:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.database'
      ```
      {: codeblock}

    - To get the hostname:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.host'
      ```
      {: codeblock}

    - To get the username:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.username'
      ```
      {: codeblock}

    - To get the password:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.password'
      ```
      {: codeblock}

1. Perform the following two steps only if you have **version 4.8.6 or 5.0.1 and later**:

   a. Fetch the store connection secret name:

    ```bash
    oc get secrets -l component=store-subsystem,app.kubernetes.io/instance=${INSTANCE} -o=custom-columns=NAME:.metadata.name | grep store-datastore-connection
    ```
    {: codeblock}   

   b. Fetch the {{site.data.keyword.postgresql}} connection values. You will pass these values to the command that you run in the next step. You must have `jq` installed.

    - To get the database:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.store_vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.database'
      ```
      {: codeblock}

    - To get the hostname:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.store_vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.host'
      ```
      {: codeblock}

    - To get the username:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.store_vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.username'
      ```
      {: codeblock}

    - To get the password:

      ```bash
      oc get secret $VCAP_SECRET_NAME -o jsonpath="{.data.store_vcap_services}" | base64 --decode | jq --raw-output '.["user-provided"][]|.credentials|.password'
      ```
      {: codeblock}

1.  Run the following command:

    ```bash
    oc exec $KEEPER_POD -- bash -c "export PGPASSWORD='$PASSWORD' && pg_dump -Fc -h $HOSTNAME -d $DATABASE -U $USERNAME" > ${BACKUP_DIR}
    ```
    {: codeblock}

    The following lists describe the arguments. You retrieved the values for some of these parameters in the previous step:

    **Only for version 4.8.8, 5.1.0, and all future versions:**  
  
    Use  `$KEEPER_POD`: Any {{site.data.keyword.postgresql}} 16 pod in your instance. 

    **For other versions:**

    Use `$KEEPER_POD`: Any {{site.data.keyword.postgresql}} pod in your instance.

    For all versions:

    - `${BACKUP_DIR}`: Specify a file where you want to write the downloaded data. Be sure to specify a backup directory in which to store the file. For example, `/bu/backup-file-name.dump` creates a backup directory named `bu`.
    - `$DATABASE`: The store database name that was retrieved from the Store VCAP secret in step 3.
    - `$HOSTNAME`: The hostname that was retrieved from the Store VCAP secret in step 3.
    - `$USERNAME`: The username that was retrieved from the Store VCAP secret in step 3.
    - `$PASSWORD`: The password that was retrieved from the Store VCAP secret in step 3.

    To see more information about the `pg_dump` command, you can run this command:

    ```bash
    oc exec -it ${KEEPER_POD} -- pg_dump --help
    ```
    {: codeblock}

1.  Take a backup of the secret that contains the encryption key. Ignore this step if the below 
    mentioned secret is not available in that release.      

    ```bash
    oc get secret -l service=conversation,app=$INSTANCE-auth-encryption
    oc get secret $INSTANCE-auth-encryption -o yaml > auth-encryption-secret.yaml
    ```
    {: codeblock}

## Restoring data
{: #backup-restore}

IBM created a restore tool called `pgmig`. The tool restores your database backup by adding it to a database that you choose. It also upgrades the schema to the one that is associated with the version of the product where you restore the data. Before the tool adds the backed-up data, it removes the data for all instances in the current service deployment, so any spares are also removed.

Prerequisite:

Setup `auth-encryption-secret` that you backed up earlier.

```bash
oc apply -f auth-encryption-secret.yaml 
oc get secret -l service=conversation,app=$INSTANCE-auth-encryption
```
{: codeblock}

1.  Install the target {{site.data.keyword.icp4dfull_notm}} cluster to which you want to restore the data.

    From the web client for the target cluster, create one service instance of for each service instance that was backed up on the old cluster. The target {{site.data.keyword.icp4dfull_notm}} cluster must have the same number of instances as there were in the environment where you backed up the database.

1.  Back up the current database before you replace it with the backed-up database.

    The tool clears the current database before it restores the backup. So, if you might need to revert to the current database, be sure to create a backup of it first.

1.  Go to the backup directory that you specified in the `${BACKUP_DIR}` parameter in the previous procedure.

1.  Run the following command to download the `pgmig` tool from the [GitHub Watson Developer Cloud Community](https://github.com/watson-developer-cloud/community/tree/master/watson-assistant/data){: external} repository.

    In the first command, update `<WA_VERSION>` to the version that you want to restore. For example, update `<WA_VERSION>` to `4.6.0` if you want to restore 4.6.0.
    {: important}

    ```bash
    wget https://github.com/watson-developer-cloud/community/raw/master/watson-assistant/data/<WA_VERSION>/pgmig
    chmod 755 pgmig
    ```
    {: codeblock}

1.  Create the following configuration files and store them in the same backup directory:

    - `resourceController.yaml` (prior to Version 5.2.1): The Resource Controller file keeps a list of all provisioned instances. See [Creating the resourceController.yaml file (prior to Version 5.2.1)](#creating-the-resourcecontrolleryaml-file-prior-to-version-521).

    - `resourceController.yaml` (For Version 5.2.1 and later): The Resource Controller file keeps a list of all provisioned instances. See [Creating the resourceController.yaml file (Version 5.2.1 and later)](#creating-the-resourcecontrolleryaml-file-version-521-and-later)

    - `postgres.yaml`: The {{site.data.keyword.postgresql}} file lists details for the target {{site.data.keyword.postgresql}} pods. See [Creating the postgres.yaml file](#creating-the-postgresyaml-file).   

1.  Get the secret:

    **Only for version 4.8.8, 5.1.0, and all future versions:**

    ```bash
    oc get secret ${INSTANCE}-postgres-16-ca -o jsonpath='{.data.ca\.crt}' | base64 -d | tee ${BACKUP_DIR}/ca.crt | openssl x509 -noout -text
    ```
    {: codeblock}

    **For other versions:**

    ```bash
    oc get secret ${INSTANCE}-postgres-ca -o jsonpath='{.data.ca\.crt}' | base64 -d | tee ${BACKUP_DIR}/ca.crt | openssl x509 -noout -text
    ```
    {: codeblock}

    - Replace `${INSTANCE}` with the name of the instance that you want to back up.
    - Replace `${BACKUP_DIR}` with the directory where the `postgres.yaml` and `resourceController.yaml` files are located.

1.  Copy the files that you downloaded and created in the previous steps to any existing directory on a {{site.data.keyword.postgresql}} pod.

    a. **Only for version 4.8.8, 5.1.0, and all future versions:**
 
    Run the following command to find {{site.data.keyword.postgresql}} pods:

    ```bash
    oc get pods | grep ${INSTANCE}-postgres-16
    ```
    {: codeblock}

    b. **For other versions:**
    
    Run the following command to find {{site.data.keyword.postgresql}} pods:

    ```bash
    oc get pods | grep ${INSTANCE}-postgres
    ```
    {: codeblock}
    
    c. The files that you must copy are `pgmig`, `postgres.yaml`, `resourceController.yaml`, `ca.crt` (the secret file that is generated in step 6), and the file that you created for your downloaded data. Run the following commands to copy the files.

     If you are restoring data to a stand-alone {{site.data.keyword.icp4dfull_notm}} cluster, then replace all references to `oc` with `kubectl` in these sample commands.
    {: note}

    ```bash
     oc exec -it ${POSTGRES_POD} -- mkdir /controller/tmp
     oc exec -it ${POSTGRES_POD} -- mkdir /controller/tmp/bu
     oc rsync ${BACKUP_DIR}/ ${POSTGRES_POD}:/controller/tmp/bu/
    ```
    {: codeblock}

    - Replace `${POSTGRES_POD}` with the name of one of the {{site.data.keyword.postgresql}} pods from the previous step.
 

1.  Stop the store deployment by scaling the store deployment down to 0 replicas:

     ```bash
     oc scale deploy ibm-watson-assistant-operator -n ${OPERATOR_NS} --replicas=0
     oc get deployments -l component=store
     ```
     {: codeblock}

    Make a note of how many replicas there are in the store deployment:
 
    ```bash
     oc scale deployment ${STORE_DEPLOYMENT} --replicas=0
    ```
    {: codeblock}


1.  Initiate the execution of a remote command in the {{site.data.keyword.postgresql}} pod:


    ```bash
    oc exec -it ${POSTGRES_POD} /bin/bash
    ```
    {: codeblock}

1.  Run the `pgmig` tool:

    **Only for version 4.8.8, 5.1.0, and all future versions:**
    
    ```bash
    cd /controller/tmp/bu
    export PG_CA_FILE=/controller/tmp/bu/ca.crt
    ./pgmig --resourceController resourceController.yaml --target postgres.yaml --source <backup-file-name.dump>
    export ENABLE_ICP=true
    ```
    {: codeblock}

    **For other versions:**

    ```bash
    cd /controller/tmp/bu
    export PG_CA_FILE=/controller/tmp/bu/ca.crt
    ./pgmig --resourceController resourceController.yaml --target postgres.yaml --source <backup-file-name.dump>
    ```
    {: codeblock}

    - Replace `<backup-file-name.dump>` with the name of the file that you created for your downloaded data.

    For more command options, see [{{site.data.keyword.postgresql}} migration tool details](#backup-pgmig-details).

    As the script runs, you are prompted for information that includes the instance on the target cluster to which to add the backed-up data. The data on the instance you specify is removed and replaced. If there are multiple instances in the backup, you are prompted multiple times to specify the target instance information.

1.  Scale the store deployment back up:

    ```bash
    oc scale deployment ${STORE_DEPLOYMENT} --replicas=${ORIGINAL_NUMBER_OF_REPLICAS}
    oc scale deploy ibm-watson-assistant-operator -n ${OPERATOR_NS} --replicas=1
    ```
    {: codeblock}

    You might need to wait a few minutes before the data your restored is visible from the web interface.

1.  After you restore the data, you must train the backend model. For more information about retraining your backend model, see [Retraining your backend model](#set-up-retrain-model).



### Creating the resourceController.yaml file 
{: #backup-resource-controller-yaml}





The **resourceController.yaml** file contains details about the new environment where you are adding the backed-up data. Add the following information to the file:

```yaml
accessTokens: 
  - value
  - value2
host: localhost
port: 5000
```
{: codeblock}

To add the values that are required but currently missing from the file, complete the following steps:

1.  To get the accessTokens values list, you need to get a list of bearer tokens for the service instances.

    - Log in to the {{site.data.keyword.icp4dfull_notm}} web client.
    - From the main {{site.data.keyword.icp4dfull_notm}} web client navigation menu, select **My instances**.
    - On the **Provisioned instances** tab, click your instance.
    - In the Access information of the instance, find the **Bearer token**. Copy the token and paste it into the accessTokens list.

    A bearer token for an instance can access all instances that are owned by the user. Therefore, if a single user owns all of the instances, then only one bearer token is required.

    If the service has multiple instances, each owned by a different user, then you must gather bearer tokens for each user who owns an instance. You can list multiple bearer token values in the `accessTokens` section.

1.  To get the host information, you need details for the pod that hosts the UI component: 

    ```bash
    oc describe pod -l component=ui
    ```
    {: codeblock}

    Look for the section that says `RESOURCE_CONTROLLER_URL: https://${release-name}-addon-assistant-gateway-svc.zen:5000/api/ibmcloud/resource-controller`.

    For example, you can use a command like this to find it:

    ```bash
    oc describe pod -l component=ui | grep RESOURCE_CONTROLLER_URL
    ```
    {: codeblock}

    Copy the host that is specified in the `RESOURCE_CONTROLLER_URL`. The host value is the `RESOURCE_CONTROLLER_URL` value, excluding the protocol at the beginning and everything from the port to the end of the value. For example, for the previous example, the host is `${release-name}-addon-assistant-gateway-svc.zen`.

1.  To get the port information, again check the RESOURCE_CONTROLLER_URL entry. The port is specified after `<host>:` in the URL. In this sample URL, the port is `5000`.

1.  Paste the values that you discovered into the YAML file and save it.



### Creating the postgres.yaml file
{: #backup-postgres-yaml}


The **postgres.yaml** file contains details about the {{site.data.keyword.postgresql}} pods in your target environment (the environment where you restore the data). Add the following information to the file:


```yaml
host: localhost
port: 5432
database: store
username: user
su_username: admin
su_password: password
```
{: codeblock}

To add the values that are required but currently missing from the file, complete the following steps:

1. **For version 4.8.6 or 5.0.1 and later**:

   To get information about the `host`, you must get the Store datastore connection strings secret.
    
     ```bash
    oc get secret ${INSTANCE}-store-datastore-connection-strings -o jsonpath='{.data.store_vcap_services}' | base64 -d

    ```
    {: codeblock}

   **For version 5.0.0 or 4.8.5 and before**:
   
   To get information about the `host`, you must get the Store VCAP secret.

    ```bash
    oc get secret ${INSTANCE}-store-vcap -o jsonpath='{.data.vcap_services}' | base64 -d
    ```
    {: codeblock}

    The `get` command returns information about the Redis and {{site.data.keyword.postgresql}} databases. Look for the segment of JSON code for the {{site.data.keyword.postgresql}} database, named `pgservice`. It looks like this:

      ```json
      {
        "user-provided":[
          {
            "name": "pgservice",
            "label": "user-provided",
            "credentials":
            {
              "host": "${INSTANCE}-rw",
              "port": 5432,
              "database": "conversation_pprd_${INSTANCE}",
              "username": "${dbadmin}",
              "password": "${password}"
            }
          }
        ],
      }
      ```
      {: codeblock}

1.  Copy the values for user-provided credentials (`host`, `port`, `database`, `username`, and `password`).

    You can specify the same values that were returned for `username` and `password` as the `su_username` and `su_password` values.

    The updated file looks something like this:
   
     **Only for version 4.8.8, 5.1.0, and all future versions:**

     ```yaml
     host: wa_inst-postgres-16-rw
     port: 5432
     database: conversation_pprd_wa_inst
     username: dbadmin
     su_username: dbadmin
     su_password: mypassword
     ```
     {: codeblock}

     **For other versions:**

     ```yaml
     host: wa_inst-postgres-rw
     port: 5432
     database: conversation_pprd_wa_inst
     username: dbadmin
     su_username: dbadmin
     su_password: mypassword
     ```
     {: codeblock}

1.  Save the `postgres.yaml` file.


### {{site.data.keyword.postgresql}} migration tool details


{: #backup-pgmig-details}

The following table lists the arguments that are supported by the `pgmig` tool:

| Argument | Description |
|---------|-------------|
| -h, --help | Command usage |                    
| -f, --force | Erase data if present in the target Store |
| -s, --source string | Backup file name |   
| -r, --resourceController string | Resource Controller configuration file name |
| -t, --target string | Target {{site.data.keyword.postgresql}} server configuration file name |
| -m, --mapping string | Service instance-mapping configuration file name (optional) |
| --testRCConnection | Test the connection for Resource Controller, then exit |
| --testPGConnection | Test the connection for {{site.data.keyword.postgresql}} server, then exit |
| -v, --version | Get Build version |
{: caption="pgmig tool arguments" caption-side="top"}

### The mapping configuration file
{: #backup-mapping-file}

After you run the script and specify the mappings when prompted, the tool generates a file that is named `enteredMapping.yaml` in the current directory. This file reflects the mapping of the old cluster details to the new cluster based on the interactive inputs that were provided while the script was running.

For example, the YAML file contains values like this:

```yaml
instance-mappings:
  00000000-0000-0000-0000-001570184978: 00000000-0000-0000-0000-001570194490
```
{: codeblock}

Where the first value (`00000000-0000-0000-0000-001570184978`) is the instance ID in the database backup and the second value (`00000000-0000-0000-0000-001570194490`) is the ID of a provisioned instance in the service on the system.

You can pass this file to the script for subsequent runs of the script in the same environment. Or you can edit it for use in other back up and restore operations. The mapping file is optional. If it is not provided, the tool prompts you for the mapping details based on information you provide in the YAML files.

## Retraining your backend model
{: #set-up-retrain-model}

Per the number of models in your assistant, you can use one of the following options to retrain your backend model:

- [Retrain your backend model manually](#set-up-retrain-model-manual)
- [Auto-retrain your backend model](#set-up-retrain-model-auto)

### Retrain your backend model manually
{: #set-up-retrain-model-manual}

When you open a dialog skill after a change in the training data, training is initiated automatically. Give the skill time to retrain on the restored data. It usually takes less than 10 minutes to get trained. The process of training a machine learning model requires at least one node to have 4 CPUs that can be dedicated to training. Therefore, open restored assistants and skills during low traffic periods and open them one at a time. If the assistant or dialog skill does not respond, then modify the workspace (for example, add an intent and then remove it). Check and confirm.

### Auto-retrain your backend model
{: #set-up-retrain-model-auto}

When you have a large number of models to retrain, you can use the auto-retrain-all job to train the backend model. To learn more about the auto-retrain-all job and its implementation, refer to the following topics:

- [Before you begin](#set-up-auto-retrain-prereq)
- [Planning](#set-up-auto-retrain-plan)
- [Procedure](#set-up-auto-retrain-procedure)
- [Speeding up the retrain process](#set-up-auto-retrain-speed-up)

#### Before you begin
{: #set-up-auto-retrain-prereq}

Before you begin the auto-retrain-all job, you must ensure that the {{site.data.keyword.postgresql}} database and Cloud Object Storage (Cloud Object Storage), which stores your action and dialog skills along with their snapshots, are active and not corrupted. In addition, you must ensure that your assistants do not receive or send any data during the auto-retrain-all job. 

#### Planning
{: #set-up-auto-retrain-plan}

To get a good estimation of the duration that is required to complete the auto-retrain-all job, you can use the `calculate_autoretrain_all_job_duration.sh` script: 

 **Only for version 5.1.0, 5.0.3, 4.8.8, and all future versions:**

 Specify the namespace where assistant is installed in the `PROJECT_CPD_INST_OPERANDS` key in the script below.
 
 ```bash
#!/bin/bash

calculate_duration() {
  local input_variable="$1"
  DURATION=$(("$NUM_OF_WORKSPACES_TO_TRAIN"*60 / (input_variable * 2) + "$NUM_OF_WORKSPACES_TO_TRAIN" * 2))
}

export PROJECT_CPD_INST_OPERANDS=<namespace where Assistant is installed>

ETCD_ENDPOINTS=$(oc get secret wa-cluruntime-datastore-connection-strings -n ${PROJECT_CPD_INST_OPERANDS} -o jsonpath="{.data.etcd}" | base64 --decode | jq -r '.endpoints')

NUM_OF_WORKSPACES_TO_TRAIN=$(oc exec wa-etcd-0 -n ${PROJECT_CPD_INST_OPERANDS} -- bash -c "
  password=\"\$( cat /var/run/credentials/pass.key)\"
  etcdctl_user=\"root:\$password\"
  export ETCDCTL_USER=\"\$etcdctl_user\"

  ETCDCTL_API=3 etcdctl --cert=/etc/etcdtls/operator/etcd-tls/etcd-client.crt --key=/etc/etcdtls/operator/etcd-tls/etcd-client.key --cacert=/etc/etcdtls/operator/etcd-tls/etcd-client-ca.crt --endpoints=${ETCD_ENDPOINTS} get  --prefix  /bluegoat/voyager-nlu/voyager-nlu-slot-wa/workspaces/ --keys-only | sed '/^$/d' | wc -l")

echo "Number of workspaces to train $NUM_OF_WORKSPACES_TO_TRAIN"

calculate_duration 5
DURATION_5=$DURATION

calculate_duration 10
DURATION_10=$DURATION

calculate_duration 15
DURATION_15=$DURATION

echo "Approximate duration of the auto retrain all job if you have 5 Training pods: $DURATION_5 seconds"
echo "Approximate duration of the auto retrain all job if you have 10 Training pods: $DURATION_10 seconds"
echo "Approximate duration of the auto retrain all job if you have 15 Training pods: $DURATION_15 seconds"
   
 ```
 {: codeblock} 
 
**For other versions:**

```bash
#!/bin/bash
calculate_duration() {
    local input_variable="$1"
    DURATION=$(("$NUM_OF_WORKSPACES_TO_TRAIN"*60 / (input_variable * 2) + "$NUM_OF_WORKSPACES_TO_TRAIN" * 2))
  }

export PROJECT_CPD_INST_OPERANDS=<namespace where Assistant is installed>

NUM_OF_WORKSPACES_TO_TRAIN=$(oc exec wa-etcd-0 -n ${PROJECT_CPD_INST_OPERANDS} -- bash -c '
  password="$( cat /var/run/credentials/pass.key )"
  etcdctl_user="root:$password"
  export ETCDCTL_USER="$etcdctl_user"

  ETCDCTL_API=3 etcdctl --cert=/etc/etcdtls/operator/etcd-tls/etcd-client.crt --key=/etc/etcdtls/operator/etcd-tls/etcd-client.key --cacert=/etc/etcdtls/operator/etcd-tls/etcd-client-ca.crt --endpoints=https://$(hostname).${CLUSTER_NAME}.cpd.svc.cluster.local:2379 get  --prefix  /bluegoat/voyager-nlu/voyager-nlu-slot-wa/workspaces/ --keys-only | sed '/^$/d' | wc -l')

echo "Number of workspaces to train $NUM_OF_WORKSPACES_TO_TRAIN"

calculate_duration 5
DURATION_5=$DURATION

calculate_duration 10
DURATION_10=$DURATION

calculate_duration 15
DURATION_15=$DURATION
echo "Approximate duration of the auto retrain all job if you have 5 Training pods: $DURATION_5 seconds"
echo "Approximate duration of the auto retrain all job if you have 10 Training pods: $DURATION_10 seconds"
echo "Approximate duration of the auto retrain all job if you have 15 Training pods: $DURATION_15 seconds"
```
{: codeblock}

In addition, you can plan to speed up the auto-retrain-all job after you get the estimation of duration. For more information about speeding up the auto-retrain-all job, see the [Speeding up the auto-retrain-all job](#set-up-auto-retrain-speed-up) topic.

#### Procedure
{: #set-up-auto-retrain-procedure}

To retrain your backend model by using the auto-retrain-all job, you do the following steps:

- [Set up the environment variables for the auto-retrain-all job](#set-up-auto-retrain-env-variables)
- [Run the auto-retrain-all job](#set-up-auto-retrain-run)
- [Validate the auto-retrain-all job](#set-up-auto-retrain-validate)

##### Set up the environment variables for the auto-retrain-all job
{: #set-up-auto-retrain-env-variables}

Set up the following environment variable before you run the auto-retrain-all job:

1. Set the `AUTO_RETRAIN` environment variable to `false` to disable any existing auto-retrain job:

    ```bash  
      export AUTO_RETRAIN="false"
    ```
    {: codeblock}

1. To set up the `BATCH_RETRAIN_ALL_SIZE` environment variable, you multiply the number of available training replicas, `CLU_TRAINING_REPLICAS`, with `2` based on the assumption that each model takes approximately `~30 seconds` to train a model. Use the following command to set up `BATCH_RETRAIN_ALL_SIZE`:

    ```bash
      export BATCH_RETRAIN_ALL_SIZE=$(($(oc get deploy ${INSTANCE}-clu-training --template='{{index .spec.replicas}}') * 2))
    ```
    {: codeblock}

1. Set `WAIT_TIME_BETWEEN_BATCH_RETRAIN_IN_SECONDS_FOR_RETRAIN_ALL` to `(60-${BATCH_RETRAIN_ALL_SIZE})`:

    ```bash
      export WAIT_TIME_BETWEEN_BATCH_RETRAIN_IN_SECONDS_FOR_RETRAIN_ALL=$((60-${BATCH_RETRAIN_ALL_SIZE}))
    ```
    {: codeblock}

1. Set `WAIT_TIME_BETWEEN_TRAININGS_FOR_RETRAIN_ALL` to 1:

    ```bash
      export WAIT_TIME_BETWEEN_TRAININGS_FOR_RETRAIN_ALL=1
    ```
    {: codeblock}

1. Set `AUTO_RETRAIN_ALL_CRON_SCHEDULE` to the time that you want to run the auto-retrain-all job:

    ```bash
      export AUTO_RETRAIN_ALL_CRON_SCHEDULE=<value of cron schedule>
    ```
    {: codeblock}

    For example, you can give a value such as `"0 40 19 11 3 ? 2024"`, which is in the following format: 
    
    `(Seconds) (Minutes) (Hours) (Day of Month) (Month) (Day of Week) (Year)`

    You must set the time in UTC time zone.
    {: important}

1. Set `AUTO_RETRAIN_ALL_ENABLED` to true:

    ```bash
      export AUTO_RETRAIN_ALL_ENABLED="true"
    ```
    {: codeblock}

##### Run the auto-retrain-all job
{: #set-up-auto-retrain-run}

1. To run the auto-retrain-all job, use the following command:

    ```bash
        export PROJECT_CPD_INST_OPERANDS=<namespace where Assistant is installed>
        export INSTANCE=`oc get wa -n ${PROJECT_CPD_INST_OPERANDS} |grep -v NAME| awk '{print $1}'`

        cat <<EOF | oc apply -f -
        apiVersion: assistant.watson.ibm.com/v1
        kind: TemporaryPatch
        metadata:
          name: ${INSTANCE}-store-admin-env-vars
          namespace: ${PROJECT_CPD_INST_OPERANDS}
        spec:
          apiVersion: assistant.watson.ibm.com/v1
          kind: WatsonAssistantStore
          name: ${INSTANCE}
          patchType: patchStrategicMerge
          patch:
            store-admin:
              deployment:
                spec:
                  template:
                    spec:
                      containers:
                      - name: store-admin
                        env:
                        - name: AUTO_RETRAIN
                          value: "${AUTO_RETRAIN}"
                        - name: AUTO_RETRAIN_ALL_CRON_SCHEDULE
                          value: "${AUTO_RETRAIN_ALL_CRON_SCHEDULE}"
                        - name: AUTO_RETRAIN_ALL_ENABLED
                          value: "${AUTO_RETRAIN_ALL_ENABLED}"
                        - name: BATCH_RETRAIN_ALL_SIZE
                          value: "${BATCH_RETRAIN_ALL_SIZE}"
                        - name: WAIT_TIME_BETWEEN_BATCH_RETRAIN_IN_SECONDS_FOR_RETRAIN_ALL
                          value: "${WAIT_TIME_BETWEEN_BATCH_RETRAIN_IN_SECONDS_FOR_RETRAIN_ALL}"
                        - name: WAIT_TIME_BETWEEN_TRAININGS_FOR_RETRAIN_ALL
                          value: "${WAIT_TIME_BETWEEN_TRAININGS_FOR_RETRAIN_ALL}"
        EOF
    ```
  {: codeblock} 

   **Only for version 5.1.0, 5.0.3, 4.8.8, and all future versions:**
 
1. Get the etcd endpoint by running the following:

   ```bash
   oc get secret wa-cluruntime-datastore-connection-strings -o jsonpath="{.data.etcd}" | base64 --decode | jq -r '.endpoints
   ```
   {: codeblock}

1. After you complete the auto-retrain-all job, you must disable the auto-retrain-all flag and enable auto-retrain flag by using the following commands:

   ```bash
      oc patch temporarypatch ${INSTANCE}-store-admin-env-vars -p '{"metadata":{"finalizers":[]}}' --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc delete temporarypatch ${INSTANCE}-store-admin-env-vars -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch watsonassistantstore/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oppy.ibm.com/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
   ```
   {: codeblock}

##### Validate the auto-retrain-all job
{: #set-up-auto-retrain-validate}

You can validate the successful completion of the auto-retrain-all job by comparing the number of `Affected workspaces found` with the `Retrained Total` count in the store-admin service log. To get the number of `Affected workspaces found` and the `Retrained Total`, run the following command:

 ```bash
 oc logs $(oc get pod -l component=store-admin --no-headers -n ${PROJECT_CPD_INST_OPERANDS}  |awk '{print $1}') | grep "\[RETRAIN-ALL-SUMMARY\] Affected workspaces found"
 ```
 {: codeblock}

If the auto-retrain-all job is successful, the `Retrained Total` count equals the number of `Affected workspaces found`. In addition, if the difference between the counts of the `Retrained Total` and `Affected workspaces found` is small, the auto-retrain-all job completes successfully by training the remaining models in the background. However, if there is a big difference between `Retrained Total` and `Affected workspaces found`, you must look at the store-admin logs to analyze the issue and consider [speeding up the auto-retrain-all job](#set-up-auto-retrain-speed-up). 

#### Speeding up the auto-retrain-all job
{: #set-up-auto-retrain-speed-up}

The duration to complete the auto-retrain-all job depends on the number of models to train. Therefore, to speed up the training process, you must `scale` the number of `CLU_TRAINING_REPLICAS` and its dependencies. For example, if you `scale` the number of `CLU_TRAINING_REPLICAS` to `x`, you must `scale` the number of dependent replicas per the following calculation:

- `TFMM_REPLICAS` to 0.5x
- `DRAGONFLY_CLU_MM_REPLICAS` to 0.3x 
- `CLU_EMBEDDING_REPLICAS` to 0.2x
- `CLU_TRITON_SERVING_REPLICAS` to 0.2x. 

If your calculation result for the number of models is a decimal number, then you must round-up the result to the next greater whole number. For example, if the number of `TFMM_REPLICAS` is 2.4, then round-up the value to 3. {: tip}

Use the following steps to `scale` the number of models: 

1. Register the values of the number of replicas per your calculation:

    ```bash
      export CLU_TRAINING_REPLICAS=<value from calculation>
      export TFMM_REPLICAS=<value from calculation>
      export DRAGONFLY_CLU_MM_REPLICAS=<value from calculation>
      export CLU_EMBEDDING_REPLICAS=<value from calculation>
      export CLU_TRITON_SERVING_REPLICAS=<value from calculation>
    ```
    {: codeblock}

1. Increase the number of `REPLICAS` by using the following command:

    ```bash
      export PROJECT_CPD_INST_OPERANDS=<namespace where Assistant is installed>
      export INSTANCE=`oc get wa -n ${PROJECT_CPD_INST_OPERANDS} |grep -v NAME| awk '{print $1}'`

      cat <<EOF | oc apply -f -
      apiVersion: assistant.watson.ibm.com/v1
      kind: TemporaryPatch
      metadata:
        name: ${INSTANCE}-clu-training-replicas
        namespace: ${PROJECT_CPD_INST_OPERANDS}
      spec:
        apiVersion: assistant.watson.ibm.com/v1
        kind: WatsonAssistantCluTraining
        name: $INSTANCE
        patchType: patchStrategicMerge
        patch:
          clu-training:
            deployment:
              training:
                spec:
                  replicas: ${CLU_TRAINING_REPLICAS}
      EOF

      cat <<EOF | oc apply -f -
      apiVersion: assistant.watson.ibm.com/v1
      kind: TemporaryPatch
      metadata:
        name: ${INSTANCE}-clu-runtime-replicas
        namespace: ${PROJECT_CPD_INST_OPERANDS}
      spec:
        apiVersion: assistant.watson.ibm.com/v1
        kind: WatsonAssistantCluRuntime
        name: ${INSTANCE}
        patchType: patchStrategicMerge
        patch:
          tfmm:
            deployment:
              spec:
                replicas: ${TFMM_REPLICAS}
          dragonfly-clu-mm:
            deployment:
              spec:
                replicas: ${DRAGONFLY_CLU_MM_REPLICAS}
      EOF

      cat <<EOF | oc apply -f -
      apiVersion: assistant.watson.ibm.com/v1
      kind: TemporaryPatch
      metadata:
        name: ${INSTANCE}-clu-replicas
        namespace: ${PROJECT_CPD_INST_OPERANDS}
      spec:
        apiVersion: assistant.watson.ibm.com/v1
        kind: WatsonAssistantClu
        name: ${INSTANCE}
        patchType: patchStrategicMerge
        patch:
          clu-embedding:
            deployment:
              spec:
                replicas: ${CLU_EMBEDDING_REPLICAS}
          clu-triton-serving:
            deployment:
              spec:
                replicas: ${CLU_TRITON_SERVING_REPLICAS}
      EOF
    ```
    {: codeblock}

1. After you complete the auto-retrain-all job, you must revert the number of `REPLICAS` to the original numbers:

     ```bash
      oc patch temporarypatch ${INSTANCE}-clu-training-replicas -p '{"metadata":{"finalizers":[]}}' --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch temporarypatch ${INSTANCE}-clu-runtime-replicas -p '{"metadata":{"finalizers":[]}}' --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch temporarypatch ${INSTANCE}-clu-replicas -p '{"metadata":{"finalizers":[]}}' --type=merge -n ${PROJECT_CPD_INST_OPERANDS}

      oc delete temporarypatch ${INSTANCE}-clu-training-replicas -n ${PROJECT_CPD_INST_OPERANDS}
      oc delete temporarypatch ${INSTANCE}-clu-runtime-replicas -n ${PROJECT_CPD_INST_OPERANDS}
      oc delete temporarypatch ${INSTANCE}-clu-replicas -n ${PROJECT_CPD_INST_OPERANDS}

      oc patch watsonassistantclutraining/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oppy.ibm.com/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch watsonassistantcluruntime/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oppy.ibm.com/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch watsonassistantclu/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oppy.ibm.com/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch watsonassistantclutraining/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oper8.org/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch watsonassistantcluruntime/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oper8.org/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      oc patch watsonassistantclu/${INSTANCE} -p "{\"metadata\":{\"annotations\":{\"oper8.org/temporary-patches\":null}}}" --type=merge -n ${PROJECT_CPD_INST_OPERANDS}
      ```
      {: codeblock}
