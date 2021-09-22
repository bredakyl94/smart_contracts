# smart_contracts

![Ethereum](https://thumbor.forbes.com/thumbor/fit-in/900x510/https://www.forbes.com/advisor/wp-content/uploads/2021/03/ethereum-1.jpeg)

This project involves building smart contracts to automate some company finances to make everyone's lives easier, increase transparency, and to make accounting and auditing practically automatic!


## The profit splitter contracts will do the following:

Pay Associate-level employees quickly and easily.
Distribute profits to different tiers of employees.

## Associate Profit Splitter Contract
This contract has two main functions:

Balance - This function is set to public view returns(uint), and must return the contract's current balance. Since we should always be sending Ether to the beneficiaries, this function should always return 0. If it does not, the deposit function is not handling the remainders properly and should be fixed. This serves as a test function.

Deposit - This function is set to public payable check, making sure only the owner can call the function and transfers an amount of Ether to three different employees.

It is important to note that uint only contains positive whole numbers, and Solidity does not fully support float/decimals, so we must deal with a potential remainder at the end of this function since amount will discard the remainder during division. We can do this by transfering the msg.value amount * 3 back to msg.sender. This will multiply the amount by 3 then subtract it from the msg.value to account for any leftover wei and send it back to HR.



## Tiered Profit Splitter Contract
In this contract, rather than splitting the profits between Associate-level employees, you will calculate rudimentary percentages for different tiers of employees (CEO, CTO, and Bob).

The deposit function has these differences:

Calculation of the number of points/units is done by dividing msg.value by 100. This allows us to multiply the points with a number representing a percentage.
The uint amount variable is used to store the amount to send each employee temporarily. For each employee, the amount is set equal to the number of points multiplied by the percentage
For employee_one, distribute points * 60.
For employee_two, distribute points * 25.
For employee_three, distribute points * 15.

After calculating the amount for the first employee, the amount is added to the total to keep a running total of how much of the msg.value has distributed.

After transfering the amount, the remainder is sent to the employee with the highest percentage by subtracting total from msg.value.


