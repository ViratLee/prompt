## Test Scenarios

### scenarion 1. Token Swap Functionality
Give open swap page
Then fill in valid token amounts
When I click the swap button
Then the swap should be executed successfully and balances updated

### scenarion 2. Cancel swap before confirmation 
Given I have filled in valid token amounts
When I click the cancel button before confirming the swap
Then the swap should be cancelled and no changes to balances should occur

### scenarion 2. Swap with insufficient balance - error displayed
Given I have filled in token amounts that exceed my balance 
When I click the swap button 
Then an error message should be displayed indicating insufficient balance and the swap should not proceed

