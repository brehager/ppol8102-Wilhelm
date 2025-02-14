# Cost of Anesthesia Services: Conceptual and Operational Definitions

## Conceptual Definition
The **cost of anesthesia services** refers to the total charges incurred for the administration of anesthesia during medical procedures. This includes fees for the anesthesiologist, anesthesia-related medications, equipment, and other associated costs. The cost may vary depending on factors such as procedure complexity, provider type, geographic location, and insurance reimbursement policies.

## Operational Definition
For this study, the **cost of anesthesia services** is defined as the Medicare reimbursement rate for anesthesia services per procedure, measured in U.S. dollars. The operationalization follows a structured data collection process from Medicare pricing datasets, where cost is recorded as a continuous variable.

---

# Simulating the Cost of Anesthesia Services

## Approach
We simulate the cost of anesthesia services based on theoretical expectations of its distribution. Anesthesia costs typically follow a **right-skewed distribution** due to a small number of high-cost procedures. Therefore, we use a **log-normal distribution** to simulate the data, following recommendations from Gelman, Hill, and Vehtari (Chapters 5.1-5.3).


---

# Sampling Distributions


# Load the dataset
data <- read.csv("~/PhD/Data/2024_pdc_s3_ppl_data_anesthesiology.csv")

# Compute observed mean and median for new and established patients
mean_cost_new <- mean(data$mode_medicare_pricing_for_new_patient, na.rm = TRUE)
median_cost_new <- median(data$mode_medicare_pricing_for_new_patient, na.rm = TRUE)

mean_cost_established <- mean(data$mode_medicare_pricing_for_established_patient, na.rm = TRUE)
median_cost_established <- median(data$mode_medicare_pricing_for_established_patient, na.rm = TRUE)

# Print results
cat("Observed Mean Cost (New Patients):", mean_cost_new, "\n")
cat("Observed Median Cost (New Patients):", median_cost_new, "\n")
cat("Observed Mean Cost (Established Patients):", mean_cost_established, "\n")
cat("Observed Median Cost (Established Patients):", median_cost_established, "\n")

# Simulating Dependent Variable 
set.seed(123)  # For reproducibility

# Log-normal distribution for cost simulation
n <- 1000
meanlog <- log(mean_cost_new)  
sdlog <- 0.5  # Assumed standard deviation

simulated_costs <- rlnorm(n, meanlog, sdlog)

costs <- na.omit(data$mode_medicare_pricing_for_new_patient)  # Remove NA values

# Observed mean and median
observed_mean <- mean(costs)
observed_median <- median(costs)

# Print observed values
cat("Observed Mean:", observed_mean, "\n")
cat("Observed Median:", observed_median, "\n")

# ---- Bootstrapping ----
set.seed(123)  # For reproducibility
n_boot <- 1000  # Number of bootstrap samples
n <- length(costs)

# Bootstrap sampling
bootstrap_medians <- replicate(n_boot, median(sample(costs, n, replace = TRUE)))
bootstrap_means <- replicate(n_boot, mean(sample(costs, n, replace = TRUE)))

# ---- Plot Sampling Distributions ----

# Histogram of bootstrap medians
ggplot(data.frame(bootstrap_medians), aes(x = bootstrap_medians)) +
  geom_histogram(bins = 30, fill = "red", alpha = 0.7) +
  labs(title = "Bootstrapped Sampling Distribution of Median Cost", x = "Median Cost (USD)", y = "Frequency")

# Histogram of bootstrap means
ggplot(data.frame(bootstrap_means), aes(x = bootstrap_means)) +
  geom_histogram(bins = 30, fill = "green", alpha = 0.7) +
  labs(title = "Bootstrapped Sampling Distribution of Mean Cost", x = "Mean Cost (USD)", y = "Frequency")



















# Plot histogram of simulated costs
ggplot(data.frame(simulated_costs), aes(x = simulated_costs)) +
  geom_histogram(bins = 30, fill = "blue", alpha = 0.7) +
  labs(title = "Simulated Distribution of Anesthesia Costs", x = "Cost (USD)", y = "Frequency")

# ---- Sampling Distributions ----
# Bootstrap the median
bootstrap_medians <- replicate(1000, median(sample(simulated_costs, n, replace = TRUE)))

# Plot sampling distribution of median
ggplot(data.frame(bootstrap_medians), aes(x = bootstrap_medians)) +
  geom_histogram(bins = 30, fill = "red", alpha = 0.7) +
  labs(title = "Sampling Distribution of Median Cost", x = "Median Cost (USD)", y = "Frequency")

# Bootstrap the mean
bootstrap_means <- replicate(1000, mean(sample(simulated_costs, n, replace = TRUE)))

# Plot sampling distribution of mean
ggplot(data.frame(bootstrap_means), aes(x = bootstrap_means)) +
  geom_histogram(bins = 30, fill = "green", alpha = 0.7) +
  labs(title = "Sampling Distribution of Mean Cost", x = "Mean Cost (USD)", y = "Frequency")






























## Sampling Distribution of the Median
```r
# Bootstrap sampling for median
bootstrap_medians <- replicate(1000, median(sample(simulated_costs, n, replace = TRUE)))

# Plot distribution of median
ggplot(data.frame(bootstrap_medians), aes(x = bootstrap_medians)) +
  geom_histogram(bins = 30, fill = "red", alpha = 0.7) +
  labs(title = "Sampling Distribution of Median Cost", x = "Median Cost (USD)", y = "Frequency")
```

## Sampling Distribution of the Mean
```r
# Bootstrap sampling for mean
bootstrap_means <- replicate(1000, mean(sample(simulated_costs, n, replace = TRUE)))

# Plot distribution of mean
ggplot(data.frame(bootstrap_means), aes(x = bootstrap_means)) +
  geom_histogram(bins = 30, fill = "green", alpha = 0.7) +
  labs(title = "Sampling Distribution of Mean Cost", x = "Mean Cost (USD)", y = "Frequency")
```

---

# Observed Mean and Median (if data available)
```r
# Assuming real data is available as 'observed_costs'
observed_mean <- mean(observed_costs)
observed_median <- median(observed_costs)

# Print results
cat("Observed Mean Cost:", observed_mean, "\n")
cat("Observed Median Cost:", observed_median, "\n")
```

---

## Summary
This document provides:
1. **Conceptual and operational definitions** of the dependent variable.
2. **Simulated anesthesia cost data** using a log-normal distribution.
3. **Visualization of the simulated distribution**.
4. **Sampling distributions of the mean and median** using bootstrap resampling.
5. **Observed mean and median calculations** if real data is available.

This methodology aligns with statistical recommendations from Gelman, Hill, and Vehtari (2020) and provides a solid foundation for analyzing anesthesia costs.
