# Clinic Management System

A desktop application developed in C# using .NET Framework, offering a user-friendly interface for efficient management of a clinic.
This comprehensive clinic management system allows you to efficiently manage patient records, doctor information, appointments, medical records, prescriptions, and payments.
It follows a three-tier architecture consisting of the Data Access Layer, Business Layer, and Presentation Layer for maintainability and scalability.

## 🐧 Linux-Specific Notes

- This application was originally designed for Windows using .NET Framework. Running it on Linux requires either Mono or Wine.
- For best performance, consider using Wine for the GUI components.
- The database can be either MariaDB (recommended for Linux) or SQL Server for Linux.
- Make sure to configure your desktop environment to handle Windows Forms applications properly.

## ⚡ Prerequisites For Linux

### Arch Linux

You'll need to install the following packages:

```bash
# Install .NET SDK and runtime
sudo pacman -S dotnet-sdk dotnet-runtime

# Install Mono (for .NET Framework compatibility)
sudo pacman -S mono mono-msbuild

# Install SQL Server alternative (MariaDB/MySQL)
sudo pacman -S mariadb mariadb-clients
# OR for MySQL
sudo pacman -S mysql mysql-clients

# Install optional GUI tools
sudo pacman -S dbeaver    # Database management tool
```

You can also install SQL Server for Linux if preferred:
```bash
# Enable AUR if not already enabled
sudo pacman -S --needed base-devel git
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
# Install SQL Server via AUR
paru -S mssql-server
```

## 🚀 Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/HananeAitBenYachou/Clinic-Management-System.git
   cd Clinic-Management-System
   ```

2. **Database Setup**
   If using MariaDB:
   ```bash
   # Start MariaDB service
   sudo systemctl start mariadb
   sudo systemctl enable mariadb
   
   # Secure the installation
   sudo mysql_secure_installation
   
   # Create database
   mysql -u root -p
   CREATE DATABASE ClinicDB;
   ```

   If using SQL Server:
   ```bash
   # Start SQL Server
   sudo systemctl start mssql-server
   sudo systemctl enable mssql-server
   
   # Configure SQL Server
   sudo /opt/mssql/bin/mssql-conf setup
   
   # Create database using sqlcmd
   sqlcmd -S localhost -U SA
   CREATE DATABASE ClinicDB;
   GO
   ```

3. **Configure Connection String**
   Open the `App.config` or `Web.config` file and update the connection string:

   For MariaDB:
   ```xml
   <connectionStrings>
     <add name="ClinicDBConnection" 
          connectionString="Server=localhost;Database=ClinicDB;User=root;Password=your_password;"
          providerName="MySql.Data.MySqlClient" />
   </connectionStrings>
   ```

   For SQL Server:
   ```xml
   <connectionStrings>
     <add name="ClinicDBConnection" 
          connectionString="Server=localhost;Database=ClinicDB;User=SA;Password=your_password;"
          providerName="System.Data.SqlClient" />
   </connectionStrings>
   ```

## 💻 Running the Application

1. **Build the Solution**
   ```bash
   # Navigate to solution directory
   cd /path/to/Clinic-Management-System
   
   # Restore packages
   nuget restore
   
   # Build solution
   msbuild /p:Configuration=Release
   ```

2. **Run the Application**
   ```bash
   # Using Mono
   mono bin/Release/ClinicManagementSystem.exe
   ```

   If you encounter any display issues, you can try:
   ```bash
   # Install Wine for better Windows Forms compatibility
   sudo pacman -S wine
   
   # Run through Wine
   wine bin/Release/ClinicManagementSystem.exe
   ```

## 🔧 Troubleshooting

### Common Issues on Linux:

1. **Font Issues**
   ```bash
   # Install Microsoft fonts
   yay -S ttf-ms-fonts
   ```

2. **Database Connection Issues**
   - Ensure the database service is running:
     ```bash
     sudo systemctl status mariadb    # For MariaDB
     # OR
     sudo systemctl status mssql-server    # For SQL Server
     ```
   - Check firewall settings:
     ```bash
     sudo ufw status    # If using UFW
     # OR
     sudo firewall-cmd --list-all    # If using firewalld
     ```

3. **Mono Runtime Issues**
   ```bash
   # Install additional Mono components
   sudo pacman -S mono-addins mono-tools
   ```
**==========================================================================**

## ⚡ Prerequisites for Windows
Before you begin, ensure you have the following installed:
- [Visual Studio](https://visualstudio.microsoft.com/downloads/) (2019 or later recommended)
- [.NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework/net472) or later
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (Express edition or higher)
- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)

## 🚀 Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/HananeAitBenYachou/Clinic-Management-System.git
   cd Clinic-Management-System
   ```

2. **Database Setup**
   - Open SQL Server Management Studio
   - Connect to your SQL Server instance
   - Create a new database named `ClinicDB` (or as specified in the connection string)
   - Run the database scripts provided in the `Database` folder (if available)

3. **Configure Connection String**
   - Open the solution in Visual Studio
   - Locate the `App.config` or `Web.config` file
   - Update the connection string with your SQL Server details:
   ```xml
   <connectionStrings>
     <add name="ClinicDBConnection" 
          connectionString="Server=YOUR_SERVER;Database=ClinicDB;Trusted_Connection=True;"
          providerName="System.Data.SqlClient" />
   </connectionStrings>
   ```

## 💻 Running the Application

1. **Open the Solution**
   - Launch Visual Studio
   - Open the solution file (`*.sln`)
   - Restore NuGet packages if prompted

2. **Build the Solution**
   - Right-click on the solution in Solution Explorer
   - Select "Build Solution" or press `Ctrl + Shift + B`

3. **Run the Application**
   - Press `F5` to run in debug mode
   - Or press `Ctrl + F5` to run without debugging

**==========================================================================**

## 🎯 Features

### 1. Patients

The system stores detailed information about patients. Each patient is assigned a unique identifier, and their profile includes their name, date of birth, gender, contact information (phone number, email), and address.

### 2. Doctors

The system maintains a comprehensive database of doctors. Each doctor is assigned a unique identifier, and their profile includes their name, specialization, date of birth, gender, contact information (phone number, email), and address.

### 3. Appointments

The system manages appointments effectively. Each appointment is assigned a unique identifier and includes the patient, doctor, appointment date and time, and appointment status. Appointment statuses include:
- Pending: The appointment has been scheduled but has not yet occurred.
- Confirmed: The appointment has been confirmed by both the patient and the healthcare provider.
- Completed: The appointment has taken place as scheduled.
- Canceled: The appointment has been canceled either by the patient or the healthcare provider.
- Rescheduled: The appointment has been rescheduled for a different date or time.
- No Show: The patient did not show up for the appointment without canceling or rescheduling.

### 4. Medical Records

The system maintains comprehensive medical records for patients. Each attended appointment is associated with a medical record. Each medical record is assigned a unique identifier and includes the patient, doctor, description of the visit, diagnosis, prescribed medication, and any additional notes.

### 5. Prescription

The system manages prescribed medications efficiently. For each medical record, there can be at most one prescription. Each prescription is assigned a unique identifier and includes the medical record, medication name, dosage, frequency, start date, end date, and any special instructions.

### 6. Payments

The system tracks payment information for appointments. Each payment is assigned a unique identifier and includes the patient, payment date, payment method, amount paid, and any additional notes. Payments are associated with individual appointments.

## Technology Used

The clinic management system is built using the following technologies:
- Programming Language: C#
- Framework: .NET Framework
- Database: Ms SQL Server
- Data Access: ADO.NET
- User Interface: WinForms
- Integrated Development Environment: Visual Studio

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the terms specified in the repository.

## 📞 Support

If you encounter any issues or have questions, please [open an issue](https://github.com/mohamadali-halwani/Clinic-Management-System/issues/new) on GitHub.
