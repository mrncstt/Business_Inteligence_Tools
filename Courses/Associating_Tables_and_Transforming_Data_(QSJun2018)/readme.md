![](https://i.imgur.com/JFeHEuc.png)
![](https://i.imgur.com/haEgVTL.png)

```
[Field Aliasing]
LIB CONNECT TO 'SOPacess';


//  ** Tables infos**
Costumers:
LOAD Address,
    City,
    CompanyName,
    ContactName,
    Country,
    CustomerID,
    DivisionID,
    Fax,
    Phone,
    PostalCode,
    StateProvince;
SQL SELECT Address,
    City,
    CompanyName,
    ContactName,
    Country,
    CustomerID,
    DivisionID,
    Fax,
    Phone,
    PostalCode,
    StateProvince
FROM customers;

Divisions:
LOAD DivID AS DivisionID,
    DivName AS DivisionName;
SQL SELECT DivID,
    DivName
FROM divisions;


Orders:
LOAD CustomerID,
    EmployeeID,
    FreightWeight,
    OrderDate,
    OrderID,
    ShipperID;
SQL SELECT CustomerID,
    EmployeeID,
    FreightWeight,
    OrderDate,
    OrderID,
    ShipperID
FROM orders;




[Transforming]
LIB CONNECT TO 'SOPacess';


//
OrderDetails:
      //You can not reference newly-created fields within the same load block
LOAD *, //Will load all the previously atributes
    LinePreDiscount * Quantity * ( 1 - Discount)
    	AS LineSalesAmount;
    
    
LOAD Discount,
    LineNo,
    OrderID,
    ProductID,
    Quantity,
    UnitPrice,
    //Nova coluna calculada
    UnitPrice * Quantity 
    	AS LinePreDiscount;


SQL SELECT Discount,
    LineNo,
    OrderID,
    ProductID,
    Quantity,
    UnitPrice
FROM orderdetails;

//The data flows upwards
//    ^
//    |

```
