```mermaid
flowchart TB
A[ref. PIV] ==> D[PIV distance]
B[ref. PathCV] ==> D
C[ref. PIV-PathCV] ==> D
D ==> E[PIV-PathCV mapping]
E ==> F[PIV-PathCV metadynamics]
click A "https://pubs.aip.org/aip/jcp/article-abstract/139/7/074101/73227/Structural-cluster-analysis-of-chemical-reactions?redirectedFrom=fulltext" "reference for PIV"
click B "https://pubs.aip.org/aip/jcp/article-abstract/126/5/054103/187372/From-A-to-B-in-free-energy-space?redirectedFrom=fulltext" "reference for PIV"
click C "https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.119.245701" "reference for PIV-PathCV"
click D "PIV_distance.md" "Associating PIVs to system configurations PIVs and cmputing distances"
click E "PIV-PathCV_driver.md" "Mapping a trajectory into PIV-PathCV space"
click F "PIV-PathCV_meta.md" "Biasing a simulation in the PIV-PathCV space"
```
