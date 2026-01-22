# EpicorKineticSyntaxSamples
Syntax samples for various Epicor Kinetic customizations

## Controls

* [TextBoxWithSearch](./Controls/TextBoxWithSearch.md)  
Explains how to add a standard Epicor search panel to allow the user to search for and select a valid Part Number to populate a Kinetic form field.
* [Troubleshooting Transactions](./Troubleshooting/Troubleshooting%20Transactions.md)  
Walks through common issues encountered when executing transactions in Epicor BPMs, Functions, or form customizations (Classic or Kinetic)
* [Transaction stuck in PartBinDeferred](./Troubleshooting/Transaction%20Stuck%20in%20PartBinDeferred.md)  
When issuing material from an Epicor Function by calling `IssueReturnSvc.PerformMaterialMovement`, the material gets issued to the job, but a PartBin record is retained with an incorrect OnHandQty (and maybe AllocatedQty) value, and a row appears in PartBinDeferred that never gets processed. This guide walks through how to _force_ Epicor to process the PartBinDeferred row to clean up the PartBin/PartAlloc/PartTran tables.

## Events

* [rest-kinetic](./Events/rest-kinetic.md)  
Walks through how to configure the `rest-kinetic` object in an event workflow to correctly pass the values from a local DataSet to the correct parameters when invoking a Kinetic business object method using a REST call.

## Other resources

* [Tips and Tricks](./Tips%20and%20Tricks.md)  
: Holding area for Kinetic examples that are not fully fleshed out or categorized

## Syntax Samples

This section includes simple examples of the basic syntax used to interact with the system. These examples may contain C#, JavaScript, or any other languages, so their applications will vary based on what type of customization you are implementing.

**To create an instance of any Business Object in C# in order to access that object's methods:**

```csharp
using (var svc = Ice.Assemblies.ServiceRenderer.GetService<Erp.Contracts.TipSvcContract>(Db))
{
    svc.GetByID(); // Add appropriate parameters
    //some other code here
    svc.GetList(); // Add appropriate parameters
    //some other code here
    svc.Update(); //Add appropriate parameters
}
```

**If you need to create an Erp context in C# (If `Db` is unavailable):**

```csharp
Erp.ErpContext DbErp = CallContext.Current.GetMainContext<Erp.ErpContext>();
if ((from Part_Row in DbErp.Part
where string.Compare(Part_Row.Company, ttUD10_xRow.Company, true) == 0
select Part_Row).Any())
{
    // Custom code here
}
```

**Write a message to server log in C#:**

```csharp
Ice.Diagnostics.Log.WriteEntry("TEST1" + " " + "test2");
```

**Reading a UD field value in C# in a Method Directive:**

```csharp
var x = ds.ABCCode.UDField<System.String>("MyNewColumn _c");
```

