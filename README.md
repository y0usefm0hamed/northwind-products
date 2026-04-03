# Northwind Products - SAP Fiori Application

A SAP Fiori Elements List Report application built using SAP Business Application Studio (BAS),
connected to the public Northwind OData service via an SAP BTP destination.
The app displays product data including ProductID, ProductName, UnitPrice, and UnitsInStock.

## Architecture Overview

- **SAP BTP Destination**: Configured in BTP Cockpit to point to the Northwind OData service
  (https://services.odata.org). This acts as a secure proxy so BAS can consume the external service.
- **SAP Business Application Studio (BAS)**: Used to scaffold and develop the Fiori Elements
  app using the Fiori generator wizard. BAS runs on Cloud Foundry and connects to the destination.
- **Cloud Foundry**: The runtime environment within SAP BTP where BAS dev spaces are hosted
  and where the application can be deployed.

## Setup Instructions

1. Log in to SAP BTP Cockpit and navigate to **Connectivity → Destinations**
2. Create a new destination:
   - Name: `Northwind`
   - URL: `https://services.odata.org`
   - Type: HTTP
   - Authentication: NoAuthentication
3. Launch **SAP Business Application Studio** from your BTP subscriptions
4. Create a new **Dev Space** of type **SAP Fiori** and wait for it to start
5. Open the project wizard → select **List Report Page** template
6. Set Data Source to **Connect to an OData Service**
7. Enter OData URL: `https://services.odata.org/V2/Northwind/Northwind.svc/`
8. Select **Products** as the Main Entity, Table Type: **Responsive**
9. Set namespace to `com.intern.northwindapp` and title to `Northwind Products`
10. Click Finish to generate the project
11. Add UI annotations in `webapp/annotations/annotations.xml` for the 4 columns
12. Run `npm start` to preview the application

## OData Entity Used

**Entity Set: Products**

The Products entity was selected because it contains several meaningful fields
(ProductID, ProductName, UnitPrice, UnitsInStock) that demonstrate a realistic
business use case — browsing and reviewing product inventory data.

## Challenges Faced

**Issue**: When entering the OData service URL in the Fiori generator, the relative path
`/V2/Northwind/Northwind.svc/` was rejected with "Invalid URL".

**Resolution**: The full absolute URL `https://services.odata.org/V2/Northwind/Northwind.svc/`
was required. Additionally, the generator showed a warning about missing backend annotations,
which was resolved by manually adding `UI.LineItem` annotations in `annotations.xml`.

## Bonus Tasks Completed

None attempted.

## Deployed Application URL

Not applicable (Bonus B1 not completed).

## Screenshots

### Deliverable 2 — Northwind Destination in BTP Cockpit
![BTP Destination](docs/D2.configured_Northwind_destination_in_BTP_Cockpit.png)

### Deliverable 3 — Application Running in BAS Preview
![App Preview](docs/D3.Application_running_in_BAS_Preview_showing_real_data.png)