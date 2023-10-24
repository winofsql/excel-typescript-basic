# excel-typescript-basic

```
function main(workbook: ExcelScript.Workbook) {
  var name = workbook.getActiveWorksheet().getName();
  console.log(name);

  workbook.getActiveCell().setValue( name );

}
```
