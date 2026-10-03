# Data setup

This project uses a subset of the **CIC-DDoS2019** dataset from the Canadian Institute for Cybersecurity at the University of New Brunswick.

Official source: https://www.unb.ca/cic/datasets/ddos-2019.html

## Files used by the historical experiment

The recovered Phase 2 notebook processed these eight attack CSVs:

```text
DrDoS_DNS.csv
DrDoS_LDAP.csv
DrDoS_MSSQL.csv
DrDoS_NTP.csv
DrDoS_NetBIOS.csv
DrDoS_SNMP.csv
DrDoS_SSDP.csv
DrDoS_UDP.csv
```

Each source file contains labeled network-flow records, including benign traffic and the corresponding DDoS attack class.

## Historical sampling procedure

The April 2025 notebook read each CSV in chunks and retained:

- 300 `BENIGN` records per source file
- 5,000 attack records per source file

After aggregation and splitting, the historical notebook reported:

| Split | Rows | Columns before later preprocessing |
| --- | ---: | ---: |
| Training | 29,680 | 87 |
| Test | 12,720 | 87 |

The reproduction pass will verify these counts from the official source data before treating them as final reproducible artifacts.

## Expected local structure

Raw data should be kept outside Git history:

```text
data/
├── README.md
├── raw/
│   ├── DrDoS_DNS.csv
│   ├── DrDoS_LDAP.csv
│   ├── DrDoS_MSSQL.csv
│   ├── DrDoS_NTP.csv
│   ├── DrDoS_NetBIOS.csv
│   ├── DrDoS_SNMP.csv
│   ├── DrDoS_SSDP.csv
│   └── DrDoS_UDP.csv
└── processed/
    └── generated during reproduction
```

## Why the CSVs are not committed

The original GitHub repository contained zero-byte CSV placeholders rather than usable data. Those placeholders were removed during repository cleanup.

The official CIC-DDoS2019 files are large and should be downloaded from the authoritative source instead of duplicated in this repository. This also keeps the research workflow explicit: source data → deterministic preparation → generated train/test artifacts.

## Dataset citation requirement

The University of New Brunswick allows redistribution of CIC-DDoS2019, but asks that use or redistribution include citation of the dataset and its associated paper:

> Iman Sharafaldin, Arash Habibi Lashkari, Saqib Hakak, and Ali A. Ghorbani, “Developing Realistic Distributed Denial of Service (DDoS) Attack Dataset and Taxonomy,” IEEE 53rd International Carnahan Conference on Security Technology, 2019.
