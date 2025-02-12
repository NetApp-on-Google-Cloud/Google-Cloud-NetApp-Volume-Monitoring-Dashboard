# Google Cloud Monitoring dashboard to monitor NetApp Volumes

## What is it?
NetApp Volumes is a native NFS/SMB file service on Google Cloud. Its volumes are filesystems which can be accessed by NFS/SMB clients over a network for file sharing purposes. For more details, see the [documentation](https://cloud.google.com/netapp/volumes/docs/discover/overview).

NetApp Volumes exports a [rich set of metrics](https://cloud.google.com/netapp/volumes/docs/monitor/cloud-monitoring-metrics) to Google [Cloud Monitoring](https://cloud.google.com/monitoring/docs/monitoring-overview). Administators can use these metrics to [create charts](https://cloud.google.com/monitoring/charts/metrics-explorer) to monitor resources. Multiple charts can be grouped into [dashboards](https://cloud.google.com/monitoring/dashboards).

## The NetApp Volumes dashboard

![Demo screenshot showing some charts of the dashboard](/dashboard-demo.png)

This repository offers a baseline dashboard with relevant charts. You can add/remove/change charts to customize it for your requirements.

Currently it offers the following charts:
* *Volume capacity usage*: This chart shows the percentage of used capacity in a volume versus its size. If a volume gets 100% full, writes to it will fail with an *Out of space* error message. Administrators want to avoid volumes which are 100% full.

* *Volume inode usage*: Every file or directory is an inode. Every volume can hold a [maximum number of inodes](https://cloud.google.com/netapp/volumes/docs/quotas#maxfiles_limit). If your volume reaches 100% inode usage, users/application will not be able to create new files or directories in the volume.

* *Volume throughput usage*: Percentage of current volume throughput vs the volumes capability. In NetApp Volumes, the maximum throughput of a volume depends on its service level and the volumes size (for Standard/Premium/Extreme) or the storage pool size (for Flex). This chart shows ther percentage of throughput consumed vs throughput available. Works well for Standard/Premium/Extreme. The results for Flex are misleading, since it shows volume throughput vs pool throughput, but all volumes in a pool share the pools throughput.

* *Volume throughput*: Shows the throughput (reads + writes + metadata combined) for every volume. Volumes have a throughput limit which depends on their size and service level (for service levels Standard, Premium and Extreme) or their storage pools size (for service level Flex).

* *Volume IOPS*: Shows the IO operations per second of a volume. NetApp Volumes exports data for three subtypes (Read, Write and Metadata) to Cloud Monitoring. This graph sums them up for per volume.

* *Volume latency*: Shows the average latency (over a 5 minute window) of read+write+metadata operations combined per volume.

* *Volume IO activity*: Table of latest top I/O activity volumes

## Installation

Follow Googles instructions on how to [install sample dashboads](https://cloud.google.com/monitoring/dashboards/dashboard-templates), but upload this [JSON file](/netapp-volumes-dashboard.json) from this repository.

## Upgrades
We plan to improve this dashboard over time by adding additonal useful charts.
You can utilize the [JSON Editor of Cloud Monitoring](https://cloud.google.com/monitoring/charts/manage-widgets#json) to replace the old dashboard definition with a new one from this repository. 

Please note that this will overwrite any changes you did to the dashboard. If you are familiar with JSON and it's structure, you can manually copy/paste the new parts you like to include into your existing JSON definition. Backup your existion JSON definition prior or import the update into a new dashboard to keeping your custom dashboard intact.

## Improvements
It is the intention to improve the dashboard by adding additonal useful charts and functionality. If you think you have a use case which is of benefit for other users of NetApp Volumes, please consider opening an issue for this repository and describe your ask and we will consider it.

We will not offer support on how to craft Cloud Monitoring queries. Please contact Google Cloud Support for Cloud Monitoring expertise.

