﻿# Integration Notes

A guide to integration of DataTables components from this repository into your MVC development project.  This guide is written for those using:

  * Visual Studio 2017
  * ASP.NET Core 1.1 or 2.0 MVC Web Application Project
  * Entity Framework Core (version appropriate for your ASP.NET Core MVC version)

## Steps to Integrate
1. Install Bower Packages
   * Bootstrap 3.3.7
   * jQuery 2.2.0
   * DataTables 1.10.16
   * DataTables.Net for Bootstrap 2.1.1
   
   This guide presumes Bootstrap and jQuery are installed, and the appropriate stylesheets and javascript are already included by Views/Shared/_Layout.cshtml.

2. Create a DataTables View using Customers.cshtml as a guide.  Note key components of this View.cshtml file:
   * References to the datatables.net-bs stylesheet
   * References to the datatables.net and datatables.net-bs javascript libraries
   * The inline-javascript declaring the datatable and column specification appropriate to your target data class (database table) model.  Take care to note the AJAX url and to which Controller the request will route
   * The HTML table into which DataTables will operate

   Other considerations include adding a link where you find appropriate to navigate the browser to your DataTables View .cshtml page.

3. Database Presumptions - this guide is not intended as a tutorial of MVC or Entity Frameworks and presumes:
   * A database table (containing the data you want DataTables to display) already exists in your database
   * A public class model exists (generally in your Models folder) for your target database table.
   * A DbContext-derived class exists and functions with Entity Frameworks to read data from our database table

4. Migrate/add the following classes in the repository Models folder into your project Models folder:
   1. DataTablesIQueryableExtensions.cs
   2. DataTablesLogicEntity.cs
   3. DataTablesModelBinder.cs
   4. DataTablesRequest.cs
   5. DataTablesResponse.cs

   After migration, it is recommended you edit and change the namespace of these classes to match other classes in your Models folder.

5. Revision to the Controller handling the Page and AJAX requests for the DataTables View.  Key components of the revisions include:
   * Use of Dependency Injection (DI) in the Controller class constructor storing a reference to the target database table context (DbContext-derived) class for the target data model.
   * Addition of the Action Method serving the DataTables Page request.  This is the one serving up your View.cshtml file.
   * Addition of the Action Method handling the AJAX request (for data) from the DataTables javascript library.  This is the method to which the AJAX url routes to.

6. Build and Test.  The project should now build and the DataTable components fully functioning.  Handled exceptions (when any occur) during AJAX requests will appear in a popup dialog.
