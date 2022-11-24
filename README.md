# APTAAnomaly ##
Windows event log anomaly detection powered by ATPA technologies

This repository contains a [velociraptor](https://docs.velociraptor.app/) artifact. It collects windows event log data, learns models from those logs, and uses those models to detect anomalous behavior. 

## NOTE ##
This is a prerelease, the tools used in this artifact are still under heavy development. There will most likely be bugs, but we would love to hear about any [issues](https://github.com/APTA-Technologies/APTAAnomaly/issues) you encounter so we can fix them as quickly as possible. Any other kind of constructive feedback is also very welcome!

## Parameters ##

If you run APTAAnomaly during an incident and want results asap, you can set `CPULoad` to 1. If you want to run it on a machine still in production, you can set `CPULoad` to a lower number, e.g. `0.125`. It's the fraction of cores to use for processing the log data rounded up to the next full number of cores.

## Usage ##

First, get the artifact into velociraptor. An easy way to do this is by going to the `view artifacts` tab in the web UI, pressing the `add an artifact` button and copying the contents of the `Windows.EventLogs.APTAAnomaly` file into the editor that pops up.

Then, to prevent spamming github with download requests for the artifact zip file, click the APTAAnomaly link under `Tools`
![image](https://user-images.githubusercontent.com/5961113/193897250-97781aa2-e7e6-4437-94f9-2139b591f92b.png)

And hit `Serve Locally`. Note, you may have to click `Materialize Hash` first.
![image](https://user-images.githubusercontent.com/5961113/193897659-1eb438d7-5f90-4db0-ab51-65342541be38.png)

After this, you can run the artifact from a notebook with the following VQL:
```SQL
SELECT * FROM Artifact.Windows.EventLogs.APTAnomaly()
```

Which after a few minutes (depending on the size of your logs) will result in an output that should look something like this:
![image](https://user-images.githubusercontent.com/5961113/193900351-8dd75f64-7a19-44e6-961d-7675eeb094fb.png)

This is essentially a table containing the log lines from each evtx file, sorted by novelty score.

## Want more? ##

Check out our timeline explorer. It ingests the annoated log files and makes it really easy to drill down, correlate, and explore all the logs.

[QuickOvervierwofTimelineExplorerandAPTAnomaly.webm](https://user-images.githubusercontent.com/4000627/203807596-4a31729f-ffa8-475f-844f-68af0b3f4544.webm)
