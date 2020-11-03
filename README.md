# Supplementary material description

This page contains additional details about the experimental setup discussed in the paper _Effective data pre-processing for AutoML_.

## Transformations and Operators

The first task in the process is deciding the kinds of transformations to be considered. In this work, they are the following:

- **Encoding (_E_)**: The process of transforming categorical attributes into continuous ones.
- **Normalization (_N_)**: The process of normalizing continuous attributes such that their values fall in the same range.
- **Discretization (_D_)**: The process of transforming continuous attributes into categorical ones.
- **Imputation (_I_)**: The process of imputing missing values.
- **Rebalancing (_R_)**: The process of adjusting the class distribution of a dataset (i.e. the ratio between the different classes/categories represented).
- **Feature Engineering (_F_)**: The process of defining the set of relevant attributes (variables, predictors) to be used in model construction.

An operator is an actual instantiation/implementation of a kind of transformation. Thus, several operators may implement the same kind of transformation, each having its own set of parameters.
For our experiments, we selected the operators and parameters from those available in the [Scikit-learn framework](https://scikit-learn.org):

| Trans. Kind | Input | Output | Operator | Parameters  |
|---|---|---|---|---|
| **Encoding (_E_)** | CA | CO | Ordinal Encoder | |
| | | | One Hot Encoder | |
| **Normalization (_N_)** | CO | CO | Standard Scaler | <li>with_mean: [True, False]<li>with_std: [True, False] |
| | | | Power Transform | |
| | | | Min Max Transform | |
| | | | Robust Scaler | <li>quantile_range: [(25,75), (10,90), (5,95)]<li/>with_centering: [True, False]<li/>with_scaling: [True, False] |
| **Discretization (_D_)** | CO | CA | KBins | <li/>n_bins: [3, 5, 7]<li/>encode: ['onehot', 'onehot-dense', 'ord.']<li/>strategy:['uniform', 'quant.', 'kmeans'] |
| | | | Binarization | threshold: [0, 0.5, 2, 5] |
| **Imputation(_I_)** | CA/CO | CA/CO | Univariate | strategy: ['most_freq.', 'constant'] |
| | | | Multivariate | <li/>initial_strategy: ['most_freq', 'const.']<li/>order: ['asc', 'dsc', 'rom', 'arab', 'rand'] |
| **Rebalancing (_R_)** | CA/CO | CA/CO | Near Miss | n_neighbors:[1, 2, 3] |
| | | | Condensed KNN | n_neighbors:[1, 2, 3] |
| | | | SMOTE | k_neighbors: [5, 6, 7] |
| **Feature Engineering (_F_)** | CA/CO | CA/CO | PCA | n_components: [1, 2, 3, 4] |
| | | | Select K Best | k: [1, 2, 3, 4] |
| | | | PCA + Select K Best | <li/>n_components: [1, 2, 3, 4]<li/>k: [1, 2, 3, 4] |
