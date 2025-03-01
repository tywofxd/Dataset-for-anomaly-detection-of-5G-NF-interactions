# Dataset-for-anomaly-detection-of-5G-NF-interactions

This is a dataset for testing anomaly detection algorithms on abnormal interactions between 5G NF invocations.

The directories and files contained therein are described as follows.

1. abnormal

   This directory contains three types of abnormal interaction samples for 5G core NFs: ue_info_get, evil_nf_delete, and nf_dos. For each type, we have recorded anomalous samples with different NFs acting as initiators. When a specific NF acts as the initiator of malicious calls, we have recorded a total of 100 anomalous samples. These 100 samples are all stored in a folder named as that particular NF. Each anomalous sample is recorded in the form of a JSON file. Each JSON file documents a process of 5G NF interactions that includes malicious calls.

   Introduction of the three types of simulated abnormal interactions.

   **Evil NF deletion:** 

   This attack was first proposed by Positive Technologies in their report about standalone 5G core security research. If a rogue NF initiates delete .../nf-instances/{nfInstanceID} to NRF and NRF does not restrict the operations allowed on NF profiles, the rogue NF could delete other NF’s profiles. In case of mass deregistration of the core components, the network will not be able to provide service to subscribers, potentially causing financial losses and reduction in subscriber trust.

   **NF DoS:** 

   This type of attack is about a rogue NF initiating high-frequency invocations to a victim NF, thereby impeding the normal interactions between the victim and other NFs [10]. We simulate this type of attack using the h2load tool to initiate get.../nnrf-disc/nf-instances requests at a high frequency from a rouge NF to the NRF. This service discovery request is common in 5G CN NF interactions and can be initiated by any NF to the NRF.  

   **UE Info extraction:** 

   This type of attack exploits a vulnerability in versions of free5GC prior to v3.0.7, allowing for the malicious extraction of a UE’s subscription information. More specifically, a rogue NF first initiates get .../nnrf-disc/nf-instances to NRF for obtaining the profile of AUSF; then, it can request AUSF’s authentication service by initiating put .../nausf-auth/ue-authentications/{suci}/5g-aka-confirmation to AUSF based on the SUCI of the UE it is interested in. The SUCI, which is the encrypted SUPI, can be transmitted directly and easily obtained. Due to the vulnerability in free5GC, even if the authentication fails (since the rogue NF does not know the correct authentication vector), AUSF will still send the UE’s SUPI back to the rogue NF. With the SUPI in hand, the rogue NF can use it to access various private information about the UE. For instance, the invocation get.../nudm-sdm/{supi}/am-data can be used to retrieve the UE’s access and mobility subscription data, and get .../nudm-sdm/{supi}/nssai can be used to retrieve the UE’s subscribed network slice.

2. normal

   This folder contains interaction data between NFs during the normal operation period of the 5G core network. Similarly, these interaction data are also stored in JSON file format. We divided it into test and training parts.

3. all_URI_templates.csv

   This CSV file contains URI templates for all possible calls between 5G core network NFs. These URI templates were obtained from https://github.com/jdegre/5GC_APIs.

4. involved_uri.txt

   This txt file contains all the URI templates used in our experiment.


More information can be found in our paper:
Y. Tan, J. Liu, Y. Li and J. Wang, "Deep Learning Based Proactive Anomaly Detection for 5G Core Control Plane Network Function Interactions," in IEEE Transactions on Cognitive Communications and Networking, doi: 10.1109/TCCN.2025.3539660.

