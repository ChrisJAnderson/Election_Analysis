# Election_Analysis
## Overview Of Election Audit
This project is a program to analyze the results of an election across several counties, calculate the winner as well as other statistics like total votes, and the count and percentage of votes in each county. Done at the request of an election commission, this project will help to analyze a massive dataset in the form of votes and quickly output the results of the election for auditing purposes.
## Election Audit Results
The program shows us that:
* There were 369,711 total votes cast in this election. We obtain this count by iterating through the provided csv file and saving the count of rows to a variable called total_votes, as in this code:
```
# Initialize a total vote counter.
total_votes = 0
# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1
```
* We can see that there is a huge imbalance of voters across the three counties included in the election. Denver County had the largest turnout with 306055 votes, or 82.8% of the vote. Jefferson County was next with 38,855 votes, or 10.5%. Arapahoe County's voter turnout was the lowest with 24801 votes, or 6.7%.
We obtain these numbers using a series of for loops, as below.
```
for county in CountyVotes:
        # 6b: Retrieve the county vote count.
        CountyVotes.get(county)
        # 6c: Calculate the percentage of votes for the county.
    TotalVotes= sum(CountyVotes.values())
    for county, votes in CountyVotes.items():
        pct=votes/TotalVotes*100
#lines 97 to 99 uses code taken from Paul Cornelius on StackOverflow
        #<Paul Cornelius> (<Mar 29, 2017>)<Python>(<2.7>)https://stackoverflow.com/questions/43084138/calculate-the-percentage-for-python-dictionary          
```
*Although the distribution of votes in this election was clearly uneven, that may not always be the case. Therefore, the program also identifies the county with the largest amount of votes for us using if/elif/else statements to compare the largest count of votes to each entry in the dictionary. This method is likely to be increasingly inefficient as it scales- out of curiousity I researched and implemented an else statement on the end that uses a lambda function that I believe would work better on larger dictionaries- but in this case there are only three entries in our dictionary of counties. The code to do this is as below.
```
# 6f: Write an if statement to determine the winning county and get its vote count.
    CountyVoteValues= CountyVotes.values()
    LargestTurnout= max(CountyVoteValues)
    if LargestTurnout==CountyVotes["Denver"]:
        WinningCounty=(
            f"\n-------------------------\n"
            f"\nLargest Turnout:\n"
            f"\nDenver county with {LargestTurnout} votes!\n"
            f"\n-------------------------\n")
    elif LargestTurnout==CountyVotes["Jefferson"]:
        WinningCounty=(
            f"\n-------------------------\n"
            f"\nLargest Turnout:\n"
            f"\nJefferson county with {LargestTurnout} votes!\n"
            f"\n-------------------------\n")
    elif LargestTurnout==CountyVotes["Arapahoe"]:
        WinningCounty=(
            f"\n-------------------------\n"
            f"\nLargest Turnout:\n"
            f"\nArapahoe county with {LargestTurnout} votes!\n"
            f"\n-------------------------\n")
    else:
        wc={max(CountyVotes, key= lambda x: CountyVotes[x])}
        #line 117 uses a lambda function taken from pythonguides.com
        #<Bijay Kumar> (<Sep 6, 2021>)<Python>https://pythonguides.com/python-find-max-value-in-a-dictionary/
        WinningCounty= ( 
            f"\n-------------------------\n"
            f"\nLargest Turnout:\n"
            f"{wc} county with {LargestTurnout} votes!\n"
            f"\n-------------------------\n")
    # 7: Print the county with the largest turnout to the terminal.
    print(WinningCounty)
```
*The program displays the proportion of votes for each candidate as well. This is equally lopsided- Raymon Anthony Duane won only 11,606 votes, or 3.1% of the vote, and Charles Casper Stockholm won 85,213 or 23% of the vote. The remaining 272,892 votes went to Diana DeGette, giving her 73.8% of the popular vote.

*The program also displays the winner of the election explicitly, which again can be useful in closer or larger races for quick reference by humans. Diana DeGette was the winner with 272,892 votes- a staggering 73.8%.
## Election Audit Summary 
In summary, this program provides concise and accurate counts of large amounts of votes with provision for multiple counties, reducing the time and inaccuracy that can arise from auditing votes by hand.  
Not only does this program reduce the time spent auditing and eliminate human counting errors, it can also output data to help campaigns make data-driven decisions regarding campaign paths and voter engagement. For example, in this election Denver county is by far the most valuable county to campaign in, with an overwhelming majority of voters. With some modification, it could also be used to track historic voter numbers by accepting and outputting data from past elections during its runtime. With further modification, and additional data regarding the part of the winning candidate for each election, the program could output whether a county is historically inclined to vote for one party over another by processing the winner and the party of the winner for each county through the use of additional for loops restricted to a single key in the dictionary of counties.
