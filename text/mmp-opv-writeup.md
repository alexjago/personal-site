# MMP-OPV

When designing an parliamentary electoral system, there are two main considerations. First, how are people represented at the local level? Second, how are the people represented as a whole?

## Local level

For local representation, a common paradigm is to split the country up into a large number of *single-member districts* - one representative for each (local-area) district. 

It's desirable, therefore, that the member representing this district have as broad a support as possible. One way to do this is with score voting (or approval, in the simplest case). Another is to use preferential voting, also known as ranked-choice, instant-runoff or single transferable vote. The latter is commonly used in multi-member districts.

The important thing about preferential voting is that it *guarantees* that the winner of the district is preferred by a clear majority to the runner-up. Vote-splitting can be largely eliminated as a phenomenon, especially under *full* preferential voting.

### Optional Preferential Voting

In this document, however, I'm going to focus on *optional* preferential voting. The voter receives a ballot paper listing *n* candidates; they number their favourite as [1], their second favourite as [2], and so on. As preferences are *optional* they need not complete the entire paper, allowing them to leave off candidates they know nothing about or are equally opposed to.

#### The Count

OPV works on an 'instant-runoff' paradigm. If no candidate has a majority of votes, the candidate with the fewest votes is declared *eliminated*. Then, all votes for that candidate are *distributed* to the next preference listed (if any; those votes with no further preference *exhaust*). This process continues until a candidate has a majority  (of non-exhausted votes) and are duly declared elected.

## Parliamentary level

At the level of the entire parliament, it's desirable that the country/state be represented accurately. The standard proxy for this in countries with party politics is to compare the party's *share of the vote* nationwide with their *share of seats* in the parliament. In countries whose parliament is composed solely of district members, minor parties are often under-represented. A party might get a consistent 10% of the vote nationwide, but that is never enough to actually win a seat and therefore they'll have no parliamentary presence at all.

Proportional representation seeks to rectify this by awarding seats to parties based on the share of the vote.

### Mixed-Member Proportional

MMP allows for both local district representation and a proportional parliament, by awarding *additional* 'at-large' seats to under-represented parties. There are a number of algorithms to do this - usually by giving the voter *two* ballots, one for their local district (usually using first-past-the-post) and one for Parliament as a whole.

## MMP on OPV

Another way is to use only one ballot and take the party (if any) of the first preference for proportional purposes. This isn't necessarily ideal, but it cuts the number of ballot papers required in half. 

So the 'overall makeup' of parliament (proportion of parties) is known from the first stage of the count. District members are elected as normal.

Then, 'top-up' seats must be allocated. The way to do this is to increase the number of seats in parliament until no party has fewer seats (calculated purely proportionally) than they won at a district level.

#### Example - seat quantity determination

Suppose there are 3 parties and 20 districts, with no proportional representation. Team Blue wins 10 districts on 45% of the vote nationwide, Team Red wins 10 districts on 40% of the vote, and Team Green wins no districts on 15%.

If we allocated those 20 seats purely proportionally, Blue would have 9 seats (losing 1) Red would have 8 seats (losing 2), and Green would have 3 seats (gaining 3).

Instead, we expand the size of the parliament such that the most over-represented party has the correct number of seats. This means *nobody ever loses a seat* -  a critical requirement, as before expansion all seats represent districts.

First, let's see what happens with a parliament of (nominally) **21** seats.

Blue is entitled to `45% * 21 = 9.45`, so 9 seats (rounding down) - a loss of one.
Red is entitled to `40% * 21 = 8.4` so 8 seats (rounding down) - also a loss of one.
Green is entitled to `15% * 21 = 3.15` so 3 seats (round down) - a gain of three.

Both Blue and Red have still *lost* seats as they were over-represented. This is *not permissible*, as those seats represented specific districts. We need to try a bigger parliament still.

Now, let's jump ahead and try a parliament nominally of 25 seats -- adding 5.

Blue is entitled to `45% * 25 = 11.25`, so 11 seats (rounding down) - a gain of two.
Red is entitled to `40% * 25 = 10` so 10 seats - no change. Bingo!
Green is entitled to `15% * 25 = 3.75` so 3 seats (if we were to always round down) - a gain of three.

In the end we have a Parliament of 24 - the proportions being 45.83% for Blue, 41.67% for Red and 12.5% for Green.
This (nominal 25) is the smallest Parliament in which the seats are vaguely proportional and nobody loses any. 

If we rounded to the nearest integer instead of always down, Team Green would benefit (here) and the proportions would be 44%, 40% and 16% respectively. In general, rounding-nearest is likely to benefit smaller parties - the one extra seat from rounding up will represent a much higher proportion of their total. Rounding to the nearest integer also means the actual size of the parliament should often be closer to its nominal size.


### Intra-party topup seat allocation

A party that has won some additional seats requires people to fill them. MMP systems with two separate ballots typically use a 'list' system. Each party chooses some list of candidates and runs down the list to fill its additional seats.

This system dispenses with the list and instead ranks all (losing) candidates from a party by their result *after preferences* - their share of the vote at their point of elimination. The best candidates by that measure take up the additional seats. 

This is a double-chance, but no more than in 2-ballot MMP for a candidate near at the top of a party List and contesting a seat they couldn't possibly win.


### Non/multiple-party 'groups'

Independents or allied parties can also form a 'group' - essentially, pooling their votes for the proportional allocation stage. However, registered parties can only be members of one 'group' (at least if rounding-nearest occurs - compare 10.4 seats vs 1.6 and 8.8 - the latter would win 11 total). Ranking is then performed across all candidates in the *group*.

### Formal recognition of Parties in the legislation

It's common that people like the idea of proportional representation but simultaneously don't like the idea of formally recognising parties in the system. This proposal attempts to imbue that spirit by performing proportional representation on 'groups' rather than parties - a party being (a subset of) a group.

