# KidsCryptoWallets
This is a project that allows a Dad to credit Kids Ethereum wallet with some Ether which cant be withdrawn until kids turn a certain age. Very challenging yet great results

Solidity API
CryptoKids
Contract
CryptoKids : contracts/CryptoKids.sol

Modifiers:
onlyOwner
modifier onlyOwner()
Functions:
constructor
constructor() public
addKid
function addKid(address payable _walletAddress, string _firstName, string _lastName, uint256 _releaseTime, uint256 _amount, bool _canWithdraw) public
balanceOf
function balanceOf() public view returns (uint256)
deposit
function deposit(address walletAddress) public payable
availableToWithdraw
function availableToWithdraw(address walletAddress) public returns (bool)
withdraw
function withdraw(address walletAddress) public payable
Events:
LogKidFundingReceived
event LogKidFundingReceived(address addr, uint256 amount, uint256 contractBalance)
