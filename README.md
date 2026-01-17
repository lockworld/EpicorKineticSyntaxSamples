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