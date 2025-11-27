# Vehicles-managment-system
🚗 Vehicle Management System — README
📌 Overview

The Vehicle Management System is a Java-based web application built using:

Servlets for backend logic

JSP for UI rendering

JDBC for database operations

MySQL (or any RDBMS)

This application allows users/admins to add, view, update, and delete vehicle records.

🛠️ Features

✔ Add new vehicles
✔ View all vehicles
✔ Update existing vehicle details
✔ Delete vehicle records
✔ Server-side validation
✔ Follows MVC architecture
✔ Clean separation between Servlet (Controller), JSP (View), and Database (Model)

📁 Project Structure
VehicleManagementSystem/
 ├── src/
 │    └── com.vms.controller/
 │           ├── AddVehicleServlet.java
 │           ├── ViewVehicleServlet.java
 │           ├── UpdateVehicleServlet.java
 │           └── DeleteVehicleServlet.java
 │
 │    └── com.vms.dao/
 │           └── VehicleDAO.java
 │
 │    └── com.vms.model/
 │           └── Vehicle.java
 │
 ├── WebContent/
 │    ├── index.jsp
 │    ├── addVehicle.jsp
 │    ├── viewVehicle.jsp
 │    ├── updateVehicle.jsp
 │    ├── error.jsp
 │    └── WEB-INF/
 │           └── web.xml
 │
 └── README.md

🧩 Tech Stack
Layer	Technology
Frontend	JSP, HTML, CSS
Backend	Java Servlets
Database	MySQL + JDBC
Server	Apache Tomcat 8/9/10
Architecture	MVC
🗂️ Database Structure
Table: vehicles
Column Name	Type	Description
id (PK)	INT AUTO_INCREMENT	Vehicle ID
name	VARCHAR(100)	Vehicle name
type	VARCHAR(50)	Car/Bike/Truck etc
number	VARCHAR(20)	Registration number
model	VARCHAR(50)	Model name
price	DOUBLE	Vehicle price
🔄 Application Flow (MVC)

User requests a page

JSP collects data → sends to Servlet

Servlet interacts with DAO

DAO performs SQL operations

Data returned to servlet

Servlet forwards to appropriate JSP

JSP displays the result

▶️ How to Run the Project
1. Import Project

Open Eclipse or IntelliJ

File → Import → Dynamic Web Project

2. Configure Database

Create table:

CREATE DATABASE vms;

USE vms;

CREATE TABLE vehicles(
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100),
  type VARCHAR(50),
  number VARCHAR(20),
  model VARCHAR(50),
  price DOUBLE
);


Update JDBC settings in VehicleDAO.java:

String url = "jdbc:mysql://localhost:3306/vms";
String user = "root";
String pass = "your_password";

3. Deploy on Tomcat

Add Tomcat server in IDE

Run project on server

4. Open Browser
http://localhost:8080/VehicleManagementSystem/

📄 Example Servlet (AddVehicleServlet)
public class AddVehicleServlet extends HttpServlet {
    protected void doPost(HttpServletRequest req, HttpServletResponse res)
            throws ServletException, IOException {

        String name = req.getParameter("name");
        String type = req.getParameter("type");
        String number = req.getParameter("number");
        String model = req.getParameter("model");
        double price = Double.parseDouble(req.getParameter("price"));

        Vehicle v = new Vehicle(name, type, number, model, price);

        VehicleDAO dao = new VehicleDAO();
        boolean status = dao.addVehicle(v);

        if(status)
            res.sendRedirect("viewVehicle");
        else
            res.sendRedirect("error.jsp");
    }
}

📚 Future Enhancements

🔹 Login system (Admin/User)
🔹 Vehicle image upload
🔹 Pagination in vehicle list
🔹 Search/Filter vehicles
🔹 REST API version
