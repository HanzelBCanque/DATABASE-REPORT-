You sent
/* Group Project 4: The E-Commerce Company (Retail Database)
   Company: ShopFast Online
   DBA Implementation Script - Final Optimized Version
*/

-- =============================================
-- 1. SETUP DATABASE AND SCHEMAS
-- =============================================

CREATE DATABASE ECommerceDB;
GO
USE ECommerceDB;
GO

CREATE SCHEMA Products;
GO
CREATE SCHEMA Customers;
GO
CREATE SCHEMA Orders;
GO
CREATE SCHEMA Inventory;
GO
CREATE SCHEMA Marketing;
GO

-- =============================================
-- 2. CREATE TABLES
-- =============================================
CREATE TABLE Products.Catalog (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Description TEXT,
    Price DECIMAL(10,2),
    Category VARCHAR(50)
);

CREATE TABLE Products.Suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR(100),
    ContactInfo VARCHAR(255)
);

CREATE TABLE Customers.Info (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100),
    SignupDate DATE
);

CREATE TABLE Customers.Addresses (
    AddressID INT PRIMARY KEY,
    CustomerID INT,
    AddressLine VARCHAR(255),
    IsDefault BIT
);

CREATE TABLE Orders.Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATETIME,
    Status VARCHAR(50)
);

CREATE TABLE Orders.OrderDetails (
    OrderDetailID INT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT,
    UnitPrice DECIMAL(10,2)
);

CREATE TABLE Inventory.Stock (
    ProductID INT,
    WarehouseID INT,
    QuantityOnHand INT,
    ReorderLevel INT
);

CREATE TABLE Inventory.Warehouses (
    WarehouseID INT PRIMARY KEY,
    Location VARCHAR(100),
    Manager VARCHAR(100)
);

CREATE TABLE Marketing.Campaigns (
    CampaignID INT PRIMARY KEY,
    CampaignName VARCHAR(100),
    DiscountPercent DECIMAL(5,2),
    TargetAudience VARCHAR(255)
);
GO

-- =============================================
-- 3. INSERT 50 RECORDS PER TABLE
-- =============================================
INSERT INTO Inventory.Warehouses (WarehouseID, Location, Manager) VALUES
(1, 'Cebu City - North Reclamation Area', 'Wally Warehouseman'),
(2, 'Mandaue City - AS Fortuna Hub', 'Mandy Manager'),
(3, 'Lapu-Lapu City - MEZ 1', 'Larry Logistics'),
(4, 'Talisay City - South Road Properties', 'Terry Tabunok'),
(5, 'Danao City - Northern Cebu Hub', 'Danny Distributor'),
(6, 'Carcar City - Southern Cebu Hub', 'Carl Central'),
(7, 'Toledo City - West Coast Depot', 'Teresa Toledo'),
(8, 'Balamban - Shipbuilding Zone', 'Bob Balamban'),
(9, 'Consolacion - Food & Tech Hub', 'Connie Central'),
(10, 'Liloan - Coastal Storage', 'Lily Liloan'),
(11, 'Manila - Tondo Port Terminal', 'Manny Metro'),
(12, 'Quezon City - North EDSA Hub', 'Quincy QC'),
(13, 'Makati - Central Business Dist', 'Mike Makati'),
(14, 'Pasig - Ortigas Logistics', 'Pat Pasig'),
(15, 'Taguig - BGC Prime Depot', 'Tina Taguig'),
(16, 'Davao City - Sasa Wharf', 'Dave Davao'),
(17, 'Cagayan de Oro - Misamis Hub', 'Cathy CDO'),
(18, 'Iloilo City - Mandurriao Depot', 'Ian Iloilo'),
(19, 'Bacolod City - Sugarland Hub', 'Ben Bacolod'),
(20, 'Zamboanga - Peninsula Storage', 'Zack Zambo'),
(21, 'Angeles City - Clark Freeport', 'Angie Angeles'),
(22, 'Subic Bay - Olongapo Terminal', 'Sam Subic'),
(23, 'Bagui City - Cordillera Hub', 'Bernie Benguet'),
(24, 'Naga City - Bicol Express Hub', 'Nick Naga'),
(25, 'Legazpi City - Albay Depot', 'Leo Legazpi'),
(26, 'Tacloban City - Leyte Central', 'Toby Tacloban'),
(27, 'Ormoc City - Western Leyte', 'Oscar Ormoc'),
(28, 'Dumaguete - Negros Oriental', 'Don Duma'),
(29, 'Tagbilaran - Bohol Gateway', 'Tina Tagb'),
(30, 'General Santos - Tuna Port', 'Gen Gensan'),
(31, 'Butuan City - Agusan Hub', 'Bert Butuan'),
(32, 'Puerto Princesa - Palawan', 'Paul Palawan'),
(33, 'Batangas City - Calabarzon', 'Bart Batangas'),
(34, 'Cavite - Dasmariñas Depot', 'Cid Cavite'),
(35, 'Laguna - Santa Rosa Tech', 'Lana Laguna'),
(36, 'Antipolo - Rizal Heights', 'Andy Antipolo'),
(37, 'Malolos - Bulacan Central', 'Molly Malolos'),
(38, 'San Fernando - Pampanga Hub', 'Fernan Pampa'),
(39, 'Tarlac City - Central Luzon', 'Tom Tarlac'),
(40, 'Dagupan City - Pangasinan', 'Dan Dagupan'),
(41, 'Vigan City - Ilocos Sur', 'Vic Vigan'),
(42, 'Laoag City - Ilocos Norte', 'Lulu Laoag'),
(43, 'Tuguegarao - Cagayan Valley', 'Tug Tugue'),
(44, 'Santiago City - Isabela Hub', 'Santi Isabela'),
(45, 'Koronadal - South Cotabato', 'Kory Koron'),
(46, 'Cotabato City - BARMM Center', 'Cody Cotabato'),
(47, 'Pagadian City - Zambo Sur', 'Page Pagadian'),
(48, 'Surigao City - Mining Hub', 'Suri Surigao'),
(49, 'Malaybalay - Bukidnon Hub', 'Mal Malay'),
(50, 'Bogo City - Northern Tip Cebu', 'Bogi Bogo');

INSERT INTO Marketing.Campaigns (CampaignID, CampaignName, DiscountPercent, TargetAudience) VALUES
(1, 'Sinulog Grand Sale', 20.00, 'Cebu Residents'),
(2, 'Summer Splash 2026', 15.00, 'Students'),
(3, 'New Year Tech Blast', 10.00, 'Early Birds'),
(4, 'Valentines Gadget Love', 25.00, 'Couples'),
(5, 'Graduation Gift Guide', 12.00, 'Parents'),
(6, 'Back to School Promo', 15.00, 'University Students'),
(7, 'Labor Day Weekend', 10.00, 'Working Professionals'),
(8, 'Mid-Year Clearance', 50.00, 'All Customers'),
(9, 'Laptop Fiesta', 18.00, 'IT Students'),
(10, 'Audio Bliss Week', 10.00, 'Music Lovers'),
(11, 'Gaming Marathon Deal', 15.00, 'PC Gamers'),
(12, 'Smart Home Upgrade', 20.00, 'Homeowners'),
(13, 'Mobile Mania', 10.00, 'Smartphone Users'),
(14, 'Wearable Health Week', 12.00, 'Fitness Enthusiasts'),
(15, 'Peripheral Bundle', 5.00, 'Office Workers'),
(16, 'Network Speed Boost', 10.00, 'Remote Workers'),
(17, 'Flash Sale Friday', 30.00, 'App Users'),
(18, 'Early Bird Christmas', 15.00, 'Planners'),
(19, '11.11 Mega Day', 40.00, 'All Customers'),
(20, '12.12 Grand Finale', 45.00, 'All Customers'),
(21, 'Storage Savings', 10.00, 'Photographers'),
(22, 'Video Creator Pro', 15.00, 'YouTubers'),
(23, 'Budget Builder Sale', 8.00, 'PC Builders'),
(24, 'Premium Series Expo', 5.00, 'VIP Members'),
(25, 'Renewal Rewards', 10.00, 'Inactive Users'),
(26, 'Referral Bonus Day', 20.00, 'Existing Customers'),
(27, 'Rainy Day Discounts', 12.00, 'Local Residents'),
(28, 'Halloween Tech Treat', 13.00, 'Gamers'),
(29, 'Cyber Monday Deals', 35.00, 'Online Shoppers'),
(30, 'Black Friday Doorbus', 50.00, 'All Customers'),
(31, 'Birthday Month Special', 20.00, 'Birthday Celebrants'),
(32, 'Loyalty Points Boost', 0.00, 'Gold Members'),
(33, 'Eco-Friendly Tech', 10.00, 'Green Consumers'),
(34, 'Warehouse Clearance', 60.00, 'Bargain Hunters'),
(35, 'Monitor Madness', 15.00, 'Designers'),
(36, 'Keyboard Click-Off', 10.00, 'Typists'),
(37, 'Smart Watch Sunday', 18.00, 'Athletes'),
(38, 'Student Essentials', 20.00, 'University of Cebu'),
(39, 'Mandaue City Charter', 15.00, 'Mandaue Residents'),
(40, 'Talisay Lechon Festival', 10.00, 'Local Patrons'),
(41, 'Business Tech Solutions', 7.00, 'SME Owners'),
(42, 'Content Creator Pack', 12.00, 'Vloggers'),
(43, 'Power Up Week', 10.00, 'Heavy Users'),
(44, 'Accessory Add-on', 5.00, 'Previous Buyers'),
(45, 'Midnight Madness', 25.00, 'Night Owls'),
(46, 'Weekend Warrior Sale', 15.00, 'Weekend Shoppers'),
(47, 'App Exclusive Deal', 22.00, 'Mobile App Users'),
(48, 'Influencer Pick Week', 10.00, 'Social Media Fans'),
(49, 'Holiday Hangover', 12.00, 'Post-Holiday Shoppers'),
(50, 'Tech Anniversary Sale', 30.00, 'Long-time Members');

INSERT INTO Inventory.Stock (ProductID, WarehouseID, QuantityOnHand, ReorderLevel) VALUES
(1, 1, 45, 10),
(2, 1, 120, 20),
(3, 2, 15, 5),  
(4, 2, 200, 30), 
(5, 1, 85, 15),
(6, 1, 30, 10), 
(7, 2, 55, 15),  
(8, 1, 300, 50),
(9, 2, 150, 40), 
(10, 1, 40, 10),
(11, 2, 65, 15),
(12, 1, 12, 5),  
(13, 2, 8, 3),  
(14, 1, 110, 25), 
(15, 2, 90, 20),
(16, 1, 44, 10), 
(17, 2, 500, 100),
(18, 1, 25, 5),  
(19, 2, 35, 10),  
(20, 1, 210, 50),
(21, 2, 18, 5),  
(22, 1, 22, 10), 
(23, 2, 5, 2),   
(24, 1, 80, 20),  
(25, 2, 1000, 200),
(26, 1, 14, 5),  
(27, 2, 19, 5),  
(28, 1, 7, 3),   
(29, 2, 3, 2),   
(30, 1, 120, 30),
(31, 2, 55, 15), 
(32, 1, 88, 20), 
(33, 2, 42, 10),
(34, 1, 31, 10), 
(35, 2, 26, 10),
(36, 1, 17, 5),  
(37, 2, 29, 10), 
(38, 1, 400, 80),
(39, 2, 15, 5),   
(40, 1, 11, 5),
(41, 2, 150, 30),
(42, 1, 60, 15), 
(43, 2, 9, 3),   
(44, 1, 130, 25),
(45, 2, 14, 5),
(46, 1, 33, 10), 
(47, 2, 500, 100),
(48, 1, 200, 50), 
(49, 2, 75, 20), 
(50, 1, 300, 50);

INSERT INTO Orders.OrderDetails (OrderDetailID, OrderID, ProductID, Quantity, UnitPrice) VALUES
(1, 2001, 1, 1, 15000.00), (2, 2001, 8, 2, 1500.00),
(3, 2002, 3, 1, 45000.00), (4, 2003, 2, 1, 2500.00),
(5, 2004, 5, 1, 3500.00),  (6, 2004, 4, 1, 1200.00),
(7, 2005, 10, 1, 5500.00), (8, 2006, 6, 1, 12000.00),
(9, 2007, 7, 1, 2200.00),  (10, 2008, 9, 3, 1800.00),
(11, 2009, 11, 1, 2800.00), (12, 2010, 12, 1, 32000.00),
(13, 2011, 29, 1, 22000.00), (14, 2012, 15, 2, 1100.00),
(15, 2013, 18, 1, 8500.00), (16, 2014, 20, 5, 600.00),
(17, 2015, 24, 1, 1300.00), (18, 2016, 25, 10, 300.00),
(19, 2017, 31, 2, 3200.00), (20, 2018, 32, 1, 5200.00),
(21, 2019, 35, 1, 5500.00), (22, 2020, 38, 2, 500.00),
(23, 2021, 41, 4, 750.00),  (24, 2022, 45, 1, 5800.00),
(25, 2023, 49, 1, 1500.00), (26, 2024, 2, 1, 2500.00),
(27, 2025, 4, 1, 1200.00),  (28, 2026, 8, 1, 1500.00),
(29, 2027, 14, 2, 900.00),  (30, 2028, 17, 1, 850.00),
(31, 2029, 22, 1, 9500.00), (32, 2030, 26, 3, 4500.00),
(33, 2031, 30, 1, 2500.00), (34, 2032, 34, 1, 4000.00),
(35, 2033, 36, 1, 3800.00), (36, 2034, 39, 1, 2900.00),
(37, 2035, 42, 2, 2400.00), (38, 2036, 44, 1, 2200.00),
(39, 2037, 47, 4, 450.00),  (40, 2038, 50, 2, 400.00),
(41, 2039, 1, 1, 15000.00), (42, 2040, 5, 1, 3500.00),
(43, 2041, 10, 1, 5500.00), (44, 2042, 13, 1, 25000.00),
(45, 2043, 19, 1, 4200.00), (46, 2044, 23, 1, 18000.00),
(47, 2045, 28, 1, 35000.00), (48, 2046, 33, 1, 7800.00),
(49, 2047, 37, 1, 4500.00), (50, 2048, 40, 1, 11000.00);

INSERT INTO Orders.Orders (OrderID, CustomerID, OrderDate, Status) VALUES
(2001, 1, '2026-03-01', 'Shipped'),
(2002, 2, '2026-03-02', 'Shipped'),
(2003, 3, '2026-03-02', 'Pending'),
(2004, 4, '2026-03-03', 'Shipped'),
(2005, 5, '2026-03-04', 'Processing'),
(2006, 6, '2026-03-05', 'Shipped'),
(2007, 7, '2026-03-05', 'Cancelled'),
(2008, 8, '2026-03-06', 'Shipped'),
(2009, 9, '2026-03-07', 'Shipped'),
(2010, 10, '2026-03-08', 'Processing'),
(2011, 11, '2026-03-08', 'Shipped'),
(2012, 12, '2026-03-09', 'Pending'),
(2013, 13, '2026-03-10', 'Shipped'),
(2014, 14, '2026-03-10', 'Shipped'),
(2015, 15, '2026-03-11', 'Shipped'),
(2016, 16, '2026-03-12', 'Returned'),
(2017, 17, '2026-03-12', 'Shipped'),
(2018, 18, '2026-03-13', 'Shipped'),
(2019, 19, '2026-03-14', 'Processing'),
(2020, 20, '2026-03-14', 'Shipped'),
(2021, 21, '2026-03-15', 'Shipped'),
(2022, 22, '2026-03-16', 'Pending'),
(2023, 23, '2026-03-17', 'Shipped'),
(2024, 24, '2026-03-17', 'Shipped'),
(2025, 25, '2026-03-18', 'Shipped'),
(2026, 26, '2026-03-19', 'Returned'),
(2027, 27, '2026-03-19', 'Shipped'),
(2028, 28, '2026-03-20', 'Shipped'),
(2029, 29, '2026-03-21', 'Processing'),
(2030, 30, '2026-03-21', 'Shipped'),
(2031, 31, '2026-03-22', 'Shipped'),
(2032, 32, '2026-03-23', 'Shipped'),
(2033, 33, '2026-03-23', 'Pending'),
(2034, 34, '2026-03-24', 'Shipped'),
(2035, 35, '2026-03-25', 'Shipped'),
(2036, 36, '2026-03-25', 'Shipped'),
(2037, 37, '2026-03-26', 'Processing'),
(2038, 38, '2026-03-26', 'Shipped'),
(2039, 39, '2026-03-26', 'Shipped'),
(2040, 40, '2026-03-26', 'Shipped'),
(2041, 41, '2026-03-26', 'Shipped'),
(2042, 42, '2026-03-26', 'Cancelled'),
(2043, 43, '2026-03-26', 'Shipped'),
(2044, 44, '2026-03-26', 'Shipped'),
(2045, 45, '2026-03-26', 'Pending'),
(2046, 46, '2026-03-26', 'Shipped'),
(2047, 47, '2026-03-26', 'Shipped'),
(2048, 48, '2026-03-26', 'Shipped'),
(2049, 49, '2026-03-26', 'Processing'),
(2050, 50, '2026-03-26', 'Shipped');

INSERT INTO Products.Catalog (ProductID, ProductName, Description, Price, Category) VALUES
(1,'TechSpark X1','128GB Smartphone',15000,'Phones'),
(2,'Pro-Sound Buds','Wireless Earbud',2500,'Audio'),
(3,'Ultra Laptop','16GB RAM SSD',45000,'Computers'),
(4,'Gaming Mouse','RGB 16000 DPI',1200,'Accessories'),
(5,'Mech Keyboard','Blue Switches',3500,'Accessories'),
(6,'4K Monitor','27-inch IPS',12000,'Display'),
(7,'HD Webcam','1080p Stream',2200,'Video'),
(8,'USB-C Hub','7-in-1 Adapter',1500,'Accessories'),
(9,'Power Bank','20000mAh Fast',1800,'Power'),
(10,'Smart Watch','Health Tracker',5500,'Wearables'),
(11,'BT Speaker','Waterproof',2800,'Audio'),
(12,'Tablet Pro','11-inch Display',32000,'Computers'),
(13,'VR Headset','Standalone VR',25000,'Gaming'),
(14,'Desk Lamp','LED Dimmable',900,'Home'),
(15,'Wireless Chg','15W Qi Cert',1100,'Power'),
(16,'Ext HDD','2TB Portable',3800,'Storage'),
(17,'MicroSD Card','128GB U3',850,'Storage'),
(18,'Gaming Chair','Ergonomic',8500,'Furniture'),
(19,'Router AX','Wi-Fi 6 Dual',4200,'Network'),
(20,'Smart Plug','Wi-Fi Enabled',600,'Home'),
(21,'E-Reader','6-inch Paper',6500,'Books'),
(22,'Action Cam','4K Waterproof',9500,'Video'),
(23,'Drone Mini','GPS 4K Camera',18000,'Gadgets'),
(24,'Laptop Stand','Aluminum',1300,'Accessories'),
(25,'LAN Cable','Cat6 5m',300,'Network'),
(26,'Printer Ink','Eco-Tank',4500,'Computers'),
(27,'Soundbar','2.1 Channel',7500,'Audio'),
(28,'DSLR Camera','24MP Body',35000,'Video'),
(29,'GPU RTX','RTX 4060',22000,'Parts'),
(30,'CPU Cooler','Air RGB',2500,'Parts'),
(31,'RAM DDR4','16GB 3200',3200,'Parts'),
(32,'NVMe SSD','1TB Gen4',5200,'Storage'),
(33,'M-Board','B550 ATX',7800,'Parts'),
(34,'PC Case','Mid Tower',4000,'Parts'),
(35,'PSU 750W','80+ Gold',5500,'Parts'),
(36,'USB Mic','Condenser',3800,'Audio'),
(37,'Pen Tablet','10-inch',4500,'Design'),
(38,'HDMI 2.1','4K 120Hz',500,'Accessories'),
(39,'Trackball','Ergonomic',2900,'Accessories'),
(40,'Projector','Portable',11000,'Video'),
(41,'Smart Bulb','RGB Zigbee',750,'Home'),
(42,'Security Cam','360 Indoor',2400,'Home'),
(43,'NAS Drive','4TB NAS',6800,'Storage'),
(44,'SATA SSD','500GB 2.5',2200,'Storage'),
(45,'UPS 1kVA','Battery',5800,'Power'),
(46,'KVM Switch','2 Port',3200,'Network'),
(47,'Case Fan','120mm PWM',450,'Parts'),
(48,'Thermal Paste','High Perf',350,'Parts'),
(49,'Laptop Bag','15-inch',1500,'Accessories'),
(50,'Phone Stand','Metal',400,'Accessories');

INSERT INTO Customers.Info (CustomerID, Name, Email, SignupDate) VALUES
(1,'Juan Cruz','juan@email.com','2026-01-01'),
(2,'Maria Santos','maria@email.com','2026-01-02'),
(3,'Pedro P','pedro@email.com','2026-01-05'),
(4,'Ana Reyes','ana@email.com','2026-01-10'),
(5,'Jose Rizal','jose@email.com','2026-01-12'),
(6,'Liza S','liza@email.com','2026-01-15'),
(7,'Coco M','coco@email.com','2026-01-18'),
(8,'Vic S','vic@email.com','2026-01-20'),
(9,'Pia W','pia@email.com','2026-01-22'),
(10,'Cat G','cat@email.com','2026-01-25'),
(11,'Hanzel C','hanzel@email.com','2026-01-28'),
(12,'Daphnie C','daphnie@email.com','2026-01-30'),
(13,'Ben A','ben@email.com','2026-02-01'),
(14,'Clara B','clara@email.com','2026-02-02'),
(15,'Dex S','dex@email.com','2026-02-03'),
(16,'Elena V','elena@email.com','2026-02-04'),
(17,'Felix T','felix@email.com','2026-02-05'),
(18,'Gina L','gina@email.com','2026-02-06'),
(19,'Hans U','hans@email.com','2026-02-07'),
(20,'Iris G','iris@email.com','2026-02-08'),
(21,'Jack S','jack@email.com','2026-02-09'),
(22,'Karl U','karl@email.com','2026-02-10'),
(23,'Leo L','leo@email.com','2026-02-11'),
(24,'Mina K','mina@email.com','2026-02-12'),
(25,'Noel R','noel@email.com','2026-02-13'),
(26,'Oma R','oma@email.com','2026-02-14'),
(27,'Paul D','paul@email.com','2026-02-15'),
(28,'Quinn L','quinn@email.com','2026-02-16'),
(29,'Rina S','rina@email.com','2026-02-17'),
(30,'Sam T','sam@email.com','2026-02-18'),
(31,'Tina W','tina@email.com','2026-02-19'),
(32,'Uly H','uly@email.com','2026-02-20'),
(33,'Vera J','vera@email.com','2026-02-21'),
(34,'Will B','will@email.com','2026-02-22'),
(35,'Xena P','xena@email.com','2026-02-23'),
(36,'Yuri M','yuri@email.com','2026-02-24'),
(37,'Zane K','zane@email.com','2026-02-25'),
(38,'Abe N','abe@email.com','2026-02-26'),
(39,'Bibi L','bibi@email.com','2026-02-27'),
(40,'Cid M','cid@email.com','2026-02-28'),
(41,'Dan K','dan@email.com','2026-03-01'),
(42,'Eve S','eve@email.com','2026-03-02'),
(43,'Fay R','fay@email.com','2026-03-03'),
(44,'Guy N','guy@email.com','2026-03-04'),
(45,'Hope P','hope@email.com','2026-03-05'),
(46,'Ian T','ian@email.com','2026-03-06'),
(47,'Joy R','joy@email.com','2026-03-07'),
(48,'Ken D','ken@email.com','2026-03-08'),
(49,'Lea F','lea@email.com','2026-03-09'),
(50,'Moe G','moe@email.com','2026-03-10');

INSERT INTO Customers.Addresses (AddressID, CustomerID, AddressLine, IsDefault) VALUES
(1, 1, '123 Colon St, Cebu City', 1),
(2, 2, '456 Gorordo Ave, Cebu City', 1),
(3, 3, '789 AS Fortuna, Mandaue', 1),
(4, 4, '101 Banilad Rd, Cebu City', 1),
(5, 5, '202 V. Rama Ave, Cebu City', 1),
(6, 6, '303 Katipunan St, Labangon', 1),
(7, 7, '404 P. del Rosario, Cebu City', 1),
(8, 8, '505 Escario St, Cebu City', 1),
(9, 9, '606 Salinas Dr, Lahug', 1),
(10, 10, '707 MJ Cuenco, Mabolo', 1),
(11, 11, '808 Juan Luna St, Cebu City', 1),
(12, 12, '909 Osmeña Blvd, Cebu City', 1),
(13, 13, '111 Tres de Abril, Labangon', 1),
(14, 14, '222 Duterte St, Banawa', 1),
(15, 15, '333 Maguikay, Mandaue City', 1),
(16, 16, '444 Bakilid, Mandaue City', 1),
(17, 17, '555 Subangdaku, Mandaue', 1),
(18, 18, '666 Tipolo, Mandaue City', 1),
(19, 19, '777 Basak, Lapu-Lapu City', 1),
(20, 20, '888 Marigondon, Lapu-Lapu', 1),
(21, 21, '999 Pajac, Lapu-Lapu City', 1),
(22, 22, '123 Gun-ob, Lapu-Lapu City', 1),
(23, 23, '456 Pusok, Lapu-Lapu City', 1),
(24, 24, '789 Babag, Lapu-Lapu City', 1),
(25, 25, '101 Talisay Road, Talisay', 1),
(26, 26, '202 Bulacao, Talisay City', 1),
(27, 27, '303 Tabunok, Talisay City', 1),
(28, 28, '404 Minglanilla Rd, Cebu', 1),
(29, 29, '505 Naga Highwy, Naga City', 1),
(30, 30, '606 San Fernando, Cebu', 1),
(31, 31, '707 Carcar Blvd, Carcar', 1),
(32, 32, '808 Sibonga Road, Cebu', 1),
(33, 33, '909 Argao Central, Cebu', 1),
(34, 34, '111 Dalaguete Highway, Cebu', 1),
(35, 35, '222 Alcoy Coast, Cebu', 1),
(36, 36, '333 Boljoon Proper, Cebu', 1),
(37, 37, '444 Oslob Whale St, Cebu', 1),
(38, 38, '555 Santander Rd, Cebu', 1),
(39, 39, '666 Samboan Falls, Cebu', 1),
(40, 40, '777 Ginatilan Road, Cebu', 1),
(41, 41, '888 Malabuyoc St, Cebu', 1),
(42, 42, '999 Alegria Coast, Cebu', 1),
(43, 43, '123 Badian Proper, Cebu', 1),
(44, 44, '456 Moalboal Beach Rd, Cebu', 1),
(45, 45, '789 Alcantara Rd, Cebu', 1),
(46, 46, '101 Ronda Highway, Cebu', 1),
(47, 47, '202 Dumanjug Road, Cebu', 1),
(48, 48, '303 Barili Center, Cebu', 1),
(49, 49, '404 Aloguinsan Rd, Cebu', 1),
(50, 50, '505 Pinamungajan, Cebu', 1);

INSERT INTO Products.Suppliers (SupplierID, SupplierName, ContactInfo) VALUES
(1, 'Global Tech Supply', 'contact@globaltech.com'),
(2, 'Electro-Hub Ph', 'support@electrohub.ph'),
(3, 'Computer Parts Inc', 'sales@comp-parts.com'),
(4, 'Audio Pro Logistics', 'info@audiopro.ph'),
(5, 'Smart Home Distributors', 'admin@smarthome.com'),
(6, 'Gadget King Wholesale', 'deals@gadgetking.com'),
(7, 'Network Solutions Ltd', 'tech@netsol.com'),
(8, 'Storage Master Corp', 'warehouse@storage.com'),
(9, 'Power Up Battery Co', 'power@batteryco.ph'),
(10, 'Wearable Tech Group', 'hello@weartech.com'),
(11, 'Vision Display Systems', 'sales@visiondisplay.com'),
(12, 'Click-Key Peripherals', 'info@clickkey.ph'),
(13, 'Elite Gaming Gear', 'support@elitegaming.com'),
(14, 'Cables & More', 'orders@cablesmore.com'),
(15, 'FastCharge Solutions', 'tech@fastcharge.ph'),
(16, 'PureSound Audio', 'admin@puresound.com'),
(17, 'MegaDrive Storage', 'sales@megadrive.com'),
(18, 'Eco-Ink Supplies', 'contact@ecoink.ph'),
(19, 'SkyDrone Gadgets', 'info@skydrone.com'),
(20, 'BrightLight Home', 'support@brightlight.com'),
(21, 'SecureCam Systems', 'sales@securecam.ph'),
(22, 'Router-Max Network', 'admin@routermax.com'),
(23, 'Pro-Cool Cooling', 'tech@procool.com'),
(24, 'Titan PC Cases', 'orders@titanpc.com'),
(25, 'GoldStandard PSU', 'info@goldpsu.ph'),
(26, 'Studio Mic Experts', 'sales@micexperts.com'),
(27, 'Graphic Pen Tablets', 'support@pentablets.com'),
(28, '4K Projection Co', 'admin@4kproject.com'),
(29, 'SmartHub Zigbee', 'tech@smarthub.ph'),
(30, 'Portable Power Ph', 'sales@portapower.ph'),
(31, 'Ergo-Chair Designs', 'info@ergochair.com'),
(32, 'Wireless Range Ltd', 'support@wirelessrange.com'),
(33, 'DataBackup NAS', 'admin@datanas.com'),
(34, 'PrintMaster Ink', 'sales@printmaster.ph'),
(35, 'Gaming Mouse Lab', 'tech@mouselab.com'),
(36, 'Hi-Def Webcams', 'orders@hidefweb.com'),
(37, 'USB-C Specialist', 'info@usbspecial.com'),
(38, 'Memory Card Pro', 'sales@memcardpro.ph'),
(39, 'Laptop Stand Co', 'support@laptopstand.com'),
(40, 'LAN Cable Factory', 'admin@lanfactory.com'),
(41, 'Soundbar Central', 'sales@soundcentral.com'),
(42, 'ActionCam Direct', 'info@actioncam.ph'),
(43, 'MiniDrone World', 'support@minidrone.com'),
(44, 'Thermal Paste Pro', 'tech@thermalpro.com'),
(45, 'Case Fan Supply', 'admin@casefan.com'),
(46, 'UPS Battery Hub', 'sales@upshub.ph'),
(47, 'KVM Switch Tech', 'info@kvmtech.com'),
(48, 'Laptop Bag Designs', 'support@laptopbag.com'),
(49, 'Phone Stand Maker', 'admin@phonestand.ph'),
(50, 'Tech Gadget Inc', 'sales@techgadget.com');


INSERT INTO Inventory.Stock (ProductID, WarehouseID, QuantityOnHand, ReorderLevel)
SELECT ProductID, (ProductID % 2) + 1, (ProductID * 7) % 100, 5 FROM Products.Catalog;

INSERT INTO Orders.Orders (OrderID, CustomerID, OrderDate, Status)
SELECT 2000 + CustomerID, CustomerID, GETDATE(), 'Shipped' FROM Customers.Info;

INSERT INTO Orders.OrderDetails (OrderDetailID, OrderID, ProductID, Quantity, UnitPrice)
SELECT CustomerID, 2000 + CustomerID, CustomerID, 1, 1000.00 FROM Customers.Info;
GO

-- =============================================
-- 4. SECURITY: USERS AND ROLES
-- =============================================
CREATE USER ContentManager_Chris WITHOUT LOGIN;
CREATE USER CustomerService_Karen WITHOUT LOGIN;
CREATE USER OrderProcessor_Oscar WITHOUT LOGIN;
CREATE USER Warehouse_Wally WITHOUT LOGIN;
CREATE USER Marketing_Monica WITHOUT LOGIN;

CREATE ROLE ContentEditors;
CREATE ROLE SupportAgents;
CREATE ROLE OrderTeam;
CREATE ROLE WarehouseStaff;
CREATE ROLE MarketingTeam;

EXEC sp_addrolemember 'ContentEditors', 'ContentManager_Chris';
EXEC sp_addrolemember 'SupportAgents', 'CustomerService_Karen';
EXEC sp_addrolemember 'OrderTeam', 'OrderProcessor_Oscar';
EXEC sp_addrolemember 'WarehouseStaff', 'Warehouse_Wally';
EXEC sp_addrolemember 'MarketingTeam', 'Marketing_Monica';
GO

-- =============================================
-- 5. CHALLENGE: CREATE WAREHOUSE VIEW
-- =============================================
GO
CREATE VIEW Inventory.vw_WarehouseStockList AS
SELECT 
    P.ProductID, 
    P.ProductName, 
    S.QuantityOnHand, 
    S.WarehouseID
FROM Products.Catalog P
JOIN Inventory.Stock S ON P.ProductID = S.ProductID;
GO
--This View gives Wally the Name + ID + Stock Level
-- Notice: We do NOT include the 'Price' column here!
CREATE OR ALTER VIEW Inventory.vw_WarehouseStockList AS
SELECT 
    S.ProductID, 
    P.ProductName, 
    S.QuantityOnHand, 
    W.Location
FROM Inventory.Stock S
JOIN Products.Catalog P ON S.ProductID = P.ProductID
JOIN Inventory.Warehouses W ON S.WarehouseID = W.WarehouseID;

CREATE OR ALTER VIEW Inventory.vw_WarehousePickingList AS
SELECT 
    S.ProductID, 
    P.ProductName, 
    S.QuantityOnHand, 
    W.Location
FROM Inventory.Stock S
JOIN Products.Catalog P ON S.ProductID = P.ProductID
JOIN Inventory.Warehouses W ON S.WarehouseID = W.WarehouseID;
-- Monica runs this to see her target audience
-- =============================================
-- 6. SECURITY REQUIREMENTS IMPLEMENTATION
-- =============================================

-- 1. Content Editors (Chris)
GRANT SELECT, INSERT, UPDATE, DELETE ON Products.Catalog TO ContentEditors;
GRANT INSERT ON Products.Suppliers TO ContentEditors;
GRANT SELECT ON Products.Suppliers TO ContentEditors;
DENY SELECT ON SCHEMA::Customers TO ContentEditors;
DENY SELECT ON SCHEMA::Orders TO ContentEditors;
DENY SELECT ON SCHEMA::Inventory TO ContentEditors;

-- 2. Customer Service Agents (Karen)
GRANT SELECT ON Customers.Info TO SupportAgents;
GRANT SELECT ON Customers.Addresses TO SupportAgents;
GRANT SELECT ON SCHEMA::Orders TO SupportAgents;
GRANT UPDATE ON Orders.Orders TO SupportAgents; 
DENY UPDATE ON Products.Catalog(Price) TO SupportAgents; 
DENY SELECT ON SCHEMA::Inventory TO SupportAgents;

-- 3. Order Processors (Oscar)
GRANT INSERT, SELECT ON Orders.Orders TO OrderTeam;
GRANT INSERT, SELECT ON Orders.OrderDetails TO OrderTeam;
GRANT SELECT ON Products.Catalog TO OrderTeam;
GRANT SELECT ON Customers.Info TO OrderTeam;
DENY UPDATE, DELETE ON Products.Catalog TO OrderTeam;

-- 4. Warehouse Staff (Wally)
GRANT SELECT, UPDATE ON Inventory.Stock TO WarehouseStaff;
GRANT SELECT ON Inventory.Warehouses TO WarehouseStaff;
GRANT SELECT ON Inventory.vw_WarehouseStockList TO WarehouseStaff; -- Use the View
DENY SELECT ON SCHEMA::Customers TO WarehouseStaff;-- This blocks Customer Info
DENY SELECT ON Products.Catalog TO WarehouseStaff; -- This blocks Prices!
GRANT SELECT ON Inventory.vw_WarehousePickingList TO WarehouseStaff;

-- 5. Marketing Team (Monica)
GRANT SELECT, INSERT, UPDATE, DELETE ON Marketing.Campaigns TO Marketing_Monica;
GRANT SELECT (CustomerID, Name, Email) ON Customers.Info TO Marketing_Monica; -- Column Grant
GRANT SELECT ON Orders.Orders TO Marketing_Monica;
GRANT SELECT ON Orders.OrderDetails TO Marketing_Monica;
DENY SELECT ON Customers.Addresses TO Marketing_Monica;
DENY SELECT ON SCHEMA::Inventory TO Marketing_Monica;
GRANT SELECT (ProductID, ProductName, Category) ON Products.Catalog TO Marketing_Monica;
GO

PRINT 'E-Commerce Database Setup and Tasks are successfully completed!';


--1.Content Editors (ContentManager_Chris):
EXECUTE AS USER = 'ContentManager_Chris';
--Full control (SELECT, INSERT, UPDATE, DELETE) over Products.Catalog.
SELECT * FROM Products.Catalog;
--example no para makita nga maka CONTROL siya sa Products
INSERT INTO Products.Catalog (ProductID, ProductName, Description, Price, Category)
VALUES (51, 'TechSpark Z9', 'New 2026 Flagship Phone', 25000.00, 'Phones');
--NYA view if naa bay nausab
SELECT * FROM Products.Catalog WHERE ProductID = 51;
--Can view supplier information.
SELECT * FROM Products.Suppliers;
--No access to customer data, orders, or inventory levels.
SELECT * FROM Customers.Info; -- gi deny ang information sa customer data, orders, or inventory levels.
REVERT;
GO



--2.Customer Service Agents (CustomerService_Karen):
EXECUTE AS USER = 'CustomerService_Karen';
--Can view customer information (Customers.Info, Customers.Addresses) to help with account issues.
SELECT * FROM Customers.Info;
SELECT * FROM Customers.Addresses;


--Can view order history for a customer (Orders schema).
SELECT * FROM Orders.Orders;

--Can update order status (e.g., mark as shipped, handle returns).
--example rani tan awa ang order before siya ma change
SELECT OrderID, Status FROM Orders.Orders WHERE OrderID = 2005;
--mag update na
UPDATE Orders.Orders 
SET Status = 'Returned' 
WHERE OrderID = 2005;


--CANNOT modify prices in the product catalog. dili siya maka change sa price
UPDATE Products.Catalog 
SET Price = 1.00 
WHERE ProductID = 1;


--CANNOT view inventory stock levels. di siya maka view sa inventory
SELECT * FROM Inventory.Stock;
REVERT;
GO

--3.Order Processors (OrderProcessor_Oscar):
EXECUTE AS USER = 'OrderProcessor_Oscar';

--Need to insert new orders and order details.
INSERT INTO Orders.Orders (OrderID, CustomerID, OrderDate, Status)
VALUES (5000, 11, GETDATE(), 'Pending');
--order details
INSERT INTO Orders.OrderDetails (OrderDetailID, OrderID, ProductID, Quantity, UnitPrice)
VALUES (7000, 5000, 1, 2, 15000.00);
--Verify the New Order exists
SELECT * FROM Orders.Orders WHERE OrderID = 5000;
SELECT * FROM Orders.OrderDetails WHERE OrderID = 5000;

--Need to read product prices and customer information to process orders.
SELECT 
    O.OrderID,
    C.Name AS Customer_Name,
    C.Email,
    P.ProductName,
    P.Category,
    OD.Quantity,
    P.Price AS Unit_Price,
    (OD.Quantity * P.Price) AS Line_Total, -- Calculates the total for that item
    O.Status,
    O.OrderDate
FROM Orders.Orders O
JOIN Customers.Info C ON O.CustomerID = C.CustomerID
JOIN Orders.OrderDetails OD ON O.OrderID = OD.OrderID
JOIN Products.Catalog P ON OD.ProductID = P.ProductID
ORDER BY O.OrderDate DESC;

--Should NOT modify product catalog or inventory directly. 
UPDATE Products.Catalog 
SET Price = 5.00 
WHERE ProductID = 1;
REVERT;
GO
--4.Warehouse Staff (Warehouse_Wally):
EXECUTE AS USER = 'Warehouse_Wally';
--Need to view and update inventory levels (Inventory.Stock) when items are picked/packed.
--ni view the inventory 
SELECT * FROM Inventory.vw_WarehouseStockList;
--PICK/PACK (Requirement: Update stock)
UPDATE Inventory.Stock 
SET QuantityOnHand = QuantityOnHand - 1 
WHERE ProductID = 1;
--Then verify if nag change bah
SELECT * FROM Inventory.Stock WHERE ProductID = 1;
--Need to view product names and IDs to know what to pick.
SELECT * FROM Inventory.vw_WarehousePickingList;
--Should NOT see product costs/prices (if they differ from selling price) or customer information.
SELECT * FROM Products.Catalog;
SELECT * FROM Customers.Info;
REVERT;
GO


--5.  Marketing Team (Marketing_Monica):
EXECUTE AS USER = 'Marketing_Monica';
--Full control over Marketing.Campaigns.
SELECT * FROM Marketing.Campaigns;
--Need to see customer email addresses (for marketing emails) and order history (to analyze buying patterns).
SELECT 
    C.Name, 
    C.Email, 
    O.OrderDate, 
    P.ProductName,
    OD.Quantity
FROM Customers.Info C
JOIN Orders.Orders O ON C.CustomerID = O.CustomerID
JOIN Orders.OrderDetails OD ON O.OrderID = OD.OrderID
JOIN Products.Catalog P ON OD.ProductID = P.ProductID;

--Should NOT see customer addresses or phone numbers (privacy).
DENY SELECT ON Customers.Addresses TO MarketingTeam;--Should NOT see inventory data.
--Should NOT see inventory data.
SELECT * FROM Inventory.Stock;
REVERT;
GO
