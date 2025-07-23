# BITCOIN_EVALUTION
BITCOIN EVALUTION has been done using SQL.
CREATE DATABASE BitcoinEvaluation;

-- Use the database
USE BitcoinEvaluation;

-- Table: User
CREATE TABLE Customer
(
    UserID INT  PRIMARY KEY,
    Username VARCHAR(255) NOT NULL,
    Email VARCHAR(255) UNIQUE NOT NULL,
    PasswordHash VARCHAR(255) NOT NULL,
 );
INSERT INTO Customer (UserID, Username, Email, PasswordHash)
VALUES
(104, 'David', 'david@example.com', 'hashed_password_104'),
(105, 'Eve', 'eve@example.com', 'hashed_password_105')


CREATE TABLE Wallet (
    WalletID INT  PRIMARY KEY,
    UserID INT NOT NULL,
    Balance DECIMAL(18, 8) DEFAULT 0.00000000,
    FOREIGN KEY (UserID) REFERENCES Customer(UserID)
);

-- Table: AddressINSERT INTO Wallet (UserID, Balance)
INSERT INTO Wallet (WalletID, UserID, Balance)
VALUES
(4, 104, 2.50000000),
(5, 105, 1.70000000)

CREATE TABLE Address (
    AddressID INT  PRIMARY KEY,
    WalletID INT NOT NULL,
    AddressHash VARCHAR(255) UNIQUE NOT NULL,
   
    FOREIGN KEY (WalletID) REFERENCES Wallet(WalletID)
);
INSERT INTO Address (AddressID, WalletID, AddressHash)
VALUES
(101, 4, 'addr_hash_001'),
(102, 5, 'addr_hash_002')

-- Table: Transaction
CREATE TABLE Transact (
    TransactionID INT  PRIMARY KEY,
    SenderAddressID INT NOT NULL,
    ReceiverAddressID INT NOT NULL,
    Amount DECIMAL(18, 8) NOT NULL,
    TransactionFee DECIMAL(18, 8) NOT NULL,
   
    FOREIGN KEY (SenderAddressID) REFERENCES Address(AddressID),
    FOREIGN KEY (ReceiverAddressID) REFERENCES Address(AddressID)
);
INSERT INTO Transact (TransactionID, SenderAddressID, ReceiverAddressID, Amount, TransactionFee)
VALUES
(1, 1, 2, 0.01500000, 0.00010000),
(2, 2, 3, 0.25000000, 0.00050000)
-- Table: Block
CREATE TABLE Block (
    BlockID INT PRIMARY KEY,
    BlockHash VARCHAR(255) UNIQUE NOT NULL,
    PreviousBlockHash VARCHAR(255) NULL,
    MerkleRoot VARCHAR(255) NOT NULL,
    Nonce INT NOT NULL,
    Difficulty INT NOT NULL,
    MinerAddressID INT NOT NULL,
    FOREIGN KEY (MinerAddressID) REFERENCES Address(AddressID)
);


-- Ensure Address records exist (1 to 50)
-- Ensure Address records exist (1 to 50)
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 1)
    INSERT INTO dbo.Address (AddressID) VALUES (1);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 2)
    INSERT INTO dbo.Address (AddressID) VALUES (2);
    INSERT INTO dbo.Address (AddressID) VALUES (2);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 3)
    INSERT INTO dbo.Address (AddressID) VALUES (3);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 4)
    INSERT INTO dbo.Address (AddressID) VALUES (4);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 5)
    INSERT INTO dbo.Address (AddressID) VALUES (5);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 6)
    INSERT INTO dbo.Address (AddressID) VALUES (6);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 7)
    INSERT INTO dbo.Address (AddressID) VALUES (7);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 8)
    INSERT INTO dbo.Address (AddressID) VALUES (8);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 9)
    INSERT INTO dbo.Address (AddressID) VALUES (9);
IF NOT EXISTS (SELECT 1 FROM dbo.Address WHERE AddressID = 10)
    INSERT INTO dbo.Address (AddressID) VALUES (10);

-- Add remaining addresses up to 50 using the same pattern...

-- Insert 50 blocks into the Block table

-- Add remaining blocks up to 50 using the same pattern...

-- Insert 50 blocks into the Block table


INSERT INTO Block (BlockID, BlockHash, PreviousBlockHash, MerkleRoot, Nonce, Difficulty, MinerAddressID)
VALUES
(1, 'blockhash_0001', NULL, 'merkle_root_0001', 123456, 5, 1),
(2, 'blockhash_0002', 'blockhash_0001', 'merkle_root_0002', 234567, 6, 2)
-- Table: Blockchain
CREATE TABLE Blockchain (
    BlockchainID INT PRIMARY KEY,
    BlockID INT NOT NULL,
    ChainLength INT NOT NULL,
    
    FOREIGN KEY (BlockID) REFERENCES Block(BlockID)
);
-- Insert 50 records into Blockchain table
INSERT INTO Blockchain (BlockchainID, BlockID, ChainLength) 
VALUES
(1, 1, 5),
(2, 2, 10)

-- Table: MiningNode
CREATE TABLE MiningNode (
    NodeID INT PRIMARY KEY,
    NodeName VARCHAR(255) NOT NULL,
    NodeAddress VARCHAR(255) NOT NULL,
    
);
INSERT INTO MiningNode (NodeID, NodeName, NodeAddress) 
VALUES
(1, 'Node_001', '192.168.1.1'),
(2, 'Node_002', '192.168.1.2')

-- Create the SmartContract table
CREATE TABLE SmartContract (
    ContractID INT PRIMARY KEY,
    ContractHash VARCHAR(255) UNIQUE NOT NULL,
    CreatorAddressID INT NOT NULL,
    ContractCode TEXT NOT NULL,
    FOREIGN KEY (CreatorAddressID) REFERENCES Address(AddressID)
);

-- Insert 50 records into the SmartContract table
INSERT INTO SmartContract (ContractID, ContractHash, CreatorAddressID, ContractCode) 
VALUES
(1, 'contracthash_0001', 1, 'contract_code_0001'),
(2, 'contracthash_0002', 2, 'contract_code_0002')
-- Create the SmartContract table
CREATE TABLE SmartContract (
    ContractID INT PRIMARY KEY,
    ContractHash VARCHAR(255) UNIQUE NOT NULL,
    CreatorAddressID INT NOT NULL,
    ContractCode TEXT NOT NULL,
    FOREIGN KEY (CreatorAddressID) REFERENCES Address(AddressID)
);

-- Insert 50 records into the SmartContract table
INSERT INTO SmartContract (ContractID, ContractHash, CreatorAddressID, ContractCode) 
VALUES
(1, 'contracthash_0001', 1, 'contract_code_0001'),
(2, 'contracthash_0002', 2, 'contract_code_0002')

CREATE TABLE Expense (
    PriceID INT PRIMARY KEY,
    Date DATE NOT NULL,                          
    OpenPrice DECIMAL(18, 8) NOT NULL,            
    HighPrice DECIMAL(18, 8) NOT NULL,            
    LowPrice DECIMAL(18, 8) NOT NULL,             
    ClosePrice DECIMAL(18, 8) NOT NULL,           
    Volume DECIMAL(18, 8) NOT NULL,               
    MarketCap DECIMAL(18, 8) NOT NULL,            
);
	SELECT * 
	FROM INFORMATION_SCHEMA.TABLES
	WHERE TABLE_NAME = 'Expense'
	SELECT TABLE_SCHEMA, TABLE_NAME
	FROM INFORMATION_SCHEMA.TABLES
	WHERE TABLE_NAME = 'Expense';

INSERT INTO Expense (PriceID, Date, OpenPrice, HighPrice, LowPrice, ClosePrice, Volume, MarketCap)
VALUES
(1, '2024-01-01', 42000.12345678, 42500.56781234, 41800.12347812, 42300.45678123, 35000.12345678, 820000000.12345678),
(2, '2024-01-02', 42300.56781234, 42800.45678123, 42100.12347812, 42650.12345678, 36000.56781234, 830000000.45678123)
CREATE TABLE Exchanges (
    ExchangeID INT PRIMARY KEY,
    ExchangeName VARCHAR(255) NOT NULL,           
    TradingPair VARCHAR(255) NOT NULL,           
    OpenPrice DECIMAL(18, 8) NOT NULL,           
    ClosePrice DECIMAL(18, 8) NOT NULL,           
    Volume DECIMAL(18, 8) NOT NULL,               
    HighPrice DECIMAL(18, 8) NOT NULL,           
    LowPrice DECIMAL(18, 8) NOT NULL,            
    Date DATE NOT NULL                           
  );
  INSERT INTO Exchanges (ExchangeID, ExchangeName, TradingPair, OpenPrice, ClosePrice, Volume, HighPrice, LowPrice, Date)
VALUES
    (1, 'Binance', 'BTC/USDT', 65000.50, 65500.75, 1200.456789, 66000.00, 64000.00, '2025-03-01'),
    (2, 'Coinbase', 'ETH/USDT', 3200.75, 3250.80, 850.123456, 3300.00, 3100.50, '2025-03-02')

  CREATE TABLE Whale_Activity (
    WhaleActivityID INT  PRIMARY KEY,
    TransactionHash VARCHAR(255) UNIQUE NOT NULL, 
    SenderAddress VARCHAR(255) NOT NULL,          
    ReceiverAddress VARCHAR(255) NOT NULL,        
    Amount DECIMAL(18, 8) NOT NULL,               
    WhaleThreshold DECIMAL(18, 8) NOT NULL,       
);
-- Create the Whale_Activity table
CREATE TABLE Whale_Activity (
    WhaleActivityID INT PRIMARY KEY,
    TransactionHash VARCHAR(255) UNIQUE NOT NULL, 
    SenderAddress VARCHAR(255) NOT NULL,          
    ReceiverAddress VARCHAR(255) NOT NULL,        
    Amount DECIMAL(18, 8) NOT NULL,               
    WhaleThreshold DECIMAL(18, 8) NOT NULL        
);

-- Insert 50 sample records
INSERT INTO Whale_Activity (WhaleActivityID, TransactionHash, SenderAddress, ReceiverAddress, Amount, WhaleThreshold) VALUES
(1, '0xabc123', '0xSender1', '0xReceiver1', 1500.50, 1000.00),
(2, '0xabc124', '0xSender2', '0xReceiver2', 2000.75, 1000.00)

 CREATE TABLE Mining_Pools (
    PoolID INT PRIMARY KEY,
    PoolName VARCHAR(255) NOT NULL,              
    PoolAddress VARCHAR(255) NOT NULL,             
    HashRate DECIMAL(18, 8) NOT NULL,             
    TotalReward DECIMAL(18, 8) NOT NULL,         
    ActiveMiners INT NOT NULL,                   
);
CREATE TABLE Mining_Pools (
    PoolID INT PRIMARY KEY,
    PoolName VARCHAR(255) NOT NULL,
    PoolAddress VARCHAR(255) NOT NULL,
    HashRate DECIMAL(18, 8) NOT NULL,
    TotalReward DECIMAL(18, 8) NOT NULL,
    ActiveMiners INT NOT NULL
);

INSERT INTO Mining_Pools (PoolID, PoolName, PoolAddress, HashRate, TotalReward, ActiveMiners) VALUES
(1, 'AlphaPool', '192.168.1.1', 1250.45, 325.75, 1200),
(2, 'BetaHash', '192.168.1.2', 980.67, 275.40, 950)
CREATE TABLE Payment_Adoption (
    AdoptionID INT  PRIMARY KEY,
    MerchantName VARCHAR(255) NOT NULL,         
    MerchantType VARCHAR(255) NOT NULL,           
    PaymentAddress VARCHAR(255) NOT NULL,         
    PaymentVolume DECIMAL(18, 8) NOT NULL,        
    Date DATE NOT NULL,                           
);
CREATE TABLE Payment_Adoption (
    AdoptionID INT PRIMARY KEY,
    MerchantName VARCHAR(255) NOT NULL,
    MerchantType VARCHAR(255) NOT NULL,
    PaymentAddress VARCHAR(255) NOT NULL,
    PaymentVolume DECIMAL(18, 8) NOT NULL,
    Date DATE NOT NULL
);

INSERT INTO Payment_Adoption (AdoptionID, MerchantName, MerchantType, PaymentAddress, PaymentVolume, Date) 
VALUES
    (1, 'Merchant_A', 'Retail', '1A2B3C4D5E6F', 1250.50, '2023-01-01'),
    (2, 'Merchant_B', 'Food', '2B3C4D5E6F7G', 890.75, '2023-01-02')



    -- 1. Select all customers
SELECT * FROM Customer;

-- 2. Select all wallets with balance > 3 BTC
SELECT * FROM Wallet WHERE Balance > 3.00000000;

-- 3. Select transactions with amount > 0.5 BTC
SELECT * FROM transact WHERE Amount > 0.50000000;

-- 4. Select blocks mined by address ID 5
SELECT * FROM Block WHERE MinerAddressID = 5;

-- 5. Select smart contracts created by address ID 10
SELECT * FROM SmartContract WHERE CreatorAddressID = 10;

-- 6. Select exchanges with volume > 1000
SELECT * FROM Exchanges WHERE Volume > 1000.00000000;

-- 7. Select whale activities with amount > 5000
SELECT * FROM Whale_Activity WHERE Amount > 5000.00000000;

-- 8. Select mining pools with hash rate > 1000
SELECT * FROM Mining_Pools WHERE HashRate > 1000.00000000;

-- 9. Select payment adoptions in January 2023
SELECT * FROM Payment_Adoption WHERE Date BETWEEN '2023-01-01' AND '2023-01-31';

-- 10. Select expenses in February 2024
SELECT * FROM Expense WHERE Date BETWEEN '2024-02-01' AND '2024-02-29';

-- 11. Select customers with usernames starting with 'A'
SELECT * FROM Customer WHERE Username LIKE 'A%';

-- 12. Select wallets with balance between 1 and 2 BTC
SELECT * FROM Wallet WHERE Balance BETWEEN 1.00000000 AND 2.00000000;

-- 13. Select transactions with fees > 0.0003 BTC
SELECT * FROM Transact WHERE TransactionFee > 0.00030000;

-- 14. Select blocks with difficulty > 20
SELECT * FROM Block WHERE Difficulty > 20;

-- 15. Select blockchain records with chain length > 100
SELECT * FROM Blockchain WHERE ChainLength > 100;

-- 16. Select mining nodes with IPs starting with '192.168.1.1'
SELECT * FROM MiningNode WHERE NodeAddress LIKE '192.168.1.1%';

-- 17. Select smart contracts with IDs between 10 and 20
SELECT * FROM SmartContract WHERE ContractID BETWEEN 10 AND 20;

-- 18. Select exchanges trading BTC/USDT pair
SELECT * FROM Exchanges WHERE TradingPair = 'BTC/USDT';

-- 19. Select whale activities with threshold = 1000
SELECT * FROM Whale_Activity WHERE WhaleThreshold = 1000.00000000;

-- 20. Select mining pools with active miners > 1000
SELECT * FROM Mining_Pools WHERE ActiveMiners > 1000;

-- 21. Select payment adoptions by retail merchants
SELECT * FROM Payment_Adoption WHERE MerchantType = 'Retail';

-- 22. Select expenses where close price > open price
SELECT * FROM Expense WHERE ClosePrice > OpenPrice;

-- 23. Select customers with specific IDs
SELECT * FROM Customer WHERE UserID IN (104, 105, 106);

-- 24. Select wallets ordered by balance descending
SELECT * FROM Wallet ORDER BY Balance DESC;

-- 25. Select top 10 transactions by amount
SELECT TOP 10 * FROM Transact ORDER BY Amount DESC;

-- 26. Select blocks mined in the last 10 positions
SELECT * FROM Block ORDER BY BlockID DESC OFFSET 0 ROWS FETCH NEXT 10 ROWS ONLY;

-- 27. Select distinct merchant types
SELECT DISTINCT MerchantType FROM Payment_Adoption;

-- 28. Select count of customers
SELECT COUNT(*) AS CustomerCount FROM Customer;

-- 29. Select average wallet balance
SELECT AVG(Balance) AS AvgBalance FROM Wallet;

-- 30. Select sum of all transaction amounts
SELECT SUM(Amount) AS TotalTransacted FROM Transact;

-- 31. Join Customer with their Wallet
SELECT c.Username, w.Balance 
FROM Customer c
JOIN Wallet w ON c.UserID = w.UserID;

-- 32. Join Wallet with Address
SELECT w.WalletID, a.AddressHash
FROM Wallet w
JOIN Address a ON w.WalletID = a.WalletID;

-- 33. Join Transaction with Sender and Receiver Addresses
SELECT t.TransactionID, s.AddressHash AS Sender, r.AddressHash AS Receiver, t.Amount
FROM Transact t
JOIN Address s ON t.SenderAddressID = s.AddressID
JOIN Address r ON t.ReceiverAddressID = r.AddressID;

-- 34. Join Block with Miner Address
SELECT b.BlockID, a.AddressHash AS MinerAddress, b.MerkleRoot
FROM Block b
JOIN Address a ON b.MinerAddressID = a.AddressID;

-- 35. Join Blockchain with Block
SELECT bc.BlockchainID, b.BlockHash, bc.ChainLength
FROM Blockchain bc
JOIN Block b ON bc.BlockID = b.BlockID;

-- 36. Join SmartContract with Creator Address
SELECT sc.ContractID, a.AddressHash AS CreatorAddress, sc.ContractHash
FROM SmartContract sc
JOIN Address a ON sc.CreatorAddressID = a.AddressID;

-- 37. Join Customer with Wallet and Address
SELECT c.Username, w.Balance, a.AddressHash
FROM Customer c
JOIN Wallet w ON c.UserID = w.UserID
JOIN Address a ON w.WalletID = a.WalletID;

-- 38. Left join all wallets with their transactions (even if no transactions)
SELECT w.WalletID, t.TransactionID, t.Amount
FROM Wallet w
LEFT JOIN Address a ON w.WalletID = a.WalletID
LEFT JOIN Transact t ON a.AddressID = t.SenderAddressID OR a.AddressID = t.ReceiverAddressID;

-- 39. Join Whale Activity with Sender and Receiver (hypothetical)
SELECT wa.TransactionHash, wa.Amount, wa.WhaleThreshold
FROM Whale_Activity wa;

-- 40. Join Mining Pools with Mining Nodes (if related)
SELECT mp.PoolName, mn.NodeName
FROM Mining_Pools mp
JOIN MiningNode mn ON mp.PoolAddress = mn.NodeAddress;

-- 41. Join Payment Adoption with Merchant Type counts
SELECT MerchantType, COUNT(*) AS MerchantCount
FROM Payment_Adoption
GROUP BY MerchantType;

-- 42. Join Expense data with daily price change calculation
SELECT Date, OpenPrice, ClosePrice, (ClosePrice - OpenPrice) AS PriceChange
FROM Expense;

-- 43. Join Customer with their transaction count
SELECT c.Username, COUNT(t.TransactionID) AS TransactionCount
FROM Customer c
JOIN Wallet w ON c.UserID = w.UserID
JOIN Address a ON w.WalletID = a.WalletID
LEFT JOIN Transact t ON a.AddressID = t.SenderAddressID OR a.AddressID = t.ReceiverAddressID
GROUP BY c.Username;

-- 44. Join Wallet with transaction sums (sent and received)
SELECT w.WalletID, 
       SUM(CASE WHEN t.SenderAddressID = a.AddressID THEN t.Amount ELSE 0 END) AS TotalSent,
       SUM(CASE WHEN t.ReceiverAddressID = a.AddressID THEN t.Amount ELSE 0 END) AS TotalReceived
FROM Wallet w
JOIN Address a ON w.WalletID = a.WalletID
LEFT JOIN Transact t ON a.AddressID = t.SenderAddressID OR a.AddressID = t.ReceiverAddressID
GROUP BY w.WalletID;

-- 45. Join Block with Transaction count per block (hypothetical, would need Transaction-Block relation)
-- This is a placeholder as your schema doesn't directly link transactions to blocks

-- 46. Join SmartContract with usage count (if tracking usage)
SELECT sc.ContractHash, COUNT(*) AS UsageCount
FROM SmartContract sc
-- Would need a join table for contract usage
GROUP BY sc.ContractHash;

-- 47. Join Exchanges with daily volume averages
SELECT ExchangeName, AVG(Volume) AS AvgDailyVolume
FROM Exchanges
GROUP BY ExchangeName;

-- 48. Join Whale Activity with size categories
SELECT TransactionHash, Amount,
       CASE 
           WHEN Amount < 1000 THEN 'Small'
           WHEN Amount BETWEEN 1000 AND 5000 THEN 'Medium'
           ELSE 'Large'
       END AS SizeCategory
FROM Whale_Activity;

-- 49. Join Mining Pools with productivity ratio
SELECT PoolName, TotalReward/ActiveMiners AS RewardPerMiner
FROM Mining_Pools;

-- 50. Join Payment Adoption with monthly totals
SELECT YEAR(Date) AS Year, MONTH(Date) AS Month, SUM(PaymentVolume) AS MonthlyVolume
FROM Payment_Adoption
GROUP BY YEAR(Date), MONTH(Date)
ORDER BY Year, Month;

-- 51. Join Customer with their first transaction date
SELECT c.Username, MIN(t.Date) AS FirstTransactionDate
FROM Customer c
JOIN Wallet w ON c.UserID = w.UserID
JOIN Address a ON w.WalletID = a.WalletID
JOIN Transact t ON a.AddressID = t.SenderAddressID OR a.AddressID = t.ReceiverAddressID
GROUP BY c.Username;

-- 52. Join Wallet with current balance calculation
SELECT w.WalletID, 
       w.Balance AS InitialBalance,
       (SELECT COALESCE(SUM(Amount), 0) FROM Transact t JOIN Address a ON t.ReceiverAddressID = a.AddressID WHERE a.WalletID = w.WalletID) AS TotalReceived,
       (SELECT COALESCE(SUM(Amount), 0) FROM Transact t JOIN Address a ON t.SenderAddressID = a.AddressID WHERE a.WalletID = w.WalletID) AS TotalSent,
       w.Balance + (SELECT COALESCE(SUM(Amount), 0) FROM Transact t JOIN Address a ON t.ReceiverAddressID = a.AddressID WHERE a.WalletID = w.WalletID) -
                  (SELECT COALESCE(SUM(Amount), 0) FROM Transact t JOIN Address a ON t.SenderAddressID = a.AddressID WHERE a.WalletID = w.WalletID) AS CurrentBalance
FROM Wallet w;

-- 53. Join Block with mining difficulty analysis
SELECT BlockID, Difficulty,
       CASE 
           WHEN Difficulty < 10 THEN 'Easy'
           WHEN Difficulty BETWEEN 10 AND 20 THEN 'Medium'
           ELSE 'Hard'
       END AS DifficultyLevel
FROM Block;

-- 54. Join SmartContract with creator wallet balance
SELECT sc.ContractID, sc.ContractHash, w.Balance AS CreatorBalance
FROM SmartContract sc
JOIN Address a ON sc.CreatorAddressID = a.AddressID
JOIN Wallet w ON a.WalletID = w.WalletID;

-- 55. Join Exchanges with price volatility
SELECT ExchangeName, TradingPair, 
       MAX(HighPrice) - MIN(LowPrice) AS PriceRange,
       (MAX(HighPrice) - MIN(LowPrice)) / AVG(ClosePrice) * 100 AS VolatilityPercentage
FROM Exchanges
GROUP BY ExchangeName, TradingPair;

-- 56. Join Whale Activity with time periods (if time was recorded)
-- Placeholder as your Whale_Activity table doesn't have timestamps

-- 57. Join Mining Pools with performance ranking
SELECT PoolName, HashRate, TotalReward,
       RANK() OVER (ORDER BY TotalReward DESC) AS PerformanceRank
FROM Mining_Pools;

-- 58. Join Payment Adoption with merchant category performance
SELECT MerchantType, 
       SUM(PaymentVolume) AS TotalVolume,
       COUNT(*) AS MerchantCount,
       SUM(PaymentVolume) / COUNT(*) AS AvgVolumePerMerchant
FROM Payment_Adoption
GROUP BY MerchantType
ORDER BY TotalVolume DESC;

-- 59. Join Expense with moving average
SELECT Date, ClosePrice,
       AVG(ClosePrice) OVER (ORDER BY Date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS SevenDayMovingAvg
FROM Expense;

-- 60. Join Customer with wallet and transaction summary
SELECT c.Username, w.Balance,
       (SELECT COUNT(*) FROM Transact t JOIN Address a ON t.SenderAddressID = a.AddressID WHERE a.WalletID = w.WalletID) AS SentCount,
       (SELECT COUNT(*) FROM Transact t JOIN Address a ON t.ReceiverAddressID = a.AddressID WHERE a.WalletID = w.WalletID) AS ReceivedCount
FROM Customer c
JOIN Wallet w ON c.UserID = w.UserID;
-- 61. Count transactions per day
SELECT CONVERT(DATE, GETDATE()) AS TransactionDate, COUNT(*) AS TransactionCount
FROM Transact
GROUP BY CONVERT(DATE, GETDATE());

-- 62. Average transaction amount by sender
SELECT a.AddressHash, AVG(t.Amount) AS AvgAmountSent
FROM Transact t
JOIN Address a ON t.SenderAddressID = a.AddressID
GROUP BY a.AddressHash;

-- 63. Total transaction volume per wallet
SELECT w.WalletID, SUM(t.Amount) AS TotalTransactionVolume
FROM Wallet w
JOIN Address a ON w.WalletID = a.WalletID
JOIN Transact t ON a.AddressID = t.SenderAddressID OR a.AddressID = t.ReceiverAddressID
GROUP BY w.WalletID;

-- 64. Most active senders (by transaction count)
SELECT a.AddressHash, COUNT(*) AS TransactionCount
FROM Transact t
JOIN Address a ON t.SenderAddressID = a.AddressID
GROUP BY a.AddressHash
ORDER BY TransactionCount DESC;

-- 65. Most active receivers (by transaction count)
SELECT a.AddressHash, COUNT(*) AS TransactionCount
FROM Transact t
JOIN Address a ON t.ReceiverAddressID = a.AddressID
GROUP BY a.AddressHash
ORDER BY TransactionCount DESC;

-- 66. Highest value transactions
SELECT TOP 10 t.TransactionID, t.Amount, 
       s.AddressHash AS Sender, r.AddressHash AS Receiver
FROM Transact t
JOIN Address s ON t.SenderAddressID = s.AddressID
JOIN Address r ON t.ReceiverAddressID = r.AddressID
ORDER BY t.Amount DESC;

-- 67. Average block difficulty
SELECT AVG(Difficulty) AS AvgDifficulty FROM Block;

-- 68. Mining activity by address
SELECT a.AddressHash, COUNT(*) AS BlocksMined
FROM Block b
JOIN Address a ON b.MinerAddressID = a.AddressID
GROUP BY a.AddressHash
ORDER BY BlocksMined DESC;

-- 69. Smart contract creation count by creator
SELECT a.AddressHash, COUNT(*) AS ContractsCreated
FROM SmartContract sc
JOIN Address a ON sc.CreatorAddressID = a.AddressID
GROUP BY a.AddressHash
ORDER BY ContractsCreated DESC;

-- 70. Exchange volume by trading pair
SELECT TradingPair, SUM(Volume) AS TotalVolume
FROM Exchanges
GROUP BY TradingPair
ORDER BY TotalVolume DESC;

-- 71. Whale activity summary
SELECT COUNT(*) AS TotalWhaleTransactions,
       SUM(Amount) AS TotalWhaleVolume,
       AVG(Amount) AS AvgWhaleTransactionSize
FROM Whale_Activity;

-- 72. Mining pool performance
SELECT PoolName, 
       SUM(TotalReward) AS TotalRewards,
       SUM(ActiveMiners) AS TotalMiners,
       SUM(TotalReward) / SUM(ActiveMiners) AS RewardPerMiner
FROM Mining_Pools
GROUP BY PoolName
ORDER BY TotalRewards DESC;

-- 73. Payment adoption by merchant type
SELECT MerchantType,
       COUNT(*) AS MerchantCount,
       SUM(PaymentVolume) AS TotalVolume,
       AVG(PaymentVolume) AS AvgVolume
FROM Payment_Adoption
GROUP BY MerchantType
ORDER BY TotalVolume DESC;

-- 74. Price volatility analysis
SELECT 
    MIN(ClosePrice) AS MinPrice,
    MAX(ClosePrice) AS MaxPrice,
    AVG(ClosePrice) AS AvgPrice,
    (MAX(ClosePrice) - MIN(ClosePrice)) / AVG(ClosePrice) * 100 AS VolatilityPercentage
FROM Expense;

-- 75. Daily price changes
SELECT Date, 
       ClosePrice,
       LAG(ClosePrice) OVER (ORDER BY Date) AS PreviousClose,
       ClosePrice - LAG(ClosePrice) OVER (ORDER BY Date) AS PriceChange,
       (ClosePrice - LAG(ClosePrice) OVER (ORDER BY Date)) / LAG(ClosePrice) OVER (ORDER BY Date) * 100 AS PercentChange
FROM Expense;

-- 76. Transaction fee analysis
SELECT 
    MIN(TransactionFee) AS MinFee,
    MAX(TransactionFee) AS MaxFee,
    AVG(TransactionFee) AS AvgFee,
    SUM(TransactionFee) AS TotalFees
FROM Transact;

-- 77. Wallet balance distribution
SELECT 
    COUNT(*) AS WalletCount,
    SUM(CASE WHEN Balance < 1 THEN 1 ELSE 0 END) AS Under1BTC,
    SUM(CASE WHEN Balance BETWEEN 1 AND 5 THEN 1 ELSE 0 END) AS Between1And5BTC,
    SUM(CASE WHEN Balance > 5 THEN 1 ELSE 0 END) AS Over5BTC
FROM Wallet;

-- 78. Transaction volume over time (if timestamps were available)
-- Placeholder as your Transact table doesn't have timestamps

-- 79. Most profitable mining pools
SELECT PoolName, TotalReward/ActiveMiners AS RewardPerMiner
FROM Mining_Pools
ORDER BY RewardPerMiner DESC;

-- 80. Merchant payment trends over time
SELECT YEAR(Date) AS Year, MONTH(Date) AS Month,
       SUM(PaymentVolume) AS MonthlyVolume,
       COUNT(DISTINCT MerchantName) AS ActiveMerchants
FROM Payment_Adoption
GROUP BY YEAR(Date), MONTH(Date)
ORDER BY Year, Month;

-- 81. Exchange price differences
SELECT Date, ExchangeName, 
       MAX(ClosePrice) - MIN(ClosePrice) AS PriceDifference
FROM Exchanges
GROUP BY Date, ExchangeName
ORDER BY PriceDifference DESC;

-- 82. Whale transaction patterns
SELECT 
    COUNT(*) AS TransactionCount,
    AVG(Amount) AS AvgAmount,
    MIN(Amount) AS MinAmount,
    MAX(Amount) AS MaxAmount
FROM Whale_Activity;

-- 83. Block mining frequency analysis
SELECT 
    COUNT(*) AS BlockCount,
    AVG(Difficulty) AS AvgDifficulty,
    MIN(Difficulty) AS MinDifficulty,
    MAX(Difficulty) AS MaxDifficulty
FROM Block;

-- 84. Smart contract code length analysis
SELECT 
    AVG(LEN(ContractCode)) AS AvgCodeLength,
    MIN(LEN(ContractCode)) AS MinCodeLength,
    MAX(LEN(ContractCode)) AS MaxCodeLength
FROM SmartContract;

-- 85. Wallet activity correlation with balance
SELECT 
    w.Balance,
    COUNT(t.TransactionID) AS TransactionCount
FROM Wallet w
LEFT JOIN Address a ON w.WalletID = a.WalletID
LEFT JOIN Transact t ON a.AddressID = t.SenderAddressID OR a.AddressID = t.ReceiverAddressID
GROUP BY w.Balance
ORDER BY w.Balance;

-- 86. Transaction amount distribution
SELECT 
    COUNT(*) AS TransactionCount,
    SUM(CASE WHEN Amount < 0.1 THEN 1 ELSE 0 END) AS Under01BTC,
    SUM(CASE WHEN Amount BETWEEN 0.1 AND 1 THEN 1 ELSE 0 END) AS Between01And1BTC,
    SUM(CASE WHEN Amount > 1 THEN 1 ELSE 0 END) AS Over1BTC
FROM Transact;

-- 87. Mining pool hash rate distribution
SELECT 
    COUNT(*) AS PoolCount,
    SUM(CASE WHEN HashRate < 1000 THEN 1 ELSE 0 END) AS Under1000,
    SUM(CASE WHEN HashRate BETWEEN 1000 AND 2000 THEN 1 ELSE 0 END) AS Between1000And2000,
    SUM(CASE WHEN HashRate > 2000 THEN 1 ELSE 0 END) AS Over2000
FROM Mining_Pools;

-- 88. Merchant payment size distribution
SELECT 
    COUNT(*) AS PaymentCount,
    SUM(CASE WHEN PaymentVolume < 500 THEN 1 ELSE 0 END) AS Under500,
    SUM(CASE WHEN PaymentVolume BETWEEN 500 AND 1000 THEN 1 ELSE 0 END) AS Between500And1000,
    SUM(CASE WHEN PaymentVolume > 1000 THEN 1 ELSE 0 END) AS Over1000
FROM Payment_Adoption;

-- 89. Price trend analysis
SELECT 
    YEAR(Date) AS Year,
    AVG(ClosePrice) AS AvgPrice,
    MIN(ClosePrice) AS MinPrice,
    MAX(ClosePrice) AS MaxPrice
FROM Expense
GROUP BY YEAR(Date)
ORDER BY Year;

-- 90. Exchange liquidity analysis
SELECT 
    ExchangeName,
    AVG(Volume) AS AvgDailyVolume,
    MIN(Volume) AS MinDailyVolume,
    MAX(Volume) AS MaxDailyVolume
FROM Exchanges
GROUP BY ExchangeName
ORDER BY AvgDailyVolume DESC;
-- 91. Insert a new customer
INSERT INTO Customer (UserID, Username, Email, PasswordHash)
VALUES (153, 'NewUser', 'newuser@example.com', 'hashed_password_153');

-- 92. Create a new wallet for the new customer
INSERT INTO Wallet (WalletID, UserID, Balance)
VALUES (51, 153, 0.00000000);

-- 93. Add an address to the new wallet
INSERT INTO Address (AddressID, WalletID, AddressHash)
VALUES (148, 51, 'new_address_hash_148');

-- 94. Record a new transaction
INSERT INTO Transact (TransactionID, SenderAddressID, ReceiverAddressID, Amount, TransactionFee)
VALUES (41, 1, 148, 0.10000000, 0.00010000);

-- 95. Update a wallet balance after a transaction
UPDATE Wallet
SET Balance = Balance - 0.10000000
WHERE WalletID = (SELECT WalletID FROM Address WHERE AddressID = 1);

UPDATE Wallet
SET Balance = Balance + 0.10000000
WHERE WalletID = (SELECT WalletID FROM Address WHERE AddressID = 148);

-- 96. Add a new block to the blockchain
INSERT INTO Block (BlockID, BlockHash, PreviousBlockHash, MerkleRoot, Nonce, Difficulty, MinerAddressID)
VALUES (41, 'new_block_hash_41', 'blockhash_0040', 'new_merkle_root_41', 543210, 41, 1);

-- 97. Update the blockchain with the new block
INSERT INTO Blockchain (BlockchainID, BlockID, ChainLength)
VALUES (51, 41, 255);

-- 98. Create a new smart contract
INSERT INTO SmartContract (ContractID, ContractHash, CreatorAddressID, ContractCode)
VALUES (51, 'new_contract_hash_51', 1, 'new_contract_code_51');

-- 99. Record a new exchange trade
INSERT INTO Exchanges (ExchangeID, ExchangeName, TradingPair, OpenPrice, ClosePrice, Volume, HighPrice, LowPrice, Date)
VALUES (33, 'Binance', 'BTC/USDT', 67500.00, 68000.00, 1400.567890, 68500.00, 67000.00, '2025-04-02');

-- 100. Record a whale activity
INSERT INTO Whale_Activity (WhaleActivityID, TransactionHash, SenderAddress, ReceiverAddress, Amount, WhaleThreshold)
VALUES (51, 'new_whale_tx_hash', 'whale_sender', 'whale_receiver', 7500.50, 1000.00);
