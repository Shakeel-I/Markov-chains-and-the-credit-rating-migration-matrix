# Markov Chain Application for IFRS 9 PD Term Structures in SAS

<img width="797" height="237" alt="image" src="https://github.com/user-attachments/assets/d168b223-dd39-4ae4-bae3-0891b0b8b056" />

This SAS approach uses a Markov chain to quantify credit rating migration risk by modeling ratings as discrete states and transitions between them over time. The core idea is that an asset’s future credit quality depends only on its current state, not on the path taken to reach it. In the code, the states are A, B, C (performing) and Default (an absorbing state). The transition matrix P encodes one-year transition probabilities, where each row sums to 1 and each entry P_ij represents the probability of moving from state i to state j in one year. For example, from A the model assigns a 80% chance to stay in A, 15% to migrate to B, 4% to C, and 1% to Default. The final column captures the probability of default, used for Stage 1 ECL under IFRS 9.

<img width="500" height="375" alt="image" src="https://github.com/user-attachments/assets/09bb83ad-e569-4bcc-8694-d0d0bf07141b" /><img width="500" height="375" alt="image" src="https://github.com/user-attachments/assets/a7c78e61-ef25-497c-803e-dd3b64081604" />

The analysis begins with a synthetic dataset of observed transitions, illustrating how firms might migrate between ratings or default. Using PROC IML, the code performs a point-in-time (PIT) calculation of the 1-year transition matrix and then propagates it across a 10-year horizon to derive both cumulative (lifetime) PD and marginal (annual) PD for each rating. The cumulative PD tracks the probability of default by the end of year t, while the marginal PD isolates the incremental default probability in each specific year. This distinction is critical for IFRS 9, which requires forward-looking PDs and lifetime credit risk assessment.

<img width="798" height="379" alt="image" src="https://github.com/user-attachments/assets/abc7b546-ad85-4266-973c-30cf10ea21eb" />


The implementation includes data reshaping for plotting, producing two visualizations: (1) cumulative PD curves by rating over 10 years, and (2) marginal PD bars by year and rating. A final tabular report presents Year, Cum_PD, and Marg_PD values with clear footnotes explaining the definitions and their relevance for Stage 2 ECL calculations.

Overall, this SAS workflow operationalizes a Markov-based framework to estimate and communicate both lifetime and annual default probabilities, supporting credit risk management, pricing, and regulatory reporting under IFRS 9.
