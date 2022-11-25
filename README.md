# oci-queue-fn-oke-demo

[![License: UPL](https://img.shields.io/badge/license-UPL-green)](https://img.shields.io/badge/license-UPL-green) [![Quality gate](https://sonarcloud.io/api/project_badges/quality_gate?project=oracle-devrel_oci-queue-fn-oke-demo)](https://sonarcloud.io/dashboard?id=oracle-devrel_oci-queue-fn-oke-demo)

## THIS IS A NEW, BLANK REPO THAT IS NOT READY FOR USE YET.  PLEASE CHECK BACK SOON!

## Introduction
MISSING

## Getting Started
MISSING

### Prerequisites

#### Create OCI Dynamic Group

To interact with OCI resources: queues & functions, the application will authenticate as instance principal.

**Create tag namespace**: authorization
**Create a tag key**: instance_principal

**Name**: queue_automation_dg
**match_rule**:
`All {instance.compartment.id='<kubernetes worker nodes compartment_ocid>',`
`tag.authorization.instance_principal.value='yes'}`

Add to Kubernetes worker nodes below the defined tag:
authorization.instance_principal = 'yes'

#### Create OCI policies

 **Name** : queue_automation_policies  

**Policies** : 

`allow dynamic-group queue_automation_dg to use queues in compartment <queue_parent_compartment><br/>allow dynamic-group queue_automation_dg to use fn-invocation in compartment <function_parent_compartment>` 

For explicit access is possible to target queue.id and function.id

**Policies** : 

`allow dynamic-group queue_automation_dg to use queues in compartment <queue_parent_compartment> where target.queue.id='<queue_OCID>'<br/>allow dynamic-group queue_automation_dg to use fn-invocation in compartment <function_parent_compartment> where target.function.id = '<function_OCID>'` 



#### Build docker image

`docker build -f Dockerfile -t <OCIR_container_image_url>` 

#### Push docker image to OCIR

https://docs.oracle.com/en-us/iaas/Content/Registry/Tasks/registrypushingimagesusingthedockercli.htm

docker push <OCIR_container_image_url>

#### OCIR Docker Secret

Create a docker secret for OCIR and update secret name in queue-automation.yaml file.

https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengpullingimagesfromocir.htm

#### Replace secret name and container image URL in queue-automation.yaml

Create deployment
`kubectl apply -f queue-automation.yaml`

## Notes/Issues
MISSING

## URLs
* Nothing at this time

## Contributing
This project is open source.  Please submit your contributions by forking this repository and submitting a pull request!  Oracle appreciates any contributions that are made by the open source community.

## License
Copyright (c) 2022 Oracle and/or its affiliates.

Licensed under the Universal Permissive License (UPL), Version 1.0.

See [LICENSE](LICENSE) for more details.

ORACLE AND ITS AFFILIATES DO NOT PROVIDE ANY WARRANTY WHATSOEVER, EXPRESS OR IMPLIED, FOR ANY SOFTWARE, MATERIAL OR CONTENT OF ANY KIND CONTAINED OR PRODUCED WITHIN THIS REPOSITORY, AND IN PARTICULAR SPECIFICALLY DISCLAIM ANY AND ALL IMPLIED WARRANTIES OF TITLE, NON-INFRINGEMENT, MERCHANTABILITY, AND FITNESS FOR A PARTICULAR PURPOSE.  FURTHERMORE, ORACLE AND ITS AFFILIATES DO NOT REPRESENT THAT ANY CUSTOMARY SECURITY REVIEW HAS BEEN PERFORMED WITH RESPECT TO ANY SOFTWARE, MATERIAL OR CONTENT CONTAINED OR PRODUCED WITHIN THIS REPOSITORY. IN ADDITION, AND WITHOUT LIMITING THE FOREGOING, THIRD PARTIES MAY HAVE POSTED SOFTWARE, MATERIAL OR CONTENT TO THIS REPOSITORY WITHOUT ANY REVIEW. USE AT YOUR OWN RISK. 