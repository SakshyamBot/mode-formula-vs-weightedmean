# INTRODUCTION AND CLAIM

The standard textbook formula for a class-interval mode is as follows:

$$
\text{Mode} = L + \left(\frac{f_1 - f_0}{2f_1 - f_0 - f_2}\right) \times h
$$

This formula makes 3 primary assumptions:

1. The data is non-discrete and continuous.
2. The modal class isn't either the first/last class, and no other classes with the same frequency exist.
3. The interval in each class is fixed and constant for all.

It primarily takes into account the frequency of the preceding and succeeding classes to find out where the actual mode is, in a continuous data.

However, if the main goal is to take the frequency of the preceding and succeeding class into consideration that acts as a "Push" or "Pull" of the modal value in the current class, we can achieve the same goals with a weighted means approach. Consider the following graph:

![Class-interval frequency distribution of heights](histogram.png)

It's a class-interval frequency distribution. The mode is directly located at the class interval $(64\text{–}65.9)$. However, in a continuous data, the mode will not be exactly at the center of the class, i.e. $76.98$. Rather it will be towards the **left** as the preceding class has a higher frequency. Intuitively, we can come up with a weighted mean approach to solve this. Using the formula:

$$
M_o = \frac{X_{i-1} F_0 + X_{i} F_1 + X_{i+1} F_2}{F_0 + F_1 + F_2}
$$

This treats frequency like a *weight* value assigned to each mean to analyze the push-pull effect (in the same spirit the classic textbook definition works). Because of its very similar intuition with the actual formula, I argue that if:

1. It achieves the same or better result in the computation of mode in class interval data;
2. It makes fewer and simpler assumptions (Occam's Razor);

it should be made a common practice to use in *Statistical Analysis* and *Computational Data Science* due to its simplistic nature while simulating models and ease of intuitive understanding. However, both conditions (1) and (2) must be unanimously true for this.

# METHODOLOGY OF EXPERIMENT

The experiment is meant to be a short observation and conclusion on a curious matter. It follows the following steps:

**1) Writing a Python program to observe the error rate for both formulas and comparing them (completely random dataset).**

- Generated a Python list using `random.randint()` containing 1000 elements. (Pigeonhole principle guarantees at least 1 number repeats at least 10 times.)
- A frequency list was created that counts occurrence of numbers from 0 to 100 with interval 10.
- Max frequency value and its index in the frequency list was extracted and stored.
- Similarly the values of frequency of preceding and succeeding class were also stored.
- The mode value for each formula was calculated and compared with the most repeated value in the actual list.
- This entire process was repeated 1000 times and the total error was calculated and printed.

**2) Same comparison done on a Normal Distribution.**

- Entirely the same experiment with the sole exception of using `random.gauss(mode, 15)` to generate the data list, with `mode` being generated randomly from 0 to 100.

# RESULTS, CONCLUSIONS AND DISCUSSION

The first case was destined for failure. Because mode calculation assumes a quasi-normal distribution, which is not the case here, the error rate skyrocketed. As each number was almost equally likely to reappear, there was no real *mode* in the traditional sense that both formulas rely on. And due to this, the error rate on average hovered around 25 for both cases. It is interesting to note that the weighted mean approach gave less error numerically than the continuous dataset though in the very small 0.01 range. However, consistently.

However, the continuous data for Normal Distribution allowed us to map where the formulas really shine properly. Using the `random.gauss` function allowed us to reduce the error drastically from 25 to 3 or 4.

Unfortunately, the continuous mode formula did win over the weighted mean method here. And consistently I might add. Based on my guess, the weighted mean formula should have worked for small discrete datasets way better than continuous formula. But, should have been overpowered for larger datasets due to *Law of Large Numbers*. This didn't happen.

Furthermore, the error difference between the classical formula and the weighted mean approach was hovering right around 0.9.

As such, due to the failure of predicting mode value via weighted sums, I rescind my hypothesis. However, the interesting results such as:

- The continuous formula working better than the weighted mean for even small discrete values;
- The apparent empirical difference of exactly 0.9 between errors;

are topics I wish to look into further in the future.
