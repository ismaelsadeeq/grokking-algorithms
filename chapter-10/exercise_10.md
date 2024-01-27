EXERCISES

10.1 In the Netflix example, you calculated the distance between two
different users using the distance formula. But not all users rate
movies the same way. Suppose you have two users, Yogi and Pinky,
who have the same taste in movies. But Yogi rates any movie he
likes as a 5, whereas Pinky is choosier and reserves the 5s for
only the best. They’re well matched, but according to the distance
algorithm, they aren’t neighbors. How would you take their
different rating strategies into account?

To address this, one approach is to normalize their rating strategies by taking the average of their ratings and using that value to calculate the distance, rather than the raw rating values. To calculate the average, each rating should be divided by the maximum possible rating. For instance, if the rating scale is from 1 to 5, the normalization would involve dividing each rating by 5.

Additionally, to further accommodate different rating strategies, if both ratings are greater than 0.5, both ratings could be scaled up to their total value. This adjustment aims to bring them closer together in the calculated distance.

This normalization approach helps account for variations in rating strategies and is a common technique in collaborative filtering systems.

10.2 Suppose Netflix nominates a group of “influencers.” For example,
Quentin Tarantino and Wes Anderson are influencers on Netflix,
so their ratings count for more than a normal user’s. How would
you change the recommendations system so it’s biased toward the
ratings of influencers?

You could give each influencer a biased rating e.g twice the its current rating.

Suppose Jon, Peter, and Wes Anderson rate a movie 3, 4, and 5, respectively.
If the normal weight is 1 and the weight for influencers is 2, the biased ratings would be 3, 4, and 5 for Jon, Peter, and Wes Anderson, respectively.
The overall biased rating would then be (3 + 4 + 5 + 5 + 5) / 5 = 4.4.

10.3 Netflix has millions of users. The earlier example looked at the five
closest neighbors for building the recommendations system. Is this
too low? Too high?

Too low, if you have N data set sets, you should look for sqrt(n) neigbors