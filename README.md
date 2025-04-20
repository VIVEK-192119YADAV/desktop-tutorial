# Welcome to GitHub Desktop!

# This is your README. READMEs are where you can communicate what your project is and how to use it.

# Write your name on line 6, save it, and then head back to GitHub Desktop.
# SMART CODE CONTRACT OVERVIEW(S0LIDITY).....
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Daanveer {
    address public owner;
    uint public totalDonations;

    struct Donor {
        address donorAddress;
        uint amount;
    }

    Donor[] public donors;

    constructor() {
        owner = msg.sender;
    }

    function donate() public payable {
        require(msg.value > 0, "Donation must be more than 0");
        totalDonations += msg.value;
        donors.push(Donor(msg.sender, msg.value));
    }

    function getDonorCount() public view returns (uint) {
        return donors.length;
    }

    function withdraw() public {
        require(msg.sender == owner, "Only owner can withdraw");
        payable(owner).transfer(address(this).balance);
    }

    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}

