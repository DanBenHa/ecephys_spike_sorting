# ecephys spike sorting

![ecephys_spike_sorting_icon](icon.png)

https://github.com/AllenInstitute/ecephys_spike_sorting

Modules for processing **e**xtra**c**ellular **e**lectro**phys**iology data from Neuropixels probes.

![python versions](https://img.shields.io/badge/python-3.5%20%7C%203.6%20%7C%203.7-blue.svg)


## Overview

These modules take data saved by the [Open Ephys GUI](https://github.com/open-ephys/plugin-gui) and prepare it for spike sorting by [Kilosort2](https://github.com/MouseLand/Kilosort2). Following the spike-sorting step (using the [kilosort_helper](ecephys_spike_sorting/modules/kilosort_helper/README.md) module), we clean up the outputs and calculate mean waveforms and quality metrics for each unit.

This code is still under development, and we welcome feedback about any step in the pipeline.

Further documentation can be found in each module's README file. For more information on Kilosort2, please read through the [GitHub wiki](https://github.com/MouseLand/Kilosort2/wiki).


## Modules

1. [extract_from_npx](ecephys_spike_sorting/modules/extract_from_npx/README.md): Calls a binary executable that converts data from compressed NPX format into .dat files (continuous data) and .npy files (event data)

2. [depth_estimation](ecephys_spike_sorting/modules/depth_estimation/README.md): Uses the LFP data to identify the surface channel, which is required by the median subtraction and kilosort modules.

3. [median_subtraction](ecephys_spike_sorting/modules/median_subtraction/README.md): Calls a binary executable that removes the DC offset and common-mode noise from the AP band continuous file.

4. [kilosort_helper](ecephys_spike_sorting/modules/kilosort_helper/README.md): Generates config files for Kilosort and launches spike sorting via the Matlab engine.

5. [kilosort_postprocessing](ecephys_spike_sorting/modules/kilosort_postprocessing/README.md): Removes putative double-counted spikes from Kilosort output.

6. [noise_templates](ecephys_spike_sorting/modules/noise_templates/README.md): Identifies noise units based on their waveform shape and ISI histogram.

7. [mean_waveforms](ecephys_spike_sorting/modules/mean_waveforms/README.md): Extracts mean waveforms from the raw data, given spike times and unit IDs. Also calculates metrics for each waveform.

8. [quality_metrics](ecephys_spike_sorting/modules/quality_metrics/README.md): Calculates quality metrics for each unit to assess isolation and sorting quality.

Not used: [automerging](ecephys_spike_sorting/modules/automerging/README.md): Automatically merges templates that belong to the same unit (included in case it's helpful to others).


## Installation and Usage

We recommend using [pipenv](https://github.com/pypa/pipenv) to run these modules. From the `ecephys_spike_sorting` top-level directory, run the following commands from a terminal

### Linux

```shell
    $ pip install --user pipenv
    $ export PIPENV_VENV_IN_PROJECT=1
    $ pipenv install
    $ pipenv shell
    (ecephys_spike_sorting) $ pip install .
```
### Windows

This will work in the standard Command Prompt, but the [cmder console emulator](https://cmder.net/) has better compatibility with Python virtual environments.

```shell
    $ pip install --user pipenv
    $ set PIPENV_VENV_IN_PROJECT=1
    $ pipenv install
    $ pipenv shell
    (.venv) $ pip install .
```

### Running Scripts

You can edit one of the processing scripts found in `ecephys_spike_sorting/scripts` and run via:

```shell
    (ecephys_spike_sorting) $ python ecephys_spike_sorting/scripts/example_script.py
```

### Wrapping Up

To leave the pipenv virtual environment, simply type:

```shell
    (ecephys_spike_sorting) $ exit
```

## Entry Points

Installing as a module should automagically expose the aforementioned modules using `setuptools` entry_points

-   extract from npx: `extract-from-npx`
-   depth estimation: `depth-estimation`
-   median subtraction: `median-subtraction`
-   kilosort helper: `kilosort-helper`
-   kilosort postprocessing: `kilosort-postprocessing`
-   noise templates: `noise_templates`
-   automerging: `automerging`
-   mean waveforms: `mean-waveforms`
-   quality metrics: `quality-metrics`


## Level of Support

This code is an important part of the internal Allen Institute code base and we are actively using and maintaining it. Issues are encouraged, but because this tool is so central to our mission, pull requests might not be accepted if they conflict with our existing plans.


## Terms of Use

See [Allen Institute Terms of Use](https://alleninstitute.org/legal/terms-use/)