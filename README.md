# condorLite
A lightweight setup to scale your analysis using Condor.

Documentation is aligned towards analysis targeting [Opendata](http://opendata.cern.ch/) releases from CERN.

* current setup assumes a cluster like environment with a common filesysem mount for the condor worker nodes.

## Setup the working environment.
Clone the repository.
```
git clone  https://github.com/ats2008/condorLite.git
cd condorLite/
```

- Cutomize `templates/run_template.sh` to suit your needs ( leave it unalterted for a template job setup ).
- Create a filelist with the list of files on which you want to run your jobs. ( see a template filelist in `filelists/DYJetsToLL_13TeV_MINIAODSIM.fls` ) ( see [cernopendata-client wiki](https://github.com/ats2008/condorLite/wiki/cernopendata%E2%80%90client) )


## Scaling up your Analysis.

For making a set of analysis jobs :
 - from an existing filelist.
```
python3 scripts/makeCondorJobs.py  -f filelists/DYJetsToLL_13TeV_MINIAODSIM.fls --run_template templates/runScript.tpl.sh  --tag DYJetsToLL_v1 -j 5 -e 2000
```
 - from `recid` of a dataset. This command will also export the filelist for the dataset into a file.
```
python3 scripts/makeCondorJobs.py --recid 16446 --tag DYJetsToLL_v1 -n 2 -j 4 -e 5000 --run_template templates/runScript.tpl.sh
```


see `python3 scripts/makeCondorJobs.py -h` for more details

#### TODOs
* add support for non-xrootd file acces using cernopendata-client
* update setup for completely detached file system in condor worker nodes. 
* Add support for a sample analysis.C / analysis.py  and its outputs. 
