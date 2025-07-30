# Notes Samuel

## Model Building

- Multimodal Model:
    - First use a separate GAN for each network
    - https://chatgpt.com/c/688390b6-f08c-832d-ace6-9329e5894bde
    - https://medium.com/@arpanroy_43094/building-a-multimodal-classifier-in-pytorch-a-step-by-step-guide-a6dbd9900802
- Monolith-GAN
    - One large model with one huge dataset
    - implement with masking
    - "Autoencoder" layer before GAN

## Ideas

### Baseline Models

- XGBoost predicting gini from node attributes
- GNN predicting gini without edge-attributes

### Missing Data

- To *interpolate* missing data one network must somehow have information of the other networks.
    - cross-attention?
    - one huge network with all kinds of links

## Questions

- How can we predict the Gini for countries which have a Gini?
    - The network is predicted as a whole...



- If we separate the networks, how can the different networks be reallly combined.
    - eg. in case of missing data
    - If we completely separate the networks we lose potential information
- Countries with missing data in GINI will most likely also have missing data in other data sources
- 