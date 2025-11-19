# Table of Contents


* [Unable to modify engineered job](#modify-engineered-job) "Update not allowed, Engineered and Prevent Changes."

---


## Modify Engineered Job

When trying to programatically modify a job using a BPM or Function, if the job has been engineered, you are not able to update it. Even if you set the `JobHead.JobEngineered` to `false` and try to call `JobEntrySvc.Update()`, the change will not be saved. The helper function `JobEntrySvc.ChangeJobHeadJobEngineered()` does not unengineer the job either.

Calling `JobEntrySvc.Update()` on an engineered job will return the error **"Update not allowed, Engineered and Prevent Changes."**

The only way I've found so far to update an engineered job is to use `JobEntrySvc.UpdateExt()` instead of `JobEntrySvc.Update()`.

Here's an example:

```csharp

// string "jobNum" is defined elsewhere or taken in as a parameter

CallService<Erp.Contracts.JobEntrySvcContract>(JobEntrySvc => {
      var uejets = new Erp.Tablesets.UpdExtJobEntryTableset();
      var jhr = uejets.JobHead.NewRow();
      jhr["Company"]=Session.CompanyID;
      jhr["JobNum"] = jobNum;
      jhr["JobEngineered"] =  false;
      uejets.JobHead.Add(jhr);
      bool obool;
      JobEntrySvc.UpdateExt(ref uejets, false, true, out obool);
});
```
