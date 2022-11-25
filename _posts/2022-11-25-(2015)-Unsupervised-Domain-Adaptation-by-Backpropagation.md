# (DANN) Unsupervised Domain Adaptation by Backpropagation

- Overall structure of the proposed model:

[image]

- Overall optimization problem:

[image]

[image]

- After gradient reverse layer, the optimization problem becomes:

[image]

## KEY RESULTS

1. Minimizing the label prediction loss contributes to learning discriminative features
2. Maximizing the domain classification loss contributes to learning domain-invariant features
3. Training the domain discriminator is closely related to the estimation of HΔH divergence