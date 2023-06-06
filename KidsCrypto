// SPDX-License-Identifier: MIT
pragma solidity >= 0.6.0 <0.9.0;

contract CryptoKids {
    // Define owner DAD
    address owner;

    event LogKidFundingReceived(address addr, uint amount, uint contractBalance);

    constructor() public{
        owner = msg.sender;
    }

    //define kid
    struct Kid {
        address payable walletAddress;
        string firstName;
        string lastName;
        uint releaseTime;
        uint amount;
        bool canWithdraw;
    }

    Kid[] public kids;

    modifier onlyOwner {
       require(msg.sender == owner, "Only the owner can add kids");
       _;
   }

    //add kid to contract
    function addKid(address payable  _walletAddress, string memory _firstName, string memory _lastName, uint _releaseTime, uint _amount, bool _canWithdraw) public onlyOwner {
        kids.push(Kid(_walletAddress, _firstName, _lastName, _releaseTime, _amount, _canWithdraw));
    }

    function balanceOf() public view returns(uint){
        return address(this).balance;
    }
    
    //deposit funds to contract, 
    function deposit(address walletAddress) payable  public onlyOwner{
        addToKidsBalance(walletAddress);
    }

    // deposit funds specifically to a kid's account
    function addToKidsBalance(address walletAddress) private onlyOwner{
        for(uint i=0; i < kids.length; i++){
            if(kids[i].walletAddress == walletAddress){
                kids[i].amount += msg.value;
                emit LogKidFundingReceived(walletAddress, msg.value, balanceOf());
            }
        }
    }

    function getIndex(address walletAddress) view private returns(uint){
        for(uint i = 0; i < kids.length; i++){
            if(kids[i].walletAddress == walletAddress){
                return  i;
            }
        }
        return 999;
    }

    //kid checks if able to withdraw
    function availableToWithdraw(address walletAddress) public returns (bool){
        uint i = getIndex(walletAddress);
        require(block.timestamp > kids[i].releaseTime, "You cannot withdraw yet");
        if(block.timestamp > kids[i].releaseTime){
            kids[i].canWithdraw = true;
            return true;
        }else{
            return false;
        }
    }

    //withdraw money
    function withdraw(address  walletAddress) payable public {
        uint i = getIndex(walletAddress);
        require(msg.sender == kids[i].walletAddress, "You must be the kid to withdraw");
        require(kids[i].canWithdraw == true, "You are not able to withdraw at this time");
        kids[i].walletAddress.transfer(kids[i].amount);
    }
}
