# BCT
//smart contract
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract BankAccount {
    address public owner;
    mapping(address => uint256) public balances;

    event Deposited(address indexed account, uint256 amount);
    event Withdrawn(address indexed account, uint256 amount);
    event Transferred(address indexed from, address indexed to, uint256 amount);

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action");
        _;
    }

    function deposit() public payable {
        require(msg.value > 0, "Deposit amount must be greater than 0");
        balances[msg.sender] += msg.value;
        emit Deposited(msg.sender, msg.value);
    }

    function withdraw(uint256 amount) public {
        require(amount > 0, "Withdrawal amount must be greater than 0");
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
        emit Withdrawn(msg.sender, amount);
    }

    function getBalance() public view returns (uint256) {
        return balances[msg.sender];
    }

    function transfer(address to, uint256 amount) public {
        require(to != address(0), "Invalid recipient address");
        require(to != msg.sender, "Cannot transfer to yourself");
        require(balances[msg.sender] >= amount, "Insufficient balance for transfer");

        balances[msg.sender] -= amount;
        balances[to] += amount;

        emit Transferred(msg.sender, to, amount);
    }
}

//solidity program
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StudentData {
    struct Student {
        uint256 studentId;
        string name;
        uint256 age;
        string course;
    }

    Student[] public students;
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function addStudent(uint256 _studentId, string memory _name, uint256 _age, string memory _course) public {
        require(msg.sender == owner, "Only the owner can add students");
        students.push(Student(_studentId, _name, _age, _course));
    }

    function getStudentCount() public view returns (uint256) {
        return students.length;
    }

    fallback() external {
        revert("Fallback function called. This contract does not accept Ether.");
    }
}

//Fibonacci Numbers...
class Fibonacci {
    public static int nonrecfibo(int n) {
        if (n <= 1) {
            return n;
        }
        int a = 0, b = 1;
        int result = 0;
        for (int i = 2; i <= n; i++) {
            result = a + b;
            a = b;
            b = result;
        }
        return result;
    }

    public static int recfibo(int n) {
        if (n <= 1) {
            return n;
        }
        return recfibo(n - 1) + recfibo(n - 2);
    }

    public static void main(String[] args) {
        int result = nonrecfibo(5);
        int result1 = recfibo(6);
        System.out.println("The fibonacci value is " + result);
        System.out.println("The fibonacci value is " + result1);
    }
}
