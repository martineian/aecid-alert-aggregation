# aecid-alert-aggregation
A method for grouping, clustering, and merging semi-structured alerts. To get started, just clone this repository and execute
```
python3 aggregate.py
```
to run the aecid-alert-aggregation with the default input files and configurations. To change the configuration, edit the aggregate_config.py file. The input files provided in this repository are alerts generated by [aminer](https://github.com/ait-aecid/logdata-anomaly-miner) and [Wazuh](https://wazuh.com/) IDS that were used to analyze the [AIT-LDSv1.1](https://zenodo.org/record/4264796#.X7vQTFAxnmE).

When running the python script, the current status of the aggregation is printed on console. In its standard configuration, the script runs for several minutes and then outputs the generated meta-alerts in the directory specified in the configuration file. The output should look as follows:

```
ubuntu@ubuntu:~/aecid-alert-aggregation$ python3 aggregate.py
delta = 0.5: 125 groups in ['data/ossec/ossec_cup.json', 'data/aminer/aminer_cup.txt']
delta = 5: 19 groups in ['data/ossec/ossec_cup.json', 'data/aminer/aminer_cup.txt']
delta = 0.5: 19 groups in ['data/ossec/ossec_onion.json', 'data/aminer/aminer_onion.txt']
delta = 5: 11 groups in ['data/ossec/ossec_onion.json', 'data/aminer/aminer_onion.txt']
delta = 0.5: 885 groups in ['data/ossec/ossec_insect.json', 'data/aminer/aminer_insect.txt']
delta = 5: 14 groups in ['data/ossec/ossec_insect.json', 'data/aminer/aminer_insect.txt']
delta = 0.5: 919 groups in ['data/ossec/ossec_spiral.json', 'data/aminer/aminer_spiral.txt']
delta = 5: 23 groups in ['data/ossec/ossec_spiral.json', 'data/aminer/aminer_spiral.txt']
Now processing file 1/4...
 Processing groups with delta = 0.5
  Processed group 1/125 from {'nmap'} phase with 2 alerts. New meta-alert 0 generated. (sim=-1.0)
  Processed group 2/125 from {'nmap'} phase with 2 alerts. New meta-alert 1 generated. (sim=0.0)
  Processed group 3/125 from {'nikto'} phase with 19603 alerts. New meta-alert 2 generated. (sim=0.0)
  Processed group 4/125 from {'vrfy'} phase with 2 alerts. New meta-alert 3 generated. (sim=0.0)
  Processed group 5/125 from {'vrfy'} phase with 38 alerts. New meta-alert 4 generated. (sim=0.0)
  Processed group 6/125 from {'vrfy'} phase with 100 alerts. Add group to meta-alert 4 (sim=0.44) representing {'vrfy'}
  Processed group 7/125 from {'vrfy'} phase with 80 alerts. Add group to meta-alert 4 (sim=1.0) representing {'vrfy'}
  Processed group 8/125 from {'vrfy'} phase with 80 alerts. Add group to meta-alert 4 (sim=1.0) representing {'vrfy'}
  ...

 Processing groups with delta = 5
  Processed group 1/23 from {'nmap'} phase with 4 alerts. Add group to meta-alert 22 (sim=0.6) representing {'nmap'}
  Processed group 2/23 from {'nikto'} phase with 6150 alerts. Add group to meta-alert 49 (sim=0.97) representing {'nikto'}
  Processed group 3/23 from {'vrfy'} phase with 766 alerts. Add group to meta-alert 25 (sim=0.82) representing {'vrfy'}
  Processed group 4/23 from {'hydra'} phase with 156 alerts. Add group to meta-alert 26 (sim=0.54) representing {'hydra', 'upload'}
  Processed group 5/23 from {'hydra'} phase with 101 alerts. Add group to meta-alert 26 (sim=0.52) representing {'hydra', 'upload'}
  Processed group 6/23 from {'hydra'} phase with 125 alerts. Add group to meta-alert 26 (sim=0.49) representing {'hydra', 'upload'}
  Processed group 7/23 from {'hydra'} phase with 107 alerts. Add group to meta-alert 26 (sim=0.54) representing {'hydra', 'upload'}
  Processed group 8/23 from {'hydra'} phase with 43 alerts. Add group to meta-alert 26 (sim=0.46) representing {'hydra', 'upload'}
  Processed group 9/23 from {'hydra'} phase with 148 alerts. Add group to meta-alert 26 (sim=0.49) representing {'hydra', 'upload'}
  Processed group 10/23 from {'hydra'} phase with 14 alerts. Add group to meta-alert 27 (sim=0.61) representing {'hydra'}
  Processed group 11/23 from {'hydra'} phase with 131 alerts. Add group to meta-alert 26 (sim=0.48) representing {'hydra', 'upload'}
  Processed group 12/23 from {'hydra'} phase with 126 alerts. Add group to meta-alert 26 (sim=0.54) representing {'hydra', 'upload'}
  Processed group 13/23 from {'hydra'} phase with 32 alerts. Add group to meta-alert 26 (sim=0.5) representing {'hydra', 'upload'}
  Processed group 14/23 from {'hydra'} phase with 184 alerts. Add group to meta-alert 26 (sim=0.5) representing {'hydra', 'upload'}
  Processed group 15/23 from {'hydra'} phase with 79 alerts. Add group to meta-alert 26 (sim=0.54) representing {'hydra', 'upload'}
  Processed group 16/23 from {'upload'} phase with 4 alerts. Add group to meta-alert 37 (sim=0.58) representing {'upload'}
  Processed group 17/23 from {'upload'} phase with 6 alerts. New meta-alert 55 generated. (sim=0.24)
  Processed group 18/23 from {'upload'} phase with 1 alerts. Add group to meta-alert 24 (sim=0.35) representing {'hydra', 'vrfy', 'upload'}
  Processed group 19/23 from {'exploit'} phase with 2 alerts. Add group to meta-alert 24 (sim=0.7) representing {'hydra', 'exploit', 'vrfy', 'upload'}
  Processed group 20/23 from {'exploit'} phase with 2 alerts. Add group to meta-alert 28 (sim=0.62) representing {'exploit'}
  Processed group 21/23 from {'exploit'} phase with 3 alerts. Add group to meta-alert 29 (sim=0.66) representing {'exploit'}
  Processed group 22/23 from {'exploit'} phase with 3 alerts. Add group to meta-alert 29 (sim=0.75) representing {'exploit'}
  Processed group 23/23 from {'exploit'} phase with 4 alerts. Add group to meta-alert 30 (sim=0.58) representing {'exploit'}

Results:
 delta = 0.5: 41 meta-alerts generated
 delta = 5: 15 meta-alerts generated

Meta-alerts are stored in data/out/aggregate/meta_alerts.txt

Alerts are stored in data/out/aggregate/alerts.txt
```

Each line of output corresponds to a group of alerts that occur in close temporal proximity. For each group, the attack phase and group size (i.e., number of alerts in the group) are printed. Moreover, the output indicates whether a group is added to an already existing meta-alert (including the similarity between the group and the meta-alert as well as the attack phase represented by the meta-alert) or whether a new meta-alert is generated. As stated at the end of the output, 41 meta-alerts were generated for a time delta of 0.5 seconds and 15 meta-alerts were generated for a time delta of 5 seconds (use parameter `deltas` in the `agggregate_config.py` file to specify the time deltas).

The directory 'samples' contains several examples that are useful for understanding the aggregation technique. The samples include:
* sample_similarity.py similarities of sample alerts
* sample_group_similarity.py similarities of sample alert groups
* sample_merge.py aggregation of sample alerts
* sample_group_merge.py aggregation of sample alert groups
* sample_hierarchical_clustering.py execution of the hierarchical clustering method on sample data
* sample.py execution of incremental meta-alert generation on sample data (corresponds to scenario 2 in paper)

The directory 'evaluation' contains several scripts that measure the performance of the approach. Note that the respective configurations are inside the scripts instead of the aggregate_config.py file. Evaluation scripts include:
* mds.py generates a similarity matrix for multi-dimensional scaling
* hierarchical_clustering.py generates an R script for plotting a dendrogram
* evaluate.py uses unsupervised clustering for meta-alert generation
* cross_validation.py uses supervised training for alert classification
* noise_evaluate.py measures the robustness of the approach

Copy any of the sample and evaluation scripts into the main directory to execute it, e.g.:
```
cp samples/sample.py ./sample.py
python3 sample.py
```

The output will be generated on the console or in the respective directory in data/out.

If you use any resources from this repository, please cite the following publications:

 * Landauer M., Skopik F., Wurzenberger M., Rauber A.: [Dealing with Security Alert Flooding: Using Machine Learning for Domain-independent Alert Aggregation.](https://dl.acm.org/doi/full/10.1145/3510581) ACM Transactions on Privacy and Security, 25(3), 1-36. \[[PDF](https://dl.acm.org/doi/pdf/10.1145/3510581)\]
