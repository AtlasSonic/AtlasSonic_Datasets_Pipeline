# AtlasSonic_Datasets_Pipeline
This Repository aims to contain the Network based Dtasets used to train and test AtlasSonic ML approaches and models. Initially, it will consist of SOA Datasets that will be dynamically updated. Each Dataset will be presented with two subsets, the original Data (mainly pcaps files and original CSVs) and Datas that has been processed using AtlaSonic teams methods. 
The Startup Datasets are: 
                        - CIC-IDS-2017
                        - CSE-CIC-2018
                        - UNSW-NB-15
                        - ToN-IoT
                        - BoT-IoT
                        - USTC-2016
                        - CUPID
                        - URG-16
                        - STL-HDL
                        - UKM-IDS20
 The Original Datasets with their mureged Pcaps are stored at: 
                        - /lustre/nlp_team-um6p-st-sccs-id7fz1zvotk/IDS/mekki/ids_data
                        - /lustre/nlp_team-um6p-st-sccs-id7fz1zvotk/IDS/205.174.165.80/CICDataset
 
 The criteria used to choose these Datasets are: Reproductiblity, Ataacks diversity and Ground Truth Data availability.
 
 To process these Datasets, we carried out the following process:
                        - Fixing the original Pcaps with PcapFix tool to make sure that all packet files are not damaged
                        - Murging Pcap files (depending on the Dataset structure)
                        - Extracting Netwok features from the murged pcaps using NFStream tool
                        - Labelling the extracted Data using Ground Truth information published by the Datasets Owners
                        - Analyzing the murged pcaps with Suricata using updated detection rules
                        - Converting Suricata JSON files into CSV files in order to identifiy Alerted Flows 
                        - Cross the labeling results (Suricata Vs Ground Truth Annotation). To do that, we used the 5-Tuples and Timestap to                                  compare the flows classification

Suricata analysis results are stored at: /lustre/nlp_team-um6p-st-sccs-id7fz1zvotk/IDS/suri_souf/Annotation_Task/Suricata

On an other hand, the idea behind reproducting the choosen Dataset is to extract flow with many Timeout value in order to assess their effect on models performance. to do so, we decided to use two values for Idle_Timeout (30s and 60s) and four values for Active_timeout (120s, 300s,  3060s et 3600s). In this regard theses two parameter indicate:
                        - Idle_Timeout: How many seconds the NFSTream Streamer should wait to close the flow and strart a new one (inacttivity time                           after the last received packet)
                        - Active_Timeout: the max duration of an active flow
Hence, each Active and Idle combination will provide a Sub-Dataset. So for each original Dataset we weill have 8 subdatasets named as follows:
                        - 30120, 30300, 3060 and 303600
                        - 60120, 60300, 6060 and 603600
                    
The Datsets processing results are stored at: /lustre/nlp_team-um6p-st-sccs-id7fz1zvotk/IDS/suri_souf/Annotation_Task. Each Dataset file has the following structure:
                        - The NFStream extraction file for each teimout combination
                        - The CSV result file for each teimout combination
                        - The crossing results file
                        ______________________________________________________________________________________
