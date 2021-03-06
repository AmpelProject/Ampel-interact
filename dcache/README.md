# The AMPEL dCache local sync system

Processed AMPEL data is stored as TransientViews through dCache. A WebDAV interface is setup to allow this information to be transferred to a local system for further analysis. The CA certificates required to connect to the dCache system using secure protocols can be obtained from the [https://wiki.egi.eu/wiki/EGI_IGTF_Release](IGTF trust anchors).

## Getting started

Executing the [sync-dcache2.sh](sync-dcache2.sh) will script in a `base_dir` will start building a file structure as follows:

```
channel_name
│   macaroon
│
└───manifest
│   │   latest.json.gz
│   │   {previous_manifest_1}.json.gz
│   │   {previous_manifest_2}.json.gz
│   │   ...
│   
└───ZTF19aa
│   └───ab
│        ZTF19aaabxjy.json.gz
│   └───ac
│        ZTF19aaacfji.json.gz
|        ...
└───ZTF19ab
│   └───ae
│        ...
...
```

Each execution of `sync-dcache2.sh` will update one *channel*. A specific authorization token, the `macaroon` file, is needed for each channel. Each token expires after 48h, but is updated as a part of the script execution. This thus needs to be run at least every 48h, otherwise the system will loose access to the server. **The initial macaroon needs to be directly provided by the AMPEL operators, it is not included in this repository.**

The `manifest` directory contains information regarding which transients were modified at which times. The remaining folders contain individual object TransientViews. Before syncing, put the empty manifest file included here [latest.json.gz](latest.json.gz) into the `manifest` directory. The 'ZTF*' directores will be created by the script as needed.


## Accessing the data

The *base_dir* and *channel_name* parameters need to be provided to the `loader` class, as demonstrated in the demo notebooks.



 

