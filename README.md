# Simple ICO
Simple ICO adds a permanent timed sale function to any ERC20 token. This code has a lower average gas cost than the standard crowdfunding model, can be used repeatedly without redeployment, and automatically stops purchasing activity once the deadline is reached. This is a major improvement to other ICO code in that it doesn't require any manual "checkGoal" or "checkDeadline" function to be ran at the end of a sale. The openSale function can have a deadline, or can be timeless. This code functions more like a traditional IPO, where the company can sell shares in multiple rounds at variable pricing.

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
			   timedSale = false;
					}
}
```
In a normal ICO, the failure condition is if the money isn't raised. If the project falls short of it's fundraising goal, it is effectivelly shipwrecked, and the investors get all of their money back. This isn't a function of traditional venture capital. Simple ICO encourages more transparent, variable, and controlled investment opportunities.

Sometimes a token is a share in a company, sometimes it represents a product that hasn't been made yet, but ideally the purchase of a token should return a genuine asset. That asset can be access to a projects contract functions, or access to the ether owned by a DAO. Simple ICO encourages investment in projects with proven value, and lets those projects do as many rounds of fundraising as they need. 

The ICO model is closer to KickStarter than it is to an Initial Public Offering. Simple ICO brings functionality similar to a company selling assets; the company can control all parameters of the sale, can set a time limit, or make the sale a static price for as long as there are shares to sell.

# ECOsystems
The Eternal Coin Offering is my phrase for a DAO which is profitable to all members. That is, members can sell their shares, or withdraw assets directly by vote. In our model, traditional equity investment is made simple and automatic. 

All you have to do is set the owner of the token contract to a standards compliant shareholders organization, at which point only that organization is able to withdraw ether owned by the DAO or the token contract itself. Our simple sale functions allow for DAO's to trade equity in a painless, easy to control manner. Where the standard now is to run a brand new ICO contract for each sale event, simpleICO adds that functionality to the token code itself. This reduces the gas costs of purchasing the token, as well as starting the event. More importantly, the sale can be timed, un timed, and the prices can be changed at the will of the DAO.
