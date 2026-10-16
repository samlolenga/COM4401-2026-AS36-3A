-- 1. EMPLOYEE ROLES

CREATE TABLE EmployeeRoles (
  RoleID INT PRIMARY KEY,
  RoleName VARCHAR(50) NOT NULL,
  StaffCount INT NOT NULL,
  Tasks VARCHAR(255) NOT NULL,
  PerformanceNeed VARCHAR(100) NOT NULL,
  BudgetPerUnit DECIMAL(8,2) NOT NULL
);

INSERT INTO EmployeeRoles
  (RoleID, RoleName, StaffCount, Tasks, PerformanceNeed, BudgetPerUnit)
VALUES
  (1, 'Administrative Assistant', 3, 'Email, documents, spreadsheets, web systems, online meetings, and basic customer records', 'Basic office hardware workstation', 950.00),
  (2, 'Project Manager', 2, 'Reports, meetings, project planning, reviewing drawings, dashboards, and client communication', 'Business workstation with stronger display/workflow setup', 1300.00),
  (3, 'Architect / CAD Designer', 5, 'CAD drawings, 2D drafting, 3D modelling, large design files, multiple monitors, and design reviews', 'CAD workstation with dedicated GPU and suitable display', 2500.00),
  (4, '3D Visualisation Specialist', 2, 'Rendering, 3D visualisation, large models, high-resolution textures, media output, and client visual presentations', 'High-performance rendering/visualisation workstation', 3750.00);


-- 2. WORKSTATION BUILDS

CREATE TABLE WorkstationBuilds (
  BuildID INT PRIMARY KEY,
  RoleID INT NOT NULL,
  BuildName VARCHAR(100) NOT NULL,
  Source VARCHAR(50) NOT NULL,
  FOREIGN KEY (RoleID) REFERENCES EmployeeRoles(RoleID)
);

INSERT INTO WorkstationBuilds (BuildID, RoleID, BuildName, Source)
VALUES
  (1, 1, 'Admin Build', 'BuildCores.com'),
  (2, 2, 'Project Manager Build', 'BuildCores.com'),
  (3, 3, 'CAD Build', 'BuildCores.com'),
  (4, 4, '3D Visualisation Build', 'BuildCores.com');

-- 3. BUILD ITEMS

CREATE TABLE BuildItems (
  ItemID INT PRIMARY KEY,
  BuildID INT NOT NULL,
  HardwareCategory VARCHAR(50) NOT NULL,
  ItemName VARCHAR(100) NOT NULL,
  Specification VARCHAR(150) NOT NULL,
  Cost DECIMAL(8,2) NOT NULL,
  FOREIGN KEY (BuildID) REFERENCES WorkstationBuilds(BuildID)
);

INSERT INTO BuildItems
  (ItemID, BuildID, HardwareCategory, ItemName, Specification, Cost)
VALUES
(401, 4, 'Case', 'NZXT H5 Flow (2024) ATX Mid Tower White', 'ATX Mid Tower with Tempered Glass, USB 3.2 Gen 2x2 Type-C', 58.95),
(402, 4, 'CPU', 'Intel Core i9-14900K', '24 Cores (8 Performance + 16 Efficient), Up to 6.0 GHz', 429.00),
(403, 4, 'Motherboard', 'ASUS PRIME Z790-A WIFI LGA1700 DDR5 ATX', 'LGA1700, DDR5 support, PCIe 5.0, Built-in Wi-Fi & LAN', 219.98),
(404, 4, 'GPU', 'Gigabyte GeForce RTX 5080 GAMING OC 16G', '16GB GDDR7, Ray Tracing, High-performance 3D rendering', 1344.99),
(405, 4, 'RAM', 'ADATA XPG LANCER RGB White 32GB (2x16GB)', 'DDR5 6000MHz CL30, Dual Channel Kit', 424.99),
(406, 4, 'CPU Cooler', 'NZXT Kraken Elite 360 RGB White (2024)', '360mm AIO Liquid Cooler with LCD Display', 229.99),
(407, 4, 'Storage', 'Kingston KC3000 2TB SSD M.2 PCIe 4.0 NVMe', '2TB High-Speed NVMe M.2 Solid State Drive', 297.99),
(408, 4, 'Power Supply', 'Seasonic Focus V4 GX-1000 Modular PSU', '1000W 80+ Gold, Fully Modular ATX 3.1 White', 129.00),
(409, 4, 'Case Fan', 'Arctic P12 Pro PST 120 White PWM', '120mm Pressure-Optimised Fan', 5.99),
(410, 4, 'Case Fan', 'Arctic P12 Pro PST 120 White PWM', '120mm Pressure-Optimised Fan', 5.99),
(411, 4, 'Mousepad', 'SteelSeries QcK Prism Cloth XL RGB', 'XL RGB Gaming Mouse Pad - Black', 54.97),
(412, 4, 'Headphones', 'HyperX Cloud III S Wired - White', 'Wired Headset with Clear Noise-Cancelling Microphone', 69.99),
(413, 4, 'Mouse', 'Razer DeathAdder V3 Pro Wireless Optical', 'Wireless High-DPI Precision Mouse - Black', 92.99),
(414, 4, 'Webcam', 'Logitech 4K Webcam', 'Ultra HD 4K Camera for Video Calls', 110.99),
(415, 4, 'Keyboard', 'EPOMAKER Ajazz AK820 Pro 75% Wireless', 'Mechanical Keyboard with Smart Display & *****', 68.99),
(416, 4, 'Cable Extension', 'EZDIY-FAB 12VHPWR PSU Extension Kit White', 'Flexible Sleeved Extension Cables', 34.99),
(417, 4, 'Ethernet Cable', 'DDMALL 3m 2 Pack Cat 8 Ethernet Cable', 'Cat 8 High-Speed Network Cable', 12.99),
(418, 4, 'HDMI Cable', 'Snowkids 10K 8K HDMI 2.1 Cable 2M', 'Ultra High Speed HDMI 2.1 Display Cable', 6.99),
(419, 4, 'Power Strip', 'HAFINO Tower Extension Lead (Grey/White)', '12-Way Vertical Plug Extension with Surge Protection', 24.63),
(420, 4, 'Monitor', 'KOORUI 27E1QA 27" 1440p 144Hz VA Monitor', '27-inch QHD (2560x1440) 144Hz Display', 125.00);


-- 4. RECOMMENDATIONS

CREATE TABLE Recommendations (
  RecommendationID INT PRIMARY KEY,
  RoleID INT NOT NULL,
  Justification TEXT NOT NULL,
  Compromise TEXT NOT NULL,
  Approved BOOLEAN NOT NULL,
  EthicalNotes TEXT NOT NULL,
  FOREIGN KEY (RoleID) REFERENCES EmployeeRoles(RoleID)
);

INSERT INTO Recommendations
  (RecommendationID, RoleID, Justification, Compromise, Approved, EthicalNotes)
VALUES
  (1, 1,
   'This workstation gives enough performance for everyday office tasks without buying unnecessary expensive components. The Ryzen 5 processor, 16GB RAM and NVMe SSD handle emails, documents, spreadsheets, web browsing and online meetings.',
   'No dedicated graphics card, because the Administrative Assistant does not do CAD or 3D rendering. Integrated graphics keeps the cost down. 500GB storage is enough for normal office files.',
   TRUE,
   'Buying only what the role needs avoids wasting company money on hardware that would not be used. Software such as Windows and Microsoft 365 is managed separately and is not included in the hardware budget.'),
  (4, 4,
   'High-performance CPU and GPU selected to deliver rapid ray tracing and handle heavy 3D rendering workloads without thermal throttling.',
   'Selected 32GB RAM initially instead of 64GB to remain near budget limits, while allowing a future upgrade path.',
   TRUE,
   'Investing in energy-efficient 80+ Gold PSU and liquid cooling ensures long-term hardware reliability and lower power draw.');


-- Query 1: List every role
SELECT * FROM EmployeeRoles;


-- Query 2: Just the names and budgets
SELECT RoleName, BudgetPerUnit FROM EmployeeRoles;


-- Query 3: The higher-budget roles (over £1000)
SELECT RoleName, BudgetPerUnit FROM EmployeeRoles WHERE BudgetPerUnit > 1000;


-- Query 4: Roles by team size, largest first
SELECT RoleName, StaffCount FROM EmployeeRoles ORDER BY StaffCount DESC;


-- Query 5: Every item in build 4
SELECT * FROM BuildItems WHERE BuildID = 4;


-- Query 6: Count the items in build 4
SELECT COUNT(*) AS ItemCount FROM BuildItems WHERE BuildID = 4;


-- Query 7: Total cost of build 4
SELECT SUM(Cost) AS TotalCost FROM BuildItems WHERE BuildID = 4;


-- Query 8: Cost of every build, most expensive first
SELECT BuildID, SUM(Cost) AS TotalCost FROM BuildItems GROUP BY BuildID ORDER BY TotalCost DESC;


-- Query 9: Which role is each build for?
SELECT b.BuildName, r.RoleName
FROM WorkstationBuilds b
JOIN EmployeeRoles r ON b.RoleID = r.RoleID;


-- Query 10: Items with their build and role
SELECT i.HardwareCategory, i.ItemName, i.Specification, i.Cost, b.BuildName, r.RoleName
FROM BuildItems i
JOIN WorkstationBuilds b ON i.BuildID = b.BuildID
JOIN EmployeeRoles r ON b.RoleID = r.RoleID;


-- Query 11: Spend per role
SELECT r.RoleName, SUM(i.Cost) AS TotalSpend
FROM BuildItems i
JOIN WorkstationBuilds b ON i.BuildID = b.BuildID
JOIN EmployeeRoles r ON b.RoleID = r.RoleID
GROUP BY r.RoleName;


-- Role totals vs budget
SELECT r.RoleName,
       r.StaffCount,
       SUM(i.Cost) AS CostPerPC,
       SUM(i.Cost) * r.StaffCount AS RoleTotal,
       r.BudgetPerUnit * r.StaffCount AS RoleBudget
FROM BuildItems i
JOIN WorkstationBuilds b ON i.BuildID = b.BuildID
JOIN EmployeeRoles r ON b.RoleID = r.RoleID
GROUP BY r.RoleID, r.RoleName, r.StaffCount, r.BudgetPerUnit;


-- Check the other tables
SELECT * FROM WorkstationBuilds;
SELECT * FROM Recommendations;