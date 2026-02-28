# Multi-Region Azure Infrastructure Project

## Overview
This project demonstrates a multi-region, highly available Azure infrastructure with Virtual Networks, Linux-based Virtual Machines, Application Gateway, Traffic Manager, and Azure Storage integration. It deploys a Python web application with separate home and upload pages, using Azure Storage for uploaded files and proper routing for errors.

---

## Architecture

- **Virtual Networks:** `vnet1` and `vnet2` deployed in different Azure regions.
- **Virtual Machines:** 
  - `vm1` hosts the **Upload Page** (`/upload`)
  - `vm2` hosts the **Default Home Page** (`/`)
- **Operating System:** Linux installed on both VMs.
- **Application Deployment:**
  - Cloned project from GitHub.
  - Executed scripts: `vm1.sh` and `vm2.sh` to initialize applications.
  - Error pages `403` and `502` configured.
- **Storage Integration:**
  - Static web files hosted in **Azure Storage Account**
  - Container name: `upload`
  - Uploads from VM1 saved in this container
  - Configuration file in VM1 updated with storage account details

---

## Routing

- **Home Page:** `https://example.com/` → VM2 default page  
- **Upload Page:** `https://example.com/upload` → VM1 upload page  

Azure Application Gateway handles **path-based routing**, and Traffic Manager provides global distribution.

---

## Deployment Steps

1. Deploy VNets (`vnet1` & `vnet2`) in Azure Portal.
2. Deploy VMs (`vm1` & `vm2`) in respective VNets.
3. Install Linux on both VMs.
4. Clone the GitHub repository on both VMs.
5. Run initialization scripts:
    ```bash
    ./vm1.sh
    ./vm2.sh
    ```
6. Edit configuration file on **VM1** to add Azure Storage account details (container `upload`).
7. Start Python application on VM1:
    ```bash
    python3 app.py
    ```
8. Configure Azure Application Gateway:
    - Path `/upload` → VM1
    - Path `/` → VM2
9. Set up Traffic Manager for multi-region distribution.
10. Verify uploaded files are saved to Azure Storage container `upload`.

---

## Key Features

- Multi-region deployment for high availability
- Path-based routing via Azure Application Gateway
- Global traffic distribution with Traffic Manager
- Home page on VM2 (`/`) and Upload page on VM1 (`/upload`)
- Error pages `403` and `502` configured
- File uploads saved to Azure Storage container

---

## Technologies Used

- **Cloud Platform:** Microsoft Azure
- **Compute:** Virtual Machines (Linux)
- **Networking:** Virtual Networks, Application Gateway, Traffic Manager
- **Backend:** Python
- **Storage:** Azure Storage (`upload` container)
- **Version Control:** GitHub
