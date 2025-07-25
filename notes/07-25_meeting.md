# Meeting 25.07.

Years: 2000 - 2022

### Handling Missing Data:

- Interpollation for Node and Edge Features
- Masking for Gini

## TODO:

- [ ] Complete Datasets with no NAs
- [ ] Model Setup
    - [ ] Which models exist?
- [ ] Baseline
    - [ ] Predict Gini with classical ML Model (e.g. XGBoost) from Nodefeatures

## Dataset Specification

For each Dimension:

No missing data, either remove 

- Edges:
    - country_a, country_b
        - ISO3
    - year
    - Edge-features
        - numeric or one-hot-encoded
        - normalized
- Nodes
    - country
        - ISO3
    - year
    - node-features
        - numeric or one-hot-encoded
        - normalized

--> save as parquet file: nodes_"dimension".parquet and edges_"dimension".parquet