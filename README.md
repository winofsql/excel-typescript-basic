# excel-typescript-basic

```typescript
function main(workbook: ExcelScript.Workbook) {
  var name = workbook.getActiveWorksheet().getName();
  console.log(name);

  workbook.getActiveCell().setValue( name );

}
```

```typescript
function main(workbook: ExcelScript.Workbook): TableData[] {
  // Get the first table in the "PlainTable" worksheet.
  // If you know the table name, use `workbook.getTable('TableName')` instead.
  const table = workbook.getWorksheet("Sheet1").getTables()[0];

  // Get all the values from the table as text.
  const texts = table.getRange().getTexts();

  // Create an array of JSON objects that match the row structure.
  let returnObjects: TableData[] = [];
  if (table.getRowCount() > 0) {
    returnObjects = returnObjectFromValues(texts);
  }

  // Log the information and return it for a Power Automate flow.
  // console.log(JSON.stringify(returnObjects));
  console.log(returnObjects);
  return returnObjects;
}

// This function converts a 2D array of values into a generic JSON object.
// In this case, we have defined the TableData object, but any similar interface would work.
function returnObjectFromValues(values: string[][]): TableData[] {
  let objectArray: TableData[] = [];
  let objectKeys: string[] = [];
  for (let i = 0; i < values.length; i++) {
    if (i === 0) {
      objectKeys = values[i];
      continue;
    }

    let object = {};
    for (let j = 0; j < values[i].length; j++) {
      object[objectKeys[j]] = values[i][j];
    }

    objectArray.push(object as TableData);
  }

  return objectArray;
}

interface TableData {
  "Event ID": string;
  Date: string;
  Location: string;
  Capacity: string;
  Speakers: string;
}

```
