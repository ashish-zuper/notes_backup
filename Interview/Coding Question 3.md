Problem Statement: Split the Bill — Payment Settlement Among Friends  
Context  
A group of friends go on an outing together. During the trip, each person pays for different expenses (food, fuel, tickets, etc.).  
At the end of the trip, they want to settle the total cost so that everyone pays an equal share.  
Your task is to compute the minimal set of transactions needed so that all debts are settled.Input  

- An integer `n` — the number of friends.
- A list of `n` entries, where each entry represents how much each friend paid during the trip.
    - For simplicity, assume friends are labeled from `0` to `n-1`.  

Example:  

n = 4
expenses = [1200, 1500, 800, 1500]

Output  
Return or print the list of transactions required for everyone to have spent equally.  
Each transaction should be in the form:

Person X pays Person Y: <amount>

Output :  

Person 0 pays Person 1: 50
Person 2 pays Person 1: 200
Person 2 pays Person 3: 250

Constraints  

- `2 ≤ n ≤ 1000`
- Each expense is a non-negative integer ≤ 10^6
- Total sum of all payments ≤ 10^9
- The output can have multiple valid solutions (any minimal or valid settlement is accepted).
