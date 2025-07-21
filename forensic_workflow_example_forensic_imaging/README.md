# Forensic workflow example: forensic Imaging

## Introduction
This example shows how SOLVE-IT can be used to examine a forensic workflow and consider the weaknesses in the process and evaluate the mitigations in place.

## An example process

For this example we can take the process required to acquire data from a hard disk. 

Referred to broadly as 'disk imaging', 
when mapped as a *process* against SOLVE-IT techniques, 
there are several that are used. For example:

* T1012: Hardware write blocker[^1]
* T1002: Disk imaging
* T1025: Writing to a forensic image
* T1042: Disk image hash verification

[^1]: Some workflows may use software write blockers (T1013), but this example assumes hardware devices in place.

## Using SOLVE-IT

The utility python script `generate_evaluation.py` can be used here.

Running the script with those technique IDs as parameters, compiles an Excel spreadsheet that extracts the weaknesses and available mitigations into a reviewable form.

```
python generate_evaluation.py T1012 T1002 T1025 T1042
```


This output will highlight that, for example, under the technique T1012: Hardware write blocker, there are currently three potential weaknesses

* Hardware write blocker fails to prevent modifications to the attached device.
* Hardware write blocker hides the existence of an HPA.
* Hardware write blocker hides the existence of an DCO.

The figure below shows a section of the example output mapping the available mitigations against those potential weaknesses.

![eval_example_imaging_write_blockers.png](eval_example_imaging_write_blockers.png)

This allows the overall process to be reviewed, and the dropdowns used to record whether mitigations are in place or not. For example, for W1118: Hardware write blocker fails to prevent modifications to the attached device, there are three potential mitigations indexed:

* M1071 Thorough testing of write blocker against multiple targets to ensure that writes are not possible.
* M1072 Regular checks for hardware write blocker firmware updates.
* M1073 Subscription to notifications from write blocker vendor for firmware updates or identified problems.

A full example .XLXS file for this illustration is available [here](case_evaluation-imaging-example.xlsx), generated in the exact manner described above. 

## Extending this with 'lab configurations'

The 'lab configuration' option is designed to automate completion of some of the fields in the generated spreadsheets. There are several reasons why can be useful:

* A standard workflow is always used in a specific way so 'NA' could be always auto-populated. e.g. a lab never uses software write blockers, only hardware write blockers, so _M1008: Use software write blocker_ should always be '_NA_' and _M1007: Use hardware write blocker_ could always be 'Y'.
* A tool has provided a configuration script, describing the testing that has been performed, thus auto populating Y where tool testing for specific mitigations has been performed by the vendor or open source tool developer.

Lab configurations are JSON files (examples are provided [here](https://github.com/SOLVE-IT-DF/solve-it/tree/main/lab_config_examples)) and an extracts are shown below. Tehy all illustrate how mitigations for specific weakness can be auto-populated with a value


This first extract illustrates that testing of a specific setup may be done as part of lab quality assurance, so this can be captured: 

```
{
  "Lab config notes": "This is a demo to be used with: generate_evaluation.py T1002  --lab_config ../lab_config_examples/example_lab.json ",
  "T1002:Disk imaging": {
    "W1006": {
      "M1005": {
        "status": "Y",
        "notes": "Standard imaging setup tested with HPA disk TTP-HPA-01"
      }
    },
    "W1007": {
      "M1006": {
        "status": "Y",
        "notes": "Standard imaging setup tested with DCO disk TTP-DCO-01"
      }
    },

```


The second extract illustrates that some mitigations are not possible in a specific lab environment, e.g. only hardware write blockers are used, not software ones (so NA is applied automatically),  physical disk repair is not conducted at this lab, and tooling for remapped sector recovery (e.g. G-lists) is not availabe in this lab (so both are given a value of N). The notes are also automatically added to a spreadsheet generated that uses this lab config file.  

```
      "M1008": {
        "status": "NA",
        "notes": "Software write blockers are not used"
      }
    },
    "W1136": {
      "M1089": {
        "status": "N",
        "notes": "Physical repair not undertaken at this lab"
      }
    },
    "W1143": {
      "M1102": {
        "status": "N",
        "notes": "Tooling for recovery of remapped sectors not available at this lab"
      }
    }
  }
}
```



To use a lab configuration the --lab_config option can be used. 

```

python generate_evaluation.py T1002  --lab_config ../lab_config_examples/example_lab.json

INFO: Loaded 117 techniques.
INFO: Loaded 188 weaknesses.
INFO: Loaded 137 mitigations.
INFO: Building reverse indices for performance optimization...
INFO: Reverse indices built: 184 weakness->technique, 136 mitigation->weakness, 136 mitigation->technique
INFO: Loaded objective mapping 'solve-it.json' with 17 objectives.
INFO: Lab configuration loaded from: ../lab_config_examples/example_lab.json
Max mitigations: 10
['T1002']
INFO: Techniques in lab config: ['T1002:Disk imaging']
INFO: Weaknesses in lab config: ['W1006', 'W1007', 'W1014', 'W1136', 'W1143']
INFO: Mitigations in lab config: ['M1005', 'M1006', 'M1007', 'M1008', 'M1089', 'M1102']
Evaluation workbook successfully generated at: output/solve-it_evaluation_workbook.xlsx

```

The screenshot below shows the auto-populated values in the generated spreadsheet when using the sample lab configuration file example_lab.json.

<img width="1453" height="381" alt="image" src="eval_example_lab_config.png" />


  



