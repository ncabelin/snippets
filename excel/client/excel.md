# EXCEL GENERATION (client side)

Here's a [Github link](https://github.com/SheetJS/js-xlsx) to the full documentation. The following is just my summary of the minimum steps I would take to implement Excel generation client side.

```
// include these files
<script src="assets/xlsx.full.min.js"></script>
<script src="assets/Blob.js"></script>
<script src="assets/FileSaver.js"></script>

// 
<script>
var Excel = {
		generate: function(data) {
			// data needs to be an array e.g. data = [[1,2,3],[true, false, null, "sheetjs"],["foo","bar",new Date("2014-02-19T14:30Z"), "0.3"], ["baz", null, "qux"]]
			
			// worksheet name
			var ws_name = "Leads";
			
			var wb = XLSX.utils.book_new(), ws = XLSX.utils.aoa_to_sheet(data);
			/* add worksheet to workbook */
			// wch is character #s
			var wscols = [
			    {wch:16}, // date
			    {wch:10}, // firstname
			    {wch:10}, // lastname
			    {wch:20}, // businessname
			    {wch:30}, // email
			    {wch:15}, // phone
			    {wch:6}, // origin
			    {wch:6}, // ad num
			];

			ws['!cols'] = wscols;
			XLSX.utils.book_append_sheet(wb, ws, ws_name);
			var wbout = XLSX.write(wb, {bookType:'xlsx', bookSST:true, type: 'array'});

			// enter the filename
			saveAs(new Blob([wbout],{type:"application/octet-stream"}), "filename_here.xlsx");
		},
		convertData: function() {
			var arr = [['Date / Time', 'Firstname', 'Lastname', 'Businessname', 'E-mail', 'Phone', 'Origin', 'Ad #']];
				
			// this part is DataTables
			Table.rows( { search:'applied' } ).data().each(function(value, index) {
					// manipulate whatever data you want here
			    arr.push(value);
			});
			return arr;
		}
	}
</script>
```