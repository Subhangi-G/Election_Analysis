# Election_Analysis

## Project Overview
An election audit of a recent local congressional election has been completed for the Colorado Board of Elections. The purpose of the audit was to calculate the following.

1. The total number of votes cast.
2. A complete list of the counties in the precinct.
3. The voter turnout for each county.
4. The percentage of votes from each county out of the total count.
5. The county with the highest turnout.
6. A complete list of candidates who recieves votes.
7. Total number of votes that each candidate received.
8. The percentage of votes each candidate won.
9. Winner of the election based on the popular vote.

## Resources
- Data Source : election_results.csv
- Software : Python 3.7.6, Visual Studio Code 1.56.0

## Election-Audit Results

### Short overview of method
First the analysis was performed to generate the results for each candidate. Candidate names were stored in an array list, "candidate_options".
The votes that each candidate received were stored in a dictionary, "candidate_votes", where each candidates names corresponded to the votes he/she received. The candidate receiving the maximum number of votes was declared to be the winner. 
Identical analysis was performed to generate the results for each county, and to declare the county with the maximum voter turnout.

For reference, below is a part of the script that analyses the data on the candidates:
```
# For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1
```
The analysis to find the winning candidate, based on the popular vote, was done in the following lines of code:
```
 for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        # Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
        txt_file.write(candidate_results)

        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage
```

The following was the output in the terminal.
```
Election Results
-------------------------
Total Votes: 369,711     
-------------------------

County Votes:
Jefferson county: 10.5% (38,855)

Denver county: 82.8% (306,055)

Arapahoe county: 6.7% (24,801)


-------------------------
Largest county turnout: Denver
-------------------------

Charles Casper Stockham: 23.0% (85,213)

Diana DeGette: 73.8% (272,892)

Raymon Anthony Doane: 3.1% (11,606)

-------------------------
Winner: Diana DeGette
Winning Vote Count: 272,892
Winning Percentage: 73.8%
-------------------------
```

The analysis of the election show the following :
- There were 369,711 votes cast in this election.

### County Results
- Counties in the precinct:
    - Jefferson
    - Denver
    - Arapahoe
    
- Voter turnout in each county and the percentage out of the total count.
    - Jefferson county had a turnout of of 38,855 votes comprising 10.5 % of the vote.
    - Denver county had a turnout of of 306,055 votes comprising 82.8 % of the vote.
    - Arapahoe county had a turnout of of 24,801 votes comprising 6.7 % of the vote.
    
The largest turnout was in Denver county with a turnout of 306,055 votes (82.8 %).

### Candidate Results
- The candidates were:
    - Charles Casper Stockham
    - Diana DeGette
    - Raymon Anthony Doane
    -
- The Candidate results were :
    - Charles Casper Stockham received 23.0 % of the vote and 85,213 number of votes.
    - Diana DeGette received 73.8 % of the vote and 272,892 number of votes.
    - Raymon Anthony Doane received 3.1 % of the vote and 11,606 number of votes.
    - 
- The winner of the election based on popular vote was:
    - Diana DeGette who recieved 73.8 % of the vote and 272,892 number of votes.

## Summary
### Business Proposal for timely analysis and presentation of voting results.

In any election the aggregation of voting data and an accurate analysis to present the results in a timely manner is critical.
This script automates the analysis of the raw data to quickly compile the results by candidates and precincts. It can be applied to any popular voting data with any number of candidates and / or precincts

Furthermore, the script can be modified to detect voter fraud committed by multiple votes casted by a single person / ballot ID. This can be done by checking if repetitions of Ballot ID are present.

Lastly - this scipt can also be modified to compbine external data sources, such as voter demographics, associated with each ballot ID to spot voting trends and preferences. An example would be to investigate if any correlation exists between religious beliefs of the voters and their preference to any particular candidate.  


