# Notes Samuel

Meine Notizen bevor ich in die Ferien gehe:

Grundsätzlich haben wir nun zwei unterschiedliche Modelle

1. Multimodaler Ansatz ohne GINI
2. Multimodaler Ansatz mit GINI

## Modelle

Ich habe jeweils Mean Absolute Percentage Error (MAPE) als lossfunction benutzt

### Multimodal ohne GINI

- Aufteilung in train/val/test nach jahren
- jedes Netzwerk wird in ein eigenes GAT geladen und sie werden dann in in fully-connected-layers (MLP) kombiniert.
- Aus jedem GAT kommt für jedes Land ein "Node-Embedding" dass die Information aus dem gesamten Netzwerk enthält.

Best result: 4.794276237487793 MAPE

### Multimodal mit GINI

- Gini wird auch als Node Attribut hinzugefügt, zu jedem einzelnen Netzwerk
- train/test/val Split ist nicht nach Jahren sondern wird mit Masking gemacht
- Am schluss gibt es 3 komplett unterschiedliche Datasets für train, test und val
    - Wieder für jedes Jahr ein eigenes Netzwerk
- Bei Länder/Jahren die für das training benutzt werden, wird der GINI (node attribute) auf 0 gesetzt.
- Nur die Länder, bei denen der GINI auf 0 gesetzt wurde, werden für das training (backpropagation) benutzt, die anderen nicht, so können wir data-leakage verhindern
    - es besteht kein data leakage, weil das model, lernt nie von den Ländern bei denen der GINI wirklich auch ein Input als node-feature ist
- beim Validation/Test set sind dann wiederum andere Länder/Jahre auf 0 gesetzt

Best result: 4.259459972381592 MAPE

## Hyperparameter Tuning

Ich habe hier Optuna verwendet, das ist eine library, mit der sich einfach und automatisch hyperparameter tunen lassen.

Der "trainings-code" wird jeweils in eine funktion gepackt, man kann dann die variablen definieren, die Optuna für einem bestimme soll. In unserem Fall sind das folgende:

- hidden_size: anzahl hidden layers in den GAT
- weight_decay
- lr: learning rate
- n_gat_layers: anzahl GAT layers
- n_dim_mlp_layers: anzahl MLP layers in den einzelnen Netzwerken nach GAT und bevor sie zusammengefügt werden
- combination_method: wie werden die einzelnen node-embeddings kombiniert: konkatenation (aneinanderreihung) oder attention (learnable parameter)
- batch_size 
- mlp_variant: unterscheidung zweischen 3 unterschiedlich grossen MLP

Optuna schreibt die resultate jeweils in ein SQLite Datenbank und gibt an, welche parameter die besten sind. Ihr könnt die Resultate analysieren, wie ich das in evaluation\analyze_optuna.ipynb gemacht habe. Ihr könnt auch die SQLite DB mit dem VSCode Optuna Dashboard Plugin analysieren.

## Wie weiter

Es kann gut sein, dass noch etwas potential in den Modellen steckt, z.B. könnte man das MLP am schluss noch etwas komplexer machen.

Man könnte auch mal probieren noch das Jahr und das Land als node attribute hinzuzufügen

### TODO

- Model Evaluation: 
    - extrahieren der besten Hyperparameter aus Optuna und Model *final* trainieren
    - Auswahl des besten Models
    - Evaluation am Test-Set
- Visualisierungen
    - Model Struktur mit Multimodalität
    - Resultate des Models
- Bericht Schreiben
    - Besonder Part 3: Development Economics Analysis (10 points)
        - keine Ahnung was wir da genau machen wollen





