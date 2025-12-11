# Transaction stuck in PartBinDeferred

When issuing material from an Epicor Function by calling `IssueReturnSvc.PerformMaterialMovement`, the material gets issued to the job, but a PartBin record is retained with an incorrect OnHandQty (and maybe AllocatedQty) value, and a row appears in PartBinDeferred that never gets processed. This guide walks through how to _force_ Epicor to process the PartBinDeferred row to clean up the PartBin/PartAlloc/PartTran tables.

The problem is that Epicor is not cleaning up after itself when `PerformMaterialMovement` is being called from within a Function. In the normal UI, Epicor will automatically process any pending transactions in PartBinDeferred to complete the process of issuing the lots, but it seems to just skip doing this when invoked from a function.

The Function will have to include code that tells Epicor to run the cleanup process to finish the transaction. Immediately after calling `IssueReturnSvc.PerformMaterialMovement`, run this code:

```csharp
// Get the real ErpContext from the Function host
Epicor.Functions.IFunctionHost host =
    (Epicor.Functions.IFunctionHost)this.GetType().BaseType.BaseType
        .GetField("host", System.Reflection.BindingFlags.NonPublic | System.Reflection.BindingFlags.Instance)
        .GetValue(this);

var db = (Erp.ErpContext)host.GetIceContext();

// Run the deferred update processor
var libDeferredUpdate = new Erp.Internal.Lib.DeferredUpdate(db);
libDeferredUpdate.UpdPQDemand();
```
**Note:** You will need to have a reference to the `Erp.Internal.Lib.DeferredUpdate.dll` assembly set up for the Function Library so that you will be able to access these methods.

This will "remind" Epicor to finish up the transaction by processing whatever is left in the PartBinDeferred table, which will clean up the discrepancies in the PartBin table and remove the "stuck" row from the PartBinDeferred table.