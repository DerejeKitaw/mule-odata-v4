## Install APIKit for OData
>[Source](https://docs.mulesoft.com/apikit/4.x/apikit-4-for-odata)
> Select Help > Install New Software
```
Name field, type APIkit for ODATA Update Site
APIKit for OData 2.0: http://studio.mulesoft.org/s4/apikit-for-odata/
APIKit for OData 4.0: http://studio.mulesoft.org/s4/apikit-for-odata4/
```

## Create an OData v4 API
> [Source](https://docs.mulesoft.com/apikit/4.x/creating-an-odatav4-api-with-apikit)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<edmx:Edmx Version="4.0" xmlns:edmx="http://docs.oasis-open.org/odata/ns/edmx">
  <edmx:DataServices>
    <Schema xmlns="http://docs.oasis-open.org/odata/ns/edm" Namespace="odata4.namespace">
      <EntityType Name="Customers"> 
        <Key> 
          <PropertyRef Name="CustomerID" />
        </Key>
        <Property Name="CompanyName" Type="Edm.String" MaxLength="40" Unicode="false" />
        <Property Name="ContactName" Type="Edm.String" MaxLength="30" Unicode="false" />
        <Property Name="ContactTitle" Type="Edm.String" MaxLength="30" Unicode="false" />
        <Property Name="CustomerID" Type="Edm.String" Nullable="false" MaxLength="5" Unicode="false" />
        <NavigationProperty Name="Orders" Type="Collection(odata4.namespace.Orders)"/>
      </EntityType>
      <EntityType Name="Orders">
        <Key>
          <PropertyRef Name="OrderID" />
          <PropertyRef Name="ShipName" />
        </Key>
        <Property Name="Freight" Type="Edm.Decimal" Precision="19" Scale="4" />
        <Property Name="OrderDate" Type="Edm.DateTimeOffset" Unicode="false" />
        <Property Name="OrderID" Type="Edm.Int32" Nullable="false" Unicode="false" />
        <Property Name="CustomerID" Type="Edm.String" MaxLength="5"/>
        <Property Name="Price" Type="Edm.Single" Unicode="false" />
        <Property Name="Priority" Type="Edm.Int16" Unicode="false" />
        <Property Name="ShipAddress" Type="Edm.String" MaxLength="60" Unicode="false" />
        <Property Name="ShipName" Type="Edm.String" Nullable="false" MaxLength="40" Unicode="false" />
        <NavigationProperty Name="Customer" Type="odata4.namespace.Customers">
        	<ReferentialConstraint Property="CustomerID" ReferencedProperty="CustomerID" />
        </NavigationProperty>
      </EntityType>
      <EntityContainer Name="OData4EntityContainer"> 
        <EntitySet Name="Customers" EntityType="odata4.namespace.Customers"> 
        	<NavigationPropertyBinding Path="Orders" Target="Orders"/>
        </EntitySet>
        <EntitySet Name="Orders" EntityType="odata4.namespace.Orders"/>
      </EntityContainer>
    </Schema>
  </edmx:DataServices>
</edmx:Edmx>
```
> `EntityType` defines the type and its properties

> `key` defines which property or set of properties is the key for the entity.
- For example, the entity set `Orders` is composed of two keys `OrderID` and `ShipName`.
> `EntityContainer` defines the sets of exposed entities.
- In this example, Orders and Customers.
> `EntitySet` contains a name and EntityType.
- Both must be defined in the schema namespace.

## odata-metadata.csdl.xml file > Generate Mule OData 4 API

