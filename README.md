# IMC-prosperity - 2023

# Round-wise details
Round 1
In this round, we worked on pearls and bananas separately. For pearls, we realized that they had a stable price of around 10,000, but there were times when the best bid was 10,002 and the best ask was 9,998. Additionally, there were trades even at -5, -4, +4 and +5 of the mean price (10k), which meant that all we had to do for pearls was market-take and market-make around 10k.

For bananas, we ran a linear regression on the last few timesteps of banana prices to predict the next price. Using this to market-take worked reasonably, and market-making along with market-taking worked quite well. We tried to implement LR-on-the-fly, but this didn't work as well (and with the Lambda error bugs that were prevalent through the competition, it was for the best to skip this approach). We noticed that the banana trends were linear-ish across days (ie, day 2 was more similar to day 1 in LR coefficients than day -1 and so on), which could give an additional boost in PnL.

The manual trading was straightforward in this round. Based on the results of Round 1, we were in 9th place.
