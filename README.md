# IMC-prosperity - 2023

# Round-wise details
Round 1
## Algorithm challenge

The first two tradable products are introduced: PEARLS and BANANAS. While the value of the PEARLS has been stable throughout the history of the archipelago, the value of BANANAS has been going up and down over time. Develop your initial trading strategy and write your first Python program to get off to a good start in this world of trading and market making. Even if the price of a product moves very little or in a very unpredictable way, there might still be clever ways to profit if you both buy and sell.

Position limits for the newly introduced products:
- PEARLS: 20
- BANANAS: 20

## Manual challenge

You get the chance to do a series of trades in some foreign island currencies. The first trade is a conversion of your SeaShells into a foreign currency, the last trade is a conversion from a foreign currency into SeaShells. Everything in between is up to you. Give some thought to what series of trades you would like to do, as there might be an opportunity to walk away with more shells than you arrived with.

In this round, we worked on pearls and bananas separately. For pearls, we realized that they had a stable price of around 10,000, but there were times when the best bid was 10,002 and the best ask was 9,998. Additionally, there were trades even at -5, -4, +4 and +5 of the mean price (10k), which meant that all we had to do for pearls was market-take and market-make around 10k.

For bananas, we ran a linear regression on the last few timesteps of banana prices to predict the next price. Using this to market-take worked reasonably, and market-making along with market-taking worked quite well. We tried to implement LR-on-the-fly, but this didn't work as well (and with the Lambda error bugs that were prevalent through the competition, it was for the best to skip this approach). We noticed that the banana trends were linear-ish across days (ie, day 2 was more similar to day 1 in LR coefficients than day -1 and so on), which could give an additional boost in PnL.

The manual trading was straightforward in this round. Based on the results of Round 1, we were in 40th place.

# Round 2
## Algorithm challenge

During this second round of the Prosperity challenge, you again get the chance to trade the same products as in round 1. However, in addition to the existing products two new products are introduced, COCONUTS as well as PINA_COLADAS. The prices of these products fluctuate quite a bit. But might they have something in common?

Position limits for the newly introduced products:

- COCONUTS: 600
- PINA_COLADAS: 300

## Manual challenge

A large group of ducks request a price for your pineapples. They will only buy pineapples at the 50% best prices that they get, so players have to be competitive. However, as the pineapple price is expected to settle at the average price that the ducks bought their pineapples at, you definitely want to make sure that you don’t sell below that price, or you’ll make a loss on your trade.

For the Coconuts/Pina Coladas, Shrut wrote up code to perform pair-trading (arbitraging pina colada - 15/8 * coconut); something else we tried was momentum-based trading, but this didn't give a PnL as high as pair-trading, so we mostly submitted the first code we came up with.

For the manual round, we submitted a guess of 9,777 based on a simulation. This was good enough to net us some profit, with the median price of the bottom 50% being 9,685. Shockingly, we got a score of below -120k in the algorithmic trading in this round, which dropped us from 40th place to... 376th place!!!

# Round 3
## Algorithm challenge

Next to the products from the previous two rounds, players are now able to go on the market and trade DIVING_GEAR as well. It’s of course obvious that diving is no fun when there’s nothing to see. Maybe the amount of DOLPHIN_SIGHTINGS reported might therefore move the price of the DIVING GEAR a bit? DOLPHIN_SIGHTINGS are, of course, just information and cannot be traded.

Position limits for the newly introduced products:

- DIVING_GEAR: 50
- BERRIES: 250

## Manual challenge

The ducks are back, and they behave exactly the same as in round two. However, after the previous round you had the opportunity to see what the rest of the market was thinking. Could you use that information to predict what your peers will do next?

After the shock of dropping to an extremely low rank, we decided to not participate in Prosperity anymore. Still, Shrut, Dhariya & Namam wrote some code for Berries and Diving Gear, which seemed to work reasonably. The ideas were as follows: For berries, he hardcoded some values of the curve (buy at timestamp 350k, sell at 500k, either buy or sell at 750k depending on the overall day's trend). For diving gear, Shrut noticed that Dolphin sightings would increase or decrease by a huge amount (+-5 or higher) if there was a true signal; a small change such as +-2 from the last dolphin sighting was very likely noise.

For the manual trading, I decided to enter 9,959 after a bit of eyeballing, which was close to the optimal score of 9,969. Our algorithm also worked extremely well this round, propelling us from 926th to 60th place (we had the overall highest score this round, based on https://jmerle.github.io/imc-prosperity-leaderboard/). Looking at these results, my suspicion grew about our Round 2 algorithm, and I asked the moderators once again for our logs; it turned out that our algorithm was actually judged incorrectly! Therefore, though we were officially 298th place, we knew that we were 20th place at the moment in reality.

# Round 4
## Algorithm challenge

Picnics are all the rage at the moment in the Archipelago, likely owing to the splendid weather. Everyone’s favorite PICNIC_BASKET is now a tradable product. This classy picnic basket contains three things:

1. a BAGUETTE
2. a nice DIP 
3. a UKULELE for the music
4. a PICNIC_BASKET containing all three

All four of the above products can now also be traded on the island exchange. Are the picnic baskets a bit expensive for you taste? Then perhaps see if you can get the contents directly.

Position limits for the newly introduced products:

- BAGUETTE: 150
- DIP: 300
- UKULELE: 70
- PICNIC_BASKET: 70

## Manual challenge

The latest edition of the island newspaper has just come in, and there are all kinds of headlines. Maybe some of these might offer a nice opportunity to trade on? Get your purse ready and buy or sell yourself some of the stocks that are the talk of the town. Be careful how you allocate your capital though, diversification is typically a good thing in trading. Especially if trading fees get progressively higher, the bigger your position in a single stock!

Once we realized that we actually had a fighting chance (and were not on flights anymore), we spent more time actually working on our algorithms compared to the last 2 rounds. For the Picnic basket group, we decided to use the same pair trading strategy, assuming that the basket had a premium of 375$ attached to it (ie, arbitraging picnic basket - 4 * dip - 2 * baguette - ukulele - 375), and fine-tune this. I ended up writing a backtester that helped us test all of our strategies by using the run function (before, we were only testing via separate simulations via iterating over past data, which was annoying to change in two places.)

For the manual trading round, we found that if the stock moves 
x% and if we invest y%, the output function would be 75xy - 90y^2
, which would put the optimal y value at y = 2.5x/6. Using this idea, we simply individually bet on the amount we thought each stock would move, invested that much, and iterated a bit. We ended up investing about 100% of our capital.

After Round 4, we jumped to Rank 5 from Rank 60 (though we knew we actually went from Rank 3 -> 5). Our manual trading score was 75k, whereas the best score we heard was around 115k; our algorithm score was 175k, which was a bit lower than expected. We had an outside shot at winning; the difference between us and the top team was only 130k.

# Round 5
## Algorithm challenge

The final round of the challenge is already here! And surprise, no new products are introduced for a change. Dull? Probably not, as you do get another treat. The island exchange now discloses to you who the counterparty is you have traded against. This means that the `counter_party` property of the `OwnTrade` object is now populated. Perhaps interesting to see if you can leverage this information to make your algorithm even more profitable?

For Round 5, my first order of business was to extend our backtester to handle market orders, while Konstantin ran some preliminary data analysis on the market order trades. We ended up implementing the following changes:

We realized that in the Picnic Basket bucket, Picnic Basket always had heavily positive PnL; this meant that the price of all the products were a leading indicator for the future price of picnic baskets, which made sense. Therefore, we decided to only trade Picnic Baskets on the signal of (picnic basket - 4 * dip - 2 * baguette - ukulele - 375).

We realized Olivia bought at the lowest point and sold at the highest point, so we used her exclusively to trade Ukuleles. For berries, her signal was used to augment our existing code and made our algorithm slightly better.

We did the same thing as point 1 for pina coladas and coconuts (ie, only trade pina coladas); this was not necessarily the best choice or a perfectly justified one (since we did not have a great increase in results from doing this), but it was a choice we made.

We further decided to never trade Dip, Baguettes or Coconuts. Some more ideas we considered (but could not get to work reliably) were:

Perform market making on dip, due to it having a large spread and low price deviation (except for a sharp dip at some point); while this performed very well on average, the sharp dip lost us a lot of money, and therefore we couldn't get this to work in a short amount of time.

Use Camilla as a signal for berries: We noticed that Camilla would constantly make profits, so she might have been a good signal for berries; however, she also got a lot of edge (great deals on the correct side of the spread), and we could not emulate her success better than how our own algorithm + Olivia's was performing.

Use some sort of momentum based ideas for Baguettes: we noticed that Baguettes usually go on a strong upward or downward run, which allowed momemtum-based strategies to work well. We were able to make a consistent 5-20k PnL on one of our signals, but changing the parameters slightly changed these numbers from -30k to 50k. We ended up not taking the risk here, and removed this signal.

Some of our main ideas in the final round were to be rigorous about not overfitting, and avoiding complicated models due to the lack of test data. In retrospect this was justified, looking at the lower scores most other teams in the top 10 got in Round 5.

Final results
After all was said and done, we ended up in... 27th place.
But when all was said and done, this was a fun competition in which we got to work on some cool ideas; so thank you to all of the people behind Prosperity, and everyone who participated - it was exciting participating alongside yall! :)
