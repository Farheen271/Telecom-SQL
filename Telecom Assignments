-- Step 1: Create the Database
CREATE DATABASE TelecomDB;
USE TelecomDB;

-- Step 2: Create Tables

-- 1. Customer Table
CREATE TABLE Customer (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20),
    address TEXT
);

-- 2. ServicePlan Table
CREATE TABLE ServicePlan (
    plan_id INT PRIMARY KEY,
    plan_name VARCHAR(50),
    plan_type ENUM('Prepaid', 'Postpaid') NOT NULL,
    monthly_fee DECIMAL(10, 2) CHECK (monthly_fee >= 0),
    call_limit INT CHECK (call_limit >= 0),
    sms_limit INT CHECK (sms_limit >= 0),
    data_limit INT CHECK (data_limit >= 0) -- in MB
);

-- 3. Subscription Table
CREATE TABLE Subscription (
    subscription_id INT PRIMARY KEY,
    customer_id INT,
    plan_id INT,
    start_date DATE NOT NULL,
    end_date DATE,
    FOREIGN KEY (customer_id) REFERENCES Customer(customer_id),
    FOREIGN KEY (plan_id) REFERENCES ServicePlan(plan_id)
);

-- 4. CallRecord Table
CREATE TABLE CallRecord (
    call_id INT PRIMARY KEY AUTO_INCREMENT,
    subscription_id INT,
    call_time DATETIME,
    duration INT CHECK (duration > 0), -- in seconds
    receiver_number VARCHAR(20),
    location_id INT,
    FOREIGN KEY (subscription_id) REFERENCES Subscription(subscription_id)
);

-- 5. SMSRecord Table
CREATE TABLE SMSRecord (
    sms_id INT PRIMARY KEY AUTO_INCREMENT,
    subscription_id INT,
    sms_time DATETIME,
    receiver_number VARCHAR(20),
    sms_length INT CHECK (sms_length >= 1),
    FOREIGN KEY (subscription_id) REFERENCES Subscription(subscription_id)
);

-- 6. DataUsage Table
CREATE TABLE DataUsage (
    usage_id INT PRIMARY KEY AUTO_INCREMENT,
    subscription_id INT,
    session_start DATETIME,
    session_end DATETIME,
    data_mb DECIMAL(10, 2) CHECK (data_mb >= 0),
    location_id INT,
    FOREIGN KEY (subscription_id) REFERENCES Subscription(subscription_id)
);

-- 7. Billing Table
CREATE TABLE Billing (
    bill_id INT PRIMARY KEY AUTO_INCREMENT,
    subscription_id INT,
    billing_month DATE,
    billing_amount DECIMAL(10, 2) CHECK (billing_amount >= 0),
    payment_status ENUM('Paid', 'Unpaid', 'Overdue'),
    FOREIGN KEY (subscription_id) REFERENCES Subscription(subscription_id)
);

-- 8. CustomerSupport Table
CREATE TABLE CustomerSupport (
    ticket_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    issue_date DATETIME,
    issue_description TEXT,
    support_status ENUM('Open', 'In Progress', 'Closed'),
    FOREIGN KEY (customer_id) REFERENCES Customer(customer_id)
);

-- 9. Device Table
CREATE TABLE Device (
    device_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    device_model VARCHAR(100),
    imei_number VARCHAR(20) UNIQUE,
    registered_date DATE,
    location_id INT,
    FOREIGN KEY (customer_id) REFERENCES Customer(customer_id)
);

-- 10. Location Table
CREATE TABLE Location (
    location_id INT PRIMARY KEY AUTO_INCREMENT,
    city VARCHAR(50),
    region VARCHAR(50),
    network_quality ENUM('Excellent', 'Good', 'Fair', 'Poor')
);

INSERT INTO Customer (customer_id, first_name, last_name, email, phone, address) VALUES
(1, 'Amit', 'Verma', 'amit.verma@gmail.com', '+91-9876543210', '123 MG Road, Delhi'),
(2, 'Sneha', 'Sharma', 'sneha.sharma@gmail.com', '+91-9823045671', '45 Laxmi Nagar, Pune'),
(3, 'Ravi', 'Patel', 'ravi.patel@yahoo.com', '+91-9898754321', '87 CG Road, Ahmedabad'),
(4, 'Priya', 'Singh', 'priya.singh@outlook.com', '+91-9123456780', '67 Banjara Hills, Hyderabad'),
(5, 'Karan', 'Mehta', 'karan.mehta@gmail.com', '+91-9955566677', '90 Sector 22, Chandigarh'),
(6, 'Anjali', 'Nair', 'anjali.nair@rediffmail.com', '+91-9787634521', '34 Marine Drive, Kochi'),
(7, 'Rahul', 'Reddy', 'rahul.reddy@gmail.com', '+91-9888899991', '56 Jubilee Hills, Hyderabad'),
(8, 'Divya', 'Joshi', 'divya.joshi@yahoo.in', '+91-9812345670', '101 Vile Parle, Mumbai'),
(9, 'Manoj', 'Kumar', 'manoj.kumar@live.com', '+91-9933344455', '76 Park Street, Kolkata'),
(10, 'Pooja', 'Das', 'pooja.das@gmail.com', '+91-9012345678', '54 Salt Lake, Kolkata'),
(11, 'Arjun', 'Iyer', 'arjun.iyer@gmail.com', '+91-9823445566', '88 Anna Nagar, Chennai'),
(12, 'Meera', 'Rao', 'meera.rao@yahoo.com', '+91-9988776655', '17 Malleswaram, Bangalore'),
(13, 'Nikhil', 'Thakur', 'nikhil.thakur@gmail.com', '+91-9789678901', '21 Model Town, Ludhiana'),
(14, 'Sonal', 'Kapoor', 'sonal.kapoor@gmail.com', '+91-9879879876', '32 Green Park, Delhi'),
(15, 'Harsh', 'Gupta', 'harsh.gupta@hotmail.com', '+91-9674567812', '78 Gariahat Road, Kolkata'),
(16, 'Neha', 'Mishra', 'neha.mishra@gmail.com', '+91-9445566778', '89 JP Nagar, Bangalore'),
(17, 'Vikas', 'Yadav', 'vikas.yadav@yahoo.com', '+91-9332211900', '11 Sadar Bazaar, Agra'),
(18, 'Ritu', 'Chawla', 'ritu.chawla@gmail.com', '+91-9112233445', '67 Shivaji Park, Mumbai'),
(19, 'Sandeep', 'Jain', 'sandeep.jain@gmail.com', '+91-9345541234', '25 Sector 17, Gurgaon'),
(20, 'Kavita', 'Bhatt', 'kavita.bhatt@rediffmail.com', '+91-9988667744', '10 Paldi, Ahmedabad'),
(21, 'Ashok', 'Bansal', 'ashok.bansal@gmail.com', '+91-9811142233', '31 Sector 14, Faridabad'),
(22, 'Roshni', 'Desai', 'roshni.desai@gmail.com', '+91-9090901212', '64 Karelibaug, Vadodara'),
(23, 'Tarun', 'Kulkarni', 'tarun.kulkarni@live.com', '+91-9123487654', '45 Deccan, Pune'),
(24, 'Bhavna', 'Jadhav', 'bhavna.jadhav@gmail.com', '+91-9556677889', '72 Aundh, Pune'),
(25, 'Naveen', 'Shetty', 'naveen.shetty@yahoo.in', '+91-9234567890', '88 Whitefield, Bangalore'),
(26, 'Swati', 'Malhotra', 'swati.malhotra@gmail.com', '+91-9845566123', '33 Sector 62, Noida'),
(27, 'Aditya', 'Chopra', 'aditya.chopra@gmail.com', '+91-9777722211', '12 Alwarpet, Chennai'),
(28, 'Tanya', 'Grover', 'tanya.grover@hotmail.com', '+91-9021223344', '50 Navi Mumbai, Mumbai'),
(29, 'Raghav', 'Agarwal', 'raghav.agarwal@gmail.com', '+91-9444455555', '14 Hazratganj, Lucknow'),
(30, 'Ishita', 'Pandey', 'ishita.pandey@gmail.com', '+91-9338899922', '92 Kankarbagh, Patna');


INSERT INTO ServicePlan (plan_id, plan_name, plan_type, monthly_fee, call_limit, sms_limit, data_limit) VALUES
(1, 'Lite Saver', 'Prepaid', 99.00, 100, 100, 1000),
(2, 'Smart Talk', 'Prepaid', 199.00, 300, 200, 2000),
(3, 'Data Pro', 'Postpaid', 399.00, 500, 500, 5000),
(4, 'Unlimited Max', 'Postpaid', 799.00, 10000, 5000, 99999),
(5, 'Youth Connect', 'Prepaid', 149.00, 200, 300, 1500),
(6, 'Business Elite', 'Postpaid', 999.00, 20000, 10000, 200000);

INSERT INTO Subscription (subscription_id, customer_id, plan_id, start_date, end_date) VALUES
(1, 1, 5, '2024-12-06', NULL),
(2, 2, 6, '2025-04-08', NULL),
(3, 3, 2, '2024-11-08', NULL),
(4, 4, 2, '2024-06-27', NULL),
(5, 5, 2, '2024-08-31', NULL),
(6, 6, 4, '2024-12-26', NULL),
(7, 7, 5, '2024-10-15', NULL),
(8, 8, 6, '2025-01-31', NULL),
(9, 9, 6, '2025-05-23', NULL),
(10, 10, 5, '2024-06-25', NULL),
(11, 11, 2, '2024-07-24', NULL),
(12, 12, 5, '2025-04-02', NULL),
(13, 13, 6, '2024-12-01', NULL),
(14, 14, 1, '2025-03-29', NULL),
(15, 15, 4, '2025-05-30', NULL),
(16, 16, 2, '2024-10-18', NULL),
(17, 17, 3, '2024-08-09', NULL),
(18, 18, 2, '2025-05-29', NULL),
(19, 19, 6, '2025-01-24', NULL),
(20, 20, 3, '2025-01-05', NULL),
(21, 21, 2, '2025-01-04', NULL),
(22, 22, 4, '2025-05-21', NULL),
(23, 23, 1, '2025-01-01', NULL),
(24, 24, 4, '2024-09-18', NULL),
(25, 25, 1, '2024-09-09', NULL),
(26, 26, 4, '2025-03-31', NULL),
(27, 27, 3, '2024-06-29', NULL),
(28, 28, 4, '2025-02-19', NULL),
(29, 29, 3, '2025-02-04', NULL),
(30, 30, 3, '2025-02-22', NULL);


INSERT INTO SMSRecord (sms_id, subscription_id, sms_time, receiver_number, sms_length) VALUES
(1, 13, '2025-03-20 05:17:59', '19422206588', 93),
(2, 14, '2025-04-03 09:58:09', '194029321122125', 85),
(3, 13, '2025-04-30 16:16:42', '46920404975562', 142),
(4, 17, '2025-05-20 08:36:27', '156369218658750', 155),
(5, 18, '2025-01-19 14:14:01', '2736260974', 109),
(6, 17, '2025-03-23 21:01:16', '8360472097', 139),
(7, 9, '2025-03-01 09:54:54', '6709544733', 104),
(8, 19, '2025-02-26 09:59:49', '187818133837391', 102),
(9, 24, '2025-04-20 04:27:02', '9247880955827', 39),
(10, 13, '2025-04-28 20:47:00', '6525531826', 42),
(11, 21, '2025-02-15 20:38:46', '61173191108492', 148),
(12, 25, '2025-05-20 16:33:18', '238468862997801', 51),
(13, 27, '2025-03-23 07:27:39', '12736832682156', 137),
(14, 29, '2025-05-24 01:15:33', '489760706240174', 51),
(15, 25, '2025-01-27 19:51:49', '6448790284719', 111),
(16, 7, '2025-01-03 09:16:18', '464212289913151', 150),
(17, 17, '2025-03-07 18:56:43', '8716962330', 69),
(18, 6, '2025-04-18 21:59:51', '8884299677320', 26),
(19, 27, '2025-01-30 17:35:27', '3783893590589', 56),
(20, 3, '2025-02-11 15:53:28', '12259697565', 117),
(21, 13, '2025-03-16 22:12:59', '713526775545931', 159),
(22, 24, '2025-02-13 14:34:56', '0684560344', 140),
(23, 22, '2025-01-05 03:37:05', '6130880814027', 71),
(24, 22, '2025-05-06 15:16:11', '16670822665202', 116),
(25, 18, '2025-05-08 15:33:39', '3521781296', 48),
(26, 9, '2025-05-24 19:00:12', '30157689482647', 59),
(27, 28, '2025-02-26 20:57:11', '12887652846608', 150),
(28, 2, '2025-02-08 10:25:53', '0776563453', 72),
(29, 16, '2025-01-03 11:25:18', '857462597251158', 101),
(30, 22, '2025-02-16 17:14:08', '9006064836', 99),
(31, 7, '2025-01-21 02:18:49', '7270478005', 24),
(32, 20, '2025-03-13 00:26:00', '5448053746', 115),
(33, 2, '2025-04-15 19:01:03', '11095848759733', 23),
(34, 13, '2025-05-27 23:26:35', '8072597376', 42),
(35, 15, '2025-04-30 04:50:56', '8347100497', 28),
(36, 19, '2025-02-11 16:21:39', '40086674748776', 119),
(37, 18, '2025-05-08 13:11:24', '248173880670458', 37),
(38, 19, '2025-05-05 19:32:14', '5529383456', 116),
(39, 4, '2025-05-09 00:47:26', '9298020265', 93),
(40, 11, '2025-06-03 14:18:16', '88788692471383', 86),
(41, 17, '2025-02-25 00:22:56', '441687924498717', 100),
(42, 19, '2025-02-21 22:38:07', '1918898921769681', 103),
(43, 10, '2025-05-01 05:40:38', '1614630005', 155),
(44, 1, '2025-04-29 22:35:05', '4331372142', 53),
(45, 11, '2025-04-08 05:28:24', '196773486954645', 90),
(46, 30, '2025-02-12 11:18:52', '9431998480', 155),
(47, 8, '2025-05-21 18:44:02', '6445045493', 28),
(48, 29, '2025-01-19 12:11:11', '19732655285', 30),
(49, 6, '2025-05-21 17:29:50', '1883060604485906', 70),
(50, 14, '2025-05-22 01:16:37', '5247692086', 20),
(51, 11, '2025-03-10 12:44:57', '6936716311', 142),
(52, 12, '2025-01-01 17:07:08', '0943880669051', 82),
(53, 25, '2025-02-15 22:25:59', '9193639338', 111),
(54, 7, '2025-01-04 11:10:55', '14776537787', 13),
(55, 14, '2025-04-17 17:05:10', '469071794431577', 89),
(56, 24, '2025-02-03 04:31:53', '16645038640266', 58),
(57, 17, '2025-01-04 01:24:57', '3992305944', 137),
(58, 10, '2025-01-08 01:14:02', '2217361291870', 154),
(59, 27, '2025-03-30 10:20:22', '900065297799659', 134),
(60, 20, '2025-05-12 12:42:46', '19624731408', 99);

-- CallRecord Table Data (60 records)
INSERT INTO CallRecord (call_id, subscription_id, call_time, duration, receiver_number, location_id) VALUES
(1, 13, '2025-03-20 05:17:59', 342, '19422206588', 5),
(2, 14, '2025-04-03 09:58:09', 215, '194029321122125', 12),
(3, 13, '2025-04-30 16:16:42', 543, '46920404975562', 5),
(4, 17, '2025-05-20 08:36:27', 127, '156369218658750', 8),
(5, 18, '2025-01-19 14:14:01', 89, '2736260974', 15),
(6, 17, '2025-03-23 21:01:16', 456, '8360472097', 8),
(7, 9, '2025-03-01 09:54:54', 321, '6709544733', 3),
(8, 19, '2025-02-26 09:59:49', 278, '187818133837391', 10),
(9, 24, '2025-04-20 04:27:02', 67, '9247880955827', 14),
(10, 13, '2025-04-28 20:47:00', 432, '6525531826', 5),
(11, 21, '2025-02-15 20:38:46', 189, '61173191108492', 11),
(12, 25, '2025-05-20 16:33:18', 76, '238468862997801', 16),
(13, 27, '2025-03-23 07:27:39', 512, '12736832682156', 7),
(14, 29, '2025-05-24 01:15:33', 98, '489760706240174', 9),
(15, 25, '2025-01-27 19:51:49', 234, '6448790284719', 16),
(16, 7, '2025-01-03 09:16:18', 178, '464212289913151', 2),
(17, 17, '2025-03-07 18:56:43', 321, '8716962330', 8),
(18, 6, '2025-04-18 21:59:51', 45, '8884299677320', 1),
(19, 27, '2025-01-30 17:35:27', 267, '3783893590589', 7),
(20, 3, '2025-02-11 15:53:28', 156, '12259697565', 4),
(21, 13, '2025-03-16 22:12:59', 432, '713526775545931', 5),
(22, 24, '2025-02-13 14:34:56', 189, '0684560344', 14),
(23, 22, '2025-01-05 03:37:05', 76, '6130880814027', 13),
(24, 22, '2025-05-06 15:16:11', 512, '16670822665202', 13),
(25, 18, '2025-05-08 15:33:39', 98, '3521781296', 15),
(26, 9, '2025-05-24 19:00:12', 234, '30157689482647', 3),
(27, 28, '2025-02-26 20:57:11', 178, '12887652846608', 18),
(28, 2, '2025-02-08 10:25:53', 321, '0776563453', 6),
(29, 16, '2025-01-03 11:25:18', 45, '857462597251158', 17),
(30, 22, '2025-02-16 17:14:08', 267, '9006064836', 13),
(31, 7, '2025-01-21 02:18:49', 156, '7270478005', 2),
(32, 20, '2025-03-13 00:26:00', 432, '5448053746', 20),
(33, 2, '2025-04-15 19:01:03', 189, '11095848759733', 6),
(34, 13, '2025-05-27 23:26:35', 76, '8072597376', 5),
(35, 15, '2025-04-30 04:50:56', 512, '8347100497', 19),
(36, 19, '2025-02-11 16:21:39', 98, '40086674748776', 10),
(37, 18, '2025-05-08 13:11:24', 234, '248173880670458', 15),
(38, 19, '2025-05-05 19:32:14', 178, '5529383456', 10),
(39, 4, '2025-05-09 00:47:26', 321, '9298020265', 22),
(40, 11, '2025-06-03 14:18:16', 45, '88788692471383', 21),
(41, 17, '2025-02-25 00:22:56', 267, '441687924498717', 8),
(42, 19, '2025-02-21 22:38:07', 156, '1918898921769681', 10),
(43, 10, '2025-05-01 05:40:38', 432, '1614630005', 23),
(44, 1, '2025-04-29 22:35:05', 189, '4331372142', 24),
(45, 11, '2025-04-08 05:28:24', 76, '196773486954645', 21),
(46, 30, '2025-02-12 11:18:52', 512, '9431998480', 30),
(47, 8, '2025-05-21 18:44:02', 98, '6445045493', 25),
(48, 29, '2025-01-19 12:11:11', 234, '19732655285', 9),
(49, 6, '2025-05-21 17:29:50', 178, '1883060604485906', 1),
(50, 14, '2025-05-22 01:16:37', 321, '5247692086', 12),
(51, 11, '2025-03-10 12:44:57', 45, '6936716311', 21),
(52, 12, '2025-01-01 17:07:08', 267, '0943880669051', 26),
(53, 25, '2025-02-15 22:25:59', 156, '9193639338', 16),
(54, 7, '2025-01-04 11:10:55', 432, '14776537787', 2),
(55, 14, '2025-04-17 17:05:10', 189, '469071794431577', 12),
(56, 24, '2025-02-03 04:31:53', 76, '16645038640266', 14),
(57, 17, '2025-01-04 01:24:57', 512, '3992305944', 8),
(58, 10, '2025-01-08 01:14:02', 98, '2217361291870', 23),
(59, 27, '2025-03-30 10:20:22', 234, '900065297799659', 7),
(60, 20, '2025-05-12 12:42:46', 178, '19624731408', 20);

-- DataUsage Table Data (60 records)
INSERT INTO DataUsage (usage_id, subscription_id, session_start, session_end, data_mb, location_id) VALUES
(1, 13, '2025-03-20 05:17:59', '2025-03-20 06:17:59', 256.75, 5),
(2, 14, '2025-04-03 09:58:09', '2025-04-03 10:58:09', 189.50, 12),
(3, 13, '2025-04-30 16:16:42', '2025-04-30 17:16:42', 512.25, 5),
(4, 17, '2025-05-20 08:36:27', '2025-05-20 09:36:27', 1024.00, 8),
(5, 18, '2025-01-19 14:14:01', '2025-01-19 15:14:01', 128.75, 15),
(6, 17, '2025-03-23 21:01:16', '2025-03-23 22:01:16', 768.50, 8),
(7, 9, '2025-03-01 09:54:54', '2025-03-01 10:54:54', 384.25, 3),
(8, 19, '2025-02-26 09:59:49', '2025-02-26 10:59:49', 256.00, 10),
(9, 24, '2025-04-20 04:27:02', '2025-04-20 05:27:02', 512.75, 14),
(10, 13, '2025-04-28 20:47:00', '2025-04-28 21:47:00', 1024.50, 5),
(11, 21, '2025-02-15 20:38:46', '2025-02-15 21:38:46', 128.25, 11),
(12, 25, '2025-05-20 16:33:18', '2025-05-20 17:33:18', 768.00, 16),
(13, 27, '2025-03-23 07:27:39', '2025-03-23 08:27:39', 384.75, 7),
(14, 29, '2025-05-24 01:15:33', '2025-05-24 02:15:33', 256.50, 9),
(15, 25, '2025-01-27 19:51:49', '2025-01-27 20:51:49', 512.25, 16),
(16, 7, '2025-01-03 09:16:18', '2025-01-03 10:16:18', 1024.00, 2),
(17, 17, '2025-03-07 18:56:43', '2025-03-07 19:56:43', 128.75, 8),
(18, 6, '2025-04-18 21:59:51', '2025-04-18 22:59:51', 768.50, 1),
(19, 27, '2025-01-30 17:35:27', '2025-01-30 18:35:27', 384.25, 7),
(20, 3, '2025-02-11 15:53:28', '2025-02-11 16:53:28', 256.00, 4),
(21, 13, '2025-03-16 22:12:59', '2025-03-16 23:12:59', 512.75, 5),
(22, 24, '2025-02-13 14:34:56', '2025-02-13 15:34:56', 1024.50, 14),
(23, 22, '2025-01-05 03:37:05', '2025-01-05 04:37:05', 128.25, 13),
(24, 22, '2025-05-06 15:16:11', '2025-05-06 16:16:11', 768.00, 13),
(25, 18, '2025-05-08 15:33:39', '2025-05-08 16:33:39', 384.75, 15),
(26, 9, '2025-05-24 19:00:12', '2025-05-24 20:00:12', 256.50, 3),
(27, 28, '2025-02-26 20:57:11', '2025-02-26 21:57:11', 512.25, 18),
(28, 2, '2025-02-08 10:25:53', '2025-02-08 11:25:53', 1024.00, 6),
(29, 16, '2025-01-03 11:25:18', '2025-01-03 12:25:18', 128.75, 17),
(30, 22, '2025-02-16 17:14:08', '2025-02-16 18:14:08', 768.50, 13),
(31, 7, '2025-01-21 02:18:49', '2025-01-21 03:18:49', 384.25, 2),
(32, 20, '2025-03-13 00:26:00', '2025-03-13 01:26:00', 256.00, 20),
(33, 2, '2025-04-15 19:01:03', '2025-04-15 20:01:03', 512.75, 6),
(34, 13, '2025-05-27 23:26:35', '2025-05-28 00:26:35', 1024.50, 5),
(35, 15, '2025-04-30 04:50:56', '2025-04-30 05:50:56', 128.25, 19),
(36, 19, '2025-02-11 16:21:39', '2025-02-11 17:21:39', 768.00, 10),
(37, 18, '2025-05-08 13:11:24', '2025-05-08 14:11:24', 384.75, 15),
(38, 19, '2025-05-05 19:32:14', '2025-05-05 20:32:14', 256.50, 10),
(39, 4, '2025-05-09 00:47:26', '2025-05-09 01:47:26', 512.25, 22),
(40, 11, '2025-06-03 14:18:16', '2025-06-03 15:18:16', 1024.00, 21),
(41, 17, '2025-02-25 00:22:56', '2025-02-25 01:22:56', 128.75, 8),
(42, 19, '2025-02-21 22:38:07', '2025-02-21 23:38:07', 768.50, 10),
(43, 10, '2025-05-01 05:40:38', '2025-05-01 06:40:38', 384.25, 23),
(44, 1, '2025-04-29 22:35:05', '2025-04-29 23:35:05', 256.00, 24),
(45, 11, '2025-04-08 05:28:24', '2025-04-08 06:28:24', 512.75, 21),
(46, 30, '2025-02-12 11:18:52', '2025-02-12 12:18:52', 1024.50, 30),
(47, 8, '2025-05-21 18:44:02', '2025-05-21 19:44:02', 128.25, 25),
(48, 29, '2025-01-19 12:11:11', '2025-01-19 13:11:11', 768.00, 9),
(49, 6, '2025-05-21 17:29:50', '2025-05-21 18:29:50', 384.75, 1),
(50, 14, '2025-05-22 01:16:37', '2025-05-22 02:16:37', 256.50, 12),
(51, 11, '2025-03-10 12:44:57', '2025-03-10 13:44:57', 512.25, 21),
(52, 12, '2025-01-01 17:07:08', '2025-01-01 18:07:08', 1024.00, 26),
(53, 25, '2025-02-15 22:25:59', '2025-02-15 23:25:59', 128.75, 16),
(54, 7, '2025-01-04 11:10:55', '2025-01-04 12:10:55', 768.50, 2),
(55, 14, '2025-04-17 17:05:10', '2025-04-17 18:05:10', 384.25, 12),
(56, 24, '2025-02-03 04:31:53', '2025-02-03 05:31:53', 256.00, 14),
(57, 17, '2025-01-04 01:24:57', '2025-01-04 02:24:57', 512.75, 8),
(58, 10, '2025-01-08 01:14:02', '2025-01-08 02:14:02', 1024.50, 23),
(59, 27, '2025-03-30 10:20:22', '2025-03-30 11:20:22', 128.25, 7),
(60, 20, '2025-05-12 12:42:46', '2025-05-12 13:42:46', 768.00, 20);

-- Billing Table Data (60 records)
INSERT INTO Billing (bill_id, subscription_id, billing_month, billing_amount, payment_status) VALUES
(1, 13, '2025-01-01', 999.00, 'Paid'),
(2, 14, '2025-01-01', 99.00, 'Paid'),
(3, 13, '2025-02-01', 999.00, 'Paid'),
(4, 17, '2025-02-01', 399.00, 'Paid'),
(5, 18, '2025-02-01', 199.00, 'Paid'),
(6, 17, '2025-03-01', 399.00, 'Paid'),
(7, 9, '2025-03-01', 999.00, 'Paid'),
(8, 19, '2025-03-01', 999.00, 'Paid'),
(9, 24, '2025-03-01', 799.00, 'Paid'),
(10, 13, '2025-04-01', 999.00, 'Paid'),
(11, 21, '2025-04-01', 199.00, 'Paid'),
(12, 25, '2025-04-01', 99.00, 'Paid'),
(13, 27, '2025-04-01', 399.00, 'Paid'),
(14, 29, '2025-04-01', 399.00, 'Paid'),
(15, 25, '2025-05-01', 99.00, 'Paid'),
(16, 7, '2025-05-01', 149.00, 'Paid'),
(17, 17, '2025-05-01', 399.00, 'Paid'),
(18, 6, '2025-05-01', 799.00, 'Paid'),
(19, 27, '2025-05-01', 399.00, 'Paid'),
(20, 3, '2025-05-01', 199.00, 'Paid'),
(21, 13, '2025-06-01', 999.00, 'Unpaid'),
(22, 24, '2025-06-01', 799.00, 'Unpaid'),
(23, 22, '2025-06-01', 799.00, 'Unpaid'),
(24, 22, '2025-06-01', 799.00, 'Unpaid'),
(25, 18, '2025-06-01', 199.00, 'Unpaid'),
(26, 9, '2025-06-01', 999.00, 'Unpaid'),
(27, 28, '2025-06-01', 799.00, 'Unpaid'),
(28, 2, '2025-06-01', 999.00, 'Unpaid'),
(29, 16, '2025-06-01', 199.00, 'Unpaid'),
(30, 22, '2025-06-01', 799.00, 'Unpaid'),
(31, 7, '2025-06-01', 149.00, 'Unpaid'),
(32, 20, '2025-06-01', 399.00, 'Unpaid'),
(33, 2, '2025-06-01', 999.00, 'Unpaid'),
(34, 13, '2025-06-01', 999.00, 'Unpaid'),
(35, 15, '2025-06-01', 799.00, 'Unpaid'),
(36, 19, '2025-06-01', 999.00, 'Unpaid'),
(37, 18, '2025-06-01', 199.00, 'Unpaid'),
(38, 19, '2025-06-01', 999.00, 'Unpaid'),
(39, 4, '2025-06-01', 199.00, 'Unpaid'),
(40, 11, '2025-06-01', 199.00, 'Unpaid'),
(41, 17, '2025-06-01', 399.00, 'Unpaid'),
(42, 19, '2025-06-01', 999.00, 'Unpaid'),
(43, 10, '2025-06-01', 149.00, 'Unpaid'),
(44, 1, '2025-06-01', 149.00, 'Unpaid'),
(45, 11, '2025-06-01', 199.00, 'Unpaid'),
(46, 30, '2025-06-01', 399.00, 'Unpaid'),
(47, 8, '2025-06-01', 999.00, 'Unpaid'),
(48, 29, '2025-06-01', 399.00, 'Unpaid'),
(49, 6, '2025-06-01', 799.00, 'Unpaid'),
(50, 14, '2025-06-01', 99.00, 'Unpaid'),
(51, 11, '2025-06-01', 199.00, 'Unpaid'),
(52, 12, '2025-06-01', 149.00, 'Unpaid'),
(53, 25, '2025-06-01', 99.00, 'Unpaid'),
(54, 7, '2025-06-01', 149.00, 'Unpaid'),
(55, 14, '2025-06-01', 99.00, 'Unpaid'),
(56, 24, '2025-06-01', 799.00, 'Unpaid'),
(57, 17, '2025-06-01', 399.00, 'Unpaid'),
(58, 10, '2025-06-01', 149.00, 'Unpaid'),
(59, 27, '2025-06-01', 399.00, 'Unpaid'),
(60, 20, '2025-06-01', 399.00, 'Unpaid');

-- CustomerSupport Table Data (30 records)
INSERT INTO CustomerSupport (ticket_id, customer_id, issue_date, issue_description, support_status) VALUES
(1, 13, '2025-01-15 09:23:45', 'Network connectivity issues in Delhi area', 'Closed'),
(2, 14, '2025-01-18 14:12:33', 'Billing discrepancy for January', 'Closed'),
(3, 13, '2025-02-02 10:45:21', 'SMS not being delivered', 'Closed'),
(4, 17, '2025-02-15 16:23:54', 'Request to change plan', 'Closed'),
(5, 18, '2025-02-20 11:34:12', 'International roaming not working', 'Closed'),
(6, 17, '2025-03-05 13:45:32', 'Data speed very slow', 'Closed'),
(7, 9, '2025-03-12 09:12:43', 'Device compatibility issue', 'Closed'),
(8, 19, '2025-03-18 15:23:54', 'Request for duplicate bill', 'Closed'),
(9, 24, '2025-03-22 10:34:21', 'Network coverage complaint', 'Closed'),
(10, 13, '2025-04-01 14:45:32', 'Payment not reflecting', 'Closed'),
(11, 21, '2025-04-05 11:23:43', 'Call drops in Bangalore', 'Closed'),
(12, 25, '2025-04-10 16:34:12', 'Plan upgrade request', 'Closed'),
(13, 27, '2025-04-15 09:45:23', 'International calling not working', 'Closed'),
(14, 29, '2025-04-20 14:12:34', 'Data usage discrepancy', 'Closed'),
(15, 25, '2025-05-02 10:23:45', 'Request for new SIM card', 'Closed'),
(16, 7, '2025-05-08 15:34:56', 'Activation of new service', 'Closed'),
(17, 17, '2025-05-12 11:45:12', 'Complaint about call quality', 'Closed'),
(18, 6, '2025-05-18 16:12:23', 'Billing query', 'Closed'),
(19, 27, '2025-05-22 10:23:34', 'Request to port number', 'Closed'),
(20, 3, '2025-05-25 14:34:45', 'Device not connecting to network', 'Closed'),
(21, 13, '2025-06-01 09:45:56', 'Recent bill seems incorrect', 'Open'),
(22, 24, '2025-06-03 15:12:12', 'No network in Pune area', 'Open'),
(23, 22, '2025-06-05 11:23:23', 'Request for family plan', 'In Progress'),
(24, 22, '2025-06-07 16:34:34', 'International roaming activation', 'In Progress'),
(25, 18, '2025-06-09 10:45:45', 'Data pack not activated', 'Open'),
(26, 9, '2025-06-10 14:12:56', 'Device upgrade request', 'In Progress'),
(27, 28, '2025-06-12 09:23:12', 'Network issues in Mumbai', 'Open'),
(28, 2, '2025-06-13 15:34:23', 'Corporate plan inquiry', 'In Progress'),
(29, 16, '2025-06-15 11:45:34', 'Billing dispute', 'Open'),
(30, 22, '2025-06-18 16:12:45', 'Request for call detail records', 'In Progress');

-- Device Table Data (30 records - one per customer)
INSERT INTO Device (device_id, customer_id, device_model, imei_number, registered_date, location_id) VALUES
(1, 1, 'iPhone 15 Pro', '354678901234567', '2024-12-06', 24),
(2, 2, 'Samsung Galaxy S24', '357890123456789', '2025-04-08', 6),
(3, 3, 'OnePlus 12', '456789012345678', '2024-11-08', 4),
(4, 4, 'Xiaomi 14', '567890123456789', '2024-06-27', 22),
(5, 5, 'Google Pixel 8 Pro', '678901234567890', '2024-08-31', 27),
(6, 6, 'iPhone 14', '789012345678901', '2024-12-26', 1),
(7, 7, 'Samsung Galaxy A54', '890123456789012', '2024-10-15', 2),
(8, 8, 'OnePlus Nord 3', '901234567890123', '2025-01-31', 25),
(9, 9, 'iPhone 13', '012345678901234', '2025-05-23', 3),
(10, 10, 'Samsung Galaxy S23 FE', '123456789012345', '2024-06-25', 23),
(11, 11, 'Nothing Phone 2', '234567890123456', '2024-07-24', 21),
(12, 12, 'Motorola Edge 40', '345678901234567', '2025-04-02', 26),
(13, 13, 'iPhone 15 Pro Max', '456788012345678', '2024-12-01', 5),
(14, 14, 'Samsung Galaxy M34', '567890223456789', '2025-03-29', 12),
(15, 15, 'OnePlus 11R', '678911234567890', '2025-05-30', 19),
(16, 16, 'Xiaomi 13T Pro', '789012345678001', '2024-10-18', 17),
(17, 17, 'Google Pixel 7a', '890113456789012', '2024-08-09', 8),
(18, 18, 'iPhone 12', '901234667890123', '2025-05-29', 15),
(19, 19, 'Samsung Galaxy Z Flip5', '012345778901234', '2025-01-24', 10),
(20, 20, 'OnePlus 10 Pro', '123456889012345', '2025-01-05', 20),
(21, 21, 'Vivo V29 Pro', '234667890123456', '2025-01-04', 11),
(22, 22, 'iPhone 14 Plus', '345678900234567', '2025-05-21', 13),
(23, 23, 'Samsung Galaxy S22', '45678901239978', '2025-01-01', 28),
(24, 24, 'OnePlus Nord CE 3', '567890023456789', '2024-09-18', 14),
(25, 25, 'Xiaomi Redmi Note 12 Pro', '678900234567890', '2024-09-09', 16),
(26, 26, 'Google Pixel 6a', '789002345678901', '2025-03-31', 29),
(27, 27, 'iPhone SE 2023', '890223456789012', '2024-06-29', 7),
(28, 28, 'Samsung Galaxy A34', '901244567890123', '2025-02-19', 18),
(29, 29, 'OnePlus Nord 2T', '010345678901234', '2025-02-04', 9),
(30, 30, 'Xiaomi 12 Pro', '123456799012345', '2025-02-22', 30);

-- Location Table Data (30 records - major Indian cities)
INSERT INTO Location (location_id, city, region, network_quality) VALUES
(1, 'Kochi', 'Kerala', 'Good'),
(2, 'Hyderabad', 'Telangana', 'Excellent'),
(3, 'Mumbai', 'Maharashtra', 'Excellent'),
(4, 'Ahmedabad', 'Gujarat', 'Good'),
(5, 'Delhi', 'Delhi', 'Excellent'),
(6, 'Pune', 'Maharashtra', 'Good'),
(7, 'Chennai', 'Tamil Nadu', 'Good'),
(8, 'Agra', 'Uttar Pradesh', 'Fair'),
(9, 'Lucknow', 'Uttar Pradesh', 'Good'),
(10, 'Gurgaon', 'Haryana', 'Excellent'),
(11, 'Faridabad', 'Haryana', 'Fair'),
(12, 'Delhi', 'Delhi', 'Excellent'),
(13, 'Vadodara', 'Gujarat', 'Good'),
(14, 'Pune', 'Maharashtra', 'Good'),
(15, 'Mumbai', 'Maharashtra', 'Excellent'),
(16, 'Bangalore', 'Karnataka', 'Excellent'),
(17, 'Bangalore', 'Karnataka', 'Excellent'),
(18, 'Mumbai', 'Maharashtra', 'Excellent'),
(19, 'Kolkata', 'West Bengal', 'Good'),
(20, 'Kolkata', 'West Bengal', 'Good'),
(21, 'Jaipur', 'Rajasthan', 'Good'),
(22, 'Indore', 'Madhya Pradesh', 'Fair'),
(23, 'Bhopal', 'Madhya Pradesh', 'Good'),
(24, 'Chandigarh', 'Punjab', 'Excellent'),
(25, 'Nagpur', 'Maharashtra', 'Good'),
(26, 'Coimbatore', 'Tamil Nadu', 'Good'),
(27, 'Visakhapatnam', 'Andhra Pradesh', 'Fair'),
(28, 'Patna', 'Bihar', 'Fair'),
(29, 'Thiruvananthapuram', 'Kerala', 'Good'),
(30, 'Goa', 'Goa', 'Excellent');


SELECT 
    c.customer_id, 
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    c.email, 
    c.phone,
    sp.plan_name,
    sp.plan_type,
    sp.monthly_fee
FROM 
    Customer c
JOIN 
    Subscription s ON c.customer_id = s.customer_id
JOIN 
    ServicePlan sp ON s.plan_id = sp.plan_id
WHERE 
    s.end_date IS NULL;
    
SELECT 
    sp.plan_id,
    sp.plan_name,
    sp.plan_type,
    COUNT(s.subscription_id) AS active_subscriptions,
    SUM(sp.monthly_fee) AS monthly_revenue
FROM 
    ServicePlan sp
LEFT JOIN 
    Subscription s ON sp.plan_id = s.plan_id AND s.end_date IS NULL
GROUP BY 
    sp.plan_id, sp.plan_name, sp.plan_type
ORDER BY 
    active_subscriptions DESC;
    
    
SELECT 
    HOUR(call_time) AS hour_of_day,
    COUNT(*) AS total_calls,
    AVG(duration) AS avg_duration,
    SUM(duration) AS total_minutes
FROM 
    CallRecord
GROUP BY 
    HOUR(call_time)
ORDER BY 
    hour_of_day;
    
SELECT 
    c.customer_id,
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    sp.plan_name,
    SUM(du.data_mb) AS total_data_used_mb,
    ROUND(SUM(du.data_mb) / sp.data_limit * 100, 2) AS percentage_of_limit
FROM 
    DataUsage du
JOIN 
    Subscription s ON du.subscription_id = s.subscription_id
JOIN 
    Customer c ON s.customer_id = c.customer_id
JOIN 
    ServicePlan sp ON s.plan_id = sp.plan_id
WHERE 
    du.session_start BETWEEN DATE_SUB(CURDATE(), INTERVAL 30 DAY) AND CURDATE()
GROUP BY 
    c.customer_id, c.first_name, c.last_name, sp.plan_name, sp.data_limit
ORDER BY 
    total_data_used_mb DESC
LIMIT 10;

        
        SELECT c.customer_id, CONCAT(c.first_name, ' ', c.last_name) AS full_name,
               SUM(b.billing_amount) AS total_spent
        FROM Customer c
        JOIN Subscription s ON c.customer_id = s.customer_id
        JOIN Billing b ON s.subscription_id = b.subscription_id
        GROUP BY c.customer_id
        HAVING total_spent > 2000
        ORDER BY total_spent DESC;
        
 
 
 
DELIMITER //

CREATE PROCEDURE GetCustomerBillingSummary(IN cust_id INT)
BEGIN
    SELECT b.billing_month, b.billing_amount, b.payment_status
    FROM Billing b
    JOIN Subscription s ON b.subscription_id = s.subscription_id
    WHERE s.customer_id = cust_id;
END //

DELIMITER ;


     
     
DELIMITER //

CREATE PROCEDURE ListSubscriptionsByPlanType(IN type ENUM('Prepaid', 'Postpaid'))
BEGIN
    SELECT c.customer_id, CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
           sp.plan_name, sp.plan_type
    FROM Customer c
    JOIN Subscription s ON c.customer_id = s.customer_id
    JOIN ServicePlan sp ON s.plan_id = sp.plan_id
    WHERE sp.plan_type = type;
END //

DELIMITER ;

DELIMITER //

CREATE FUNCTION GetSMSCount(sub_id INT)
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE sms_count INT;
    SELECT COUNT(*) INTO sms_count
    FROM SMSRecord
    WHERE subscription_id = sub_id;
    RETURN sms_count;
END //

DELIMITER ;

CALL GetCustomerBillingSummary(8);

-- For Prepaid plans
CALL ListSubscriptionsByPlanType('Prepaid');

-- For Postpaid plans
CALL ListSubscriptionsByPlanType('Postpaid');

SELECT GetSMSCount(3) AS sms_count;

SELECT s.subscription_id, GetSMSCount(s.subscription_id) AS sms_count
FROM Subscription s
WHERE s.customer_id = 12;
