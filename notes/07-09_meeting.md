# Meeting 25.06.2025

## Fragen:

- How to handle the *time* Dimension?
    - Is it enough to only use one year (withhout time dimension) and take certain countries as training, validation and test countries?
    - Do we use multiple years and use some of them for training, validation and testing?
    - If we use multiple time series, can the country it self be a value?
        - In this case the model could reference previous gini values of the same country.
            - Depending on the use-case this could be "okay"

### Konkrete Fragen

- How do we split our data into train-test-split?
- What time frame should we use?
- Sanity check?
    - One graph for each year