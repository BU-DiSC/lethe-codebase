<H1> Lethe codebase: "Lethe: A Tunable Delete-Aware LSM Engine" </H1>

This repository is the modified version of RocksDB which contains Fade and was used to run the experiments for our latest work: "Lethe: A Tunable Delete-Aware LSM Engine". 

Data-intensive applications fueled the evolution of log structured merge (LSM) based key-value engines that employ the out-of-place paradigm to support high ingestion rates with low read/write interference. These benefits, however, come at the cost of treating deletes as a second-class citizen. A delete inserts a tombstone that invalidates older instances of the deleted key. State-of-the-art LSM engines do not provide guarantees as to how fast a tombstone will propagate to persist the deletion. Further, LSM engines only support deletion on the sort key. To delete on another attribute (e.g., timestamp), the entire tree is read and re-written. We highlight that fast persistent deletion without affecting read performance is key to support: (i) streaming systems operating on a window of data, (ii) privacy with latency guarantees on the right-to-be-forgotten, and (iii) en masse cloud deployment of data systems that makes storage a precious resource

This work is accepted for publication in [SIGMOD 2020](https://dl.acm.org/doi/abs/10.1145/3318464.3389757). You can also access [our website](https://disc-projects.bu.edu/lethe/) for more information. 

<H1> Workload Generation </H1>
To run our experiments we also implemented our own workload generator: https://github.com/BU-DiSC/K-V-Workload-Generator
To generate a workload, simply give 

```
make
./load_gen
```

with the desired parameters. These include: Number of inserts, updates, deletes, point & range lookups, distribution styles, etc. 

<H1> Quick How-To </H1>
To run a simple experiment you can follow this guide:

First, clone the workload generator reposirtory and generate a workload. A simple command would be: 

```
./load_gen -I10000 -Q3000
```

More options are available. Type:

```
./load_gen --help 
```

for more details.

This will generate a workload with 10000 inserts and 3000 point-queries on existing keys. 

Then, move the newly generated workload.txt file in lethe-codebase/examples/\_\_working_branch/ where our API resides. Make sure that the lethe-codebase and the K-V-Workload-Generator repositories are located in the same path.

```
cp workload.txt ../lethe-codebase/examples/__working_branch/
```

After that, make sure that you have also compiled RocksDB. To do that navigate to LSM-Compaction-Analysis/ and run:
```
make static_lib
```

To run the workload, you need to go to examples/__working_branch/ directory and just give:

```
make
./working_version
```

More options are available. Type:

```
./working_version --help 
```

for more details.
