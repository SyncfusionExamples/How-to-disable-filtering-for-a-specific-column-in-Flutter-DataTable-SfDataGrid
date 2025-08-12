# How-to-disable-filtering-for-a-specific-column-in-Flutter-DataTable-SfDataGrid

In this article, we will show how to disable filtering for a specific column in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the necessary properties. The SfDataGrid provides a callback named [onFilterChanging](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/onFilterChanging.html), which is triggered when filtering is applied to a specific column through the UI.

Within the onFilterChanging callback, you can access the details property to retrieve information about the column being filtered, such as its name. By returning false from this callback, you can prevent filtering from being applied to that particular column.

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Syncfusion Flutter DataGrid')),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: TextButton(
              onPressed: () {
                setState(() {
                  canDisableFiltering = true;
                });
              },
              style: TextButton.styleFrom(minimumSize: Size(200, 50)),
              child: Text('Disable ID Filter'),
            ),
          ),
          Expanded(
            child: SfDataGrid(
              source: employeeDataSource,
              allowFiltering: true,
              onFilterChanging: (details) {
                if (details.column.columnName == 'id' && canDisableFiltering) {
                  return false; //Disabling ID column Filter
                }
                return true;
              },
              columnWidthMode: ColumnWidthMode.fill,
              columns: <GridColumn>[
                GridColumn(
                  columnName: 'id',
                  label: Container(
                    padding: EdgeInsets.all(16.0),
                    alignment: Alignment.center,
                    child: Text('ID'),
                  ),
                ),
                GridColumn(
                  columnName: 'name',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Name'),
                  ),
                ),
                GridColumn(
                  columnName: 'designation',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Designation', overflow: TextOverflow.ellipsis),
                  ),
                ),
                GridColumn(
                  columnName: 'salary',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Salary'),
                  ),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-disable-filtering-for-a-specific-column-in-Flutter-DataTable-SfDataGrid.git).
