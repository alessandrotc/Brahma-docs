---

We like how protocols like visor finance and popsicle finance have built with initial version of the automated vaults for managing lp positions on uniswap. As they are first movers into this they faced a few challenges in their initial implementation. Here we go over a few of them and provide details on how Aastra prevents them.‌

### **Visor Hack**

Someone was able to get access to `emergencyWithdraw` function and withdrew the user funds deposited in `HyperVisor` vault. The Visor has refunded users post hack. This hack could have been prevented if the governance was multi-sig decreasing the chances for this hack. More details about the hack can be found [here](https://visorfinance.medium.com/visor-beta-incident-report-1b2521b9266).​‌

### **Popsicle Finance Hack**

Popsicle finance had a functionality in their vaults where user's can withdraw the fees earned from their underlying uniswap v3 positions. The exploit happened due to reward debt not being transferred when lp tokens are transferred. So the hacker was able to earn large share of fees using same lp tokens by transferring the lp tokens to multiple wallets. This introduced the problem of double spending. More details about the hack can be found [here](https://popsiclefinance.medium.com/popsicle-finance-post-mortem-after-fragola-hack-f45b302362e0).‌

### **Our Approach**

- Starting from the deployment of first vaults, we are using a gnosis multi-sig shared across ...... for the governance account of protocol. This reduce any individual malicious attacker from accessing the governance account.

- The current architecture of Aastra vaults doesn't give users direct access to the fees earned from their lp position. Instead user's can access funds that are invested in lp position or lying ideal in vault. This prevents the need to maintain state of fees so when lp tokens are transferred their is no change in state. And if there is a `withDraw` call made shares are burned mitigating the issue of double spend to happen in first place.
