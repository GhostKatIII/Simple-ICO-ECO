# Eternal Coin Offering
ECO adds a reusable timed sale function to the ERC20 token. This code has a lower average gas cost than the standard crowdfunding model, can be used repeatedly without redeployment, and automatically stops purchasing activity once the deadline is reached. This is a major improvement to other ICO code in that it doesn't require any manual "checkGoal" or "checkDeadline" function to be ran at the end of a sale. The openSale function can have a deadline, or can be timeless. Most importantly, it can be reused. This code adds intrinsic sale event functionality to the standard itself. 
```C#
    
modifier isOpen() {if (timedSale = false || now <= dLine) _; } // checks deadline if timed sale is true

function buy() isOpen payable public {
        require(!isClosed);
	      uint amount = msg.value / buyPrice;             
        _transfer(this, msg.sender, amount);              
    }

function openSale(uint tMin, bool isTimed) onlyOwner public {
		isClosed = false;
		    if (isTimed == true) {
		    dLine = now + tMin * 1 minutes;
		    timedSale = true;
			}
		
		    if (isTimed == false) {
			   timedSale = false;       //setting the timed sale to false, opens the buy function
					}
}

	function reSet () public onlyOwner {
		if (isClosed == false) {isClosed = true;} // closes the buy function for untimed sale events
}

function eKo(uint256 amount) onlyOwner public {             
    require(this.balance >= amount);                       //easy withdraw function gives immediate access to funds raised
    msg.sender.transfer(amount);
}
```
In a normal ICO, the failure condition is if the money isn't raised. If the project falls short of it's fundraising goal, it is effectivelly shipwrecked, and the investors get all of their money back. This isn't a function of traditional venture capital, where an investment can't be reversed. Simple ICO encourages more transparent, variable, and controlled investment opportunities.

Sometimes a token is a share, sometimes it represents a product that hasn't been made yet, but ideally the purchase of a token should return a genuine asset. That asset can be access to contract functions, or access to ether owned by a DAO. ECO encourages investment in projects with proven value, and lets those projects do as many rounds of fundraising as they need. 

This function is similar to a company selling assets; the company can control all parameters of the sale, can set a time limit, or make the sale a static price for as long as there are shares to sell.

# ECOsystems
The Eternal Coin Offering System is my phrase for a DAO which is profitable to all members. That is, members can sell their shares, or withdraw assets directly by vote. In our model, traditional equity investment is made simple and automatic. 

All you have to do is set the owner of the token contract to a standards compliant shareholders organization, at which point only that organization is able to withdraw ether owned by the token contract. Our simple sale functions allow for DAO's to trade equity in a painless, automated, and easy to control manner. 
