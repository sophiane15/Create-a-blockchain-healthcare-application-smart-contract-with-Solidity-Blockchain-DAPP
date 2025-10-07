# 🏥 Blockchain Healthcare Records – Smart Contract

  
  
  

A secure medical-records management system built on the Ethereum blockchain, enabling authorized healthcare providers to add and review patient records in a decentralized, transparent manner.

## 📋 Table of Contents

- [Overview](#overview)  
- [Features](#features)  
- [Smart Contract Architecture](#smart-contract-architecture)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Security](#security)  

## 🎯 Overview

This project implements a Solidity smart contract for decentralized management of medical records. It ensures the security, confidentiality, and integrity of health data via blockchain technology, while providing controlled access to authorized healthcare providers.

### 🌟 Blockchain Solution Benefits

- **Immutability**: Records cannot be modified once added  
- **Traceability**: Complete audit trail of all access and changes  
- **Decentralization**: No single point of failure  
- **Transparency**: Publicly verifiable logs  
- **Security**: Permission-based access control  

## ⚡ Features

### 🔐 Access Management

- **Single Owner**: Only the deployer can authorize new providers  
- **Authorized Providers**: Only approved professionals can add or retrieve records  
- **Granular Control**: Multi-level permissions system  

### 📊 Records Management

- **Record Addition**: Secure registration of new medical entries  
- **Consultation**: Access to full patient history  
- **Timestamping**: Automatic timestamp for each entry  
- **Standardized Structure**: Uniform format for all records  

### 🗄️ Data Structure

Each medical record contains:  
- **Record ID**: Unique, auto-incremented identifier  
- **Patient Name**: Patient’s full name  
- **Diagnosis**: Medical diagnosis  
- **Treatment**: Prescribed treatment plan  
- **Timestamp**: Date and time of creation  

## 🏗️ Smart Contract Architecture

### Data Structures

```solidity
struct Record {
    uint256 recordID;      // Unique record identifier
    string patientName;    // Patient’s name
    string diagnosis;      // Medical diagnosis
    string treatment;      // Treatment plan
    uint256 timestamp;     // Creation timestamp
}
```

### Mappings

- `mapping(uint256 => Record[])`  
  Associates each patient ID with their records  
- `mapping(address => bool)`  
  Manages authorized provider addresses  

### Security Modifiers

- `onlyOwner`  
  Restricts certain functions to the contract owner  
- `onlyAuthorizedProvider`  
  Restricts access to authorized providers only  

## 🚀 Installation

### Prerequisites

- Node.js (v16 or higher)  
- npm or yarn  
- Remix IDE, Truffle, or Hardhat  
- MetaMask or another Ethereum wallet  

### Steps

1. **Clone the repository**  
   ```bash
   git clone https://github.com/your-username/Create-a-blockchain-healthcare-application-smart-contract.git
   cd Create-a-blockchain-healthcare-application-smart-contract
   ```
2. **Install dependencies**  
   ```bash
   npm install
   ```
3. **Configure your environment**  
   ```bash
   # Create a .env file with your private keys
   PRIVATE_KEY=your_private_key
   INFURA_PROJECT_ID=your_infura_project_id
   ```
4. **Compile the contract**  
   ```bash
   # With Hardhat
   npx hardhat compile

   # Or with Remix IDE (copy-paste the code)
   ```
5. **Deploy to a test network**  
   ```bash
   # Deploy to Goerli testnet
   npx hardhat run scripts/deploy.js --network goerli
   ```

## 📖 Usage

### Initial Deployment

```solidity
// The deployer becomes the contract owner
constructor() {
    owner = msg.sender;
}
```

### Authorize a Provider

```solidity
// Only the owner can call this function
function authorizeProvider(address provider) public onlyOwner {
    authorizedProviders[provider] = true;
}
```

### Add a Medical Record

```solidity
// Only authorized providers can add records
function addRecord(
    uint256 patientID, 
    string memory patientName, 
    string memory diagnosis, 
    string memory treatment
) public onlyAuthorizedProvider {
    // Implementation...
}
```

### Retrieve Patient Records

```solidity
// Returns all records for a patient
function getPatientRecords(uint256 patientID) 
    public view onlyAuthorizedProvider 
    returns (Record[] memory) {
    return patientRecords[patientID];
}
```

### JavaScript Interaction Example

```javascript
// Connect to the contract
const contract = new web3.eth.Contract(ABI, contractAddress);

// Authorize a new provider (owner only)
await contract.methods.authorizeProvider("0x123...").send({ from: ownerAddress });

// Add a new medical record
await contract.methods.addRecord(
    1001,
    "Jean Dupont",
    "Hypertension",
    "Lisinopril 10mg daily"
).send({ from: authorizedProviderAddress });

// Retrieve patient records
const records = await contract.methods.getPatientRecords(1001).call();
```

## 🔒 Security

### Implemented Measures

1. **Strict Access Control**  
   - Only the owner can authorize providers  
   - Only authorized providers can manipulate data  

2. **Permission Validation**  
   - Rights verified before each operation  
   - Explicit error messages for unauthorized access  

3. **Data Immutability**  
   - Records cannot be modified once created  
   - Full, auditable history of all additions  

### Best Practices

- **Never share** your private keys  
- **Always test** on a test network before production  
- **Verify provider addresses** before authorizing  
- **Monitor contract events** for suspicious activity

Sources
