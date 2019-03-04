pragma solidity >=0.4.2;
contract Pavan {
    address public owner;
    // the owner has to visible
    //use constructor to assign the owner
    constructor()public  {
        owner = msg.sender;
        // owner is assigned as msg.sender
    }
    //Declare the modifier
    //Modifier is used to check the Condition
    //Modifier modifierName
    modifier onlyOwner {
        //when checking the condition we have to use the "require"
        require(msg.sender == owner);
        // evvery time in we have to give "_;"
        _;
    }
    //whether to check the owner is correct or not use boolen type
    function checkOwner() public view returns(bool) {
       if(msg.sender == owner){
           return true;
       } else {
           return false;
       }
    }
    //trannsferOwnership means the onlyOwner will give the access to another user to send the tokens
    function transferOwnership(address newOwnership)onlyOwner public {
        owner = newOwnership;
    }
}
//In ico the pause condition is used whenever the Hacker tried to hack the ico. 
//If the adddress does not matches the ico will be paused and in this 
//we can use resume also fromm where we had stopped
contract Pause is Pavan{
    // we decalare the pause with bool datatype
    bool public pause;
    constructor() public {
        pause = true;
    }
    modifier isPaused {
        require(pause != true);
        _;
    }
    function paused()onlyOwner public {
        pause = true;
    }
    function unpause()onlyOwner public {
        pause = false;
    }
}
//stop type in ico it is used to whenever the onlyOwner address in not matched and it will be dead ico
//and we have option of Play and it is started from starting
contract Stop is Pavan {
    bool public stop;
    constructor() public payable {
        stop = false;
    }
    modifier isStop {
        require(stop != true);
        _;
    }
    function stop1()onlyOwner public {
        stop = true;
    }
    function play()onlyOwner public {
        stop = false;
    }
}
contract pardhu is Pavan,Pause,Stop {
    uint num;
    string name;
    function setdata(uint a, string memory b)onlyOwner isPaused isStop public returns(string memory) {
         num = a;
         name = b;
    }
    function getdata() public view returns(uint,string memory) {
        return (num,name);
    }
}
