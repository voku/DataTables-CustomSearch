#DataTables-CustomSearch

An extension to the jQuery plugin DataTables 1.10 (http://next.datatables.net) allowing you to specify custom search fields.


##Quick Example

```javascript
var table = $('table').dataTable();
new $.fn.dataTable.CustomSearch(table);
```


##Options

###container
Can be a jQuery selector string or a jQuery object. Will be where the fields are appended to. If not passed in then it will prepend it to the DataTables wrapper (effectively putting it on top of the table).

###hideStandardSearch
Whether or not to hide the DataTables search field.

###fields
An array of columns to give search fields. Starts at index of 0.
```javascript
fields: [0,2,3,4,5,6]
```

If an array is passed in as fields the field will search both columns using OR.
```javascript
fields: [0,[2,3],[4,6],5]
```

If you want to have more control then you need to pass in an object.
```javascript
fields: [
  {
    field: '#myField',
    columns: 0
  },
  [2,3],
  {
    label: 'String Field',
    columns: [4,6],
    type: 'string'
  },
  {
    label: 'Number Field',
    columns: 5,
    type: 'number',
    range: ['min','max']
  },
  {
    type: 'select',
    columns: 7,
    options: [
      {
        value: 'a',
        text: 'abc'
      },
      'def'
    ]
  }
]
```

##Fields Options

####columns
Default: ```[]```

Required

Accepts: number or array of numbers

Requirements: none

This will tie the field to the column(s) (starting with an index of 0).


####field
Default: ''

Optional

Accepts: jQuery selector string or jQuery object

Requirements: none

This will tie an existing field to search the column. If supplied the label, type, and options will be ignored.


####label
Default: Column Header (if a range then a concat of the column headers).

Optional

Accepts: string (plain text or html)

Requirements: none

The text in the ```<label>``` tag.


####type
Default: DataTables column types (https://next.datatables.net/reference/option/columns.type)

Optional

Accepts: ```'string', 'number', 'select', 'date'```

Requirements: none

This specifies the type of field to create, and affects how it is searched.


####range
Default: ```[]```

Optional

Accepts: ```[], ['min'], ['max'], ['min', 'max']```

Requirements: type is number or date

This will create a min and/or max field that the column values will have to be between.


####advanced
Default: false

Optional

Accepts: boolean

Requirements: none

Puts a dropdown in from the of the field giving the user advanced searching options. It will have: contains, does not contain, is equal to, is not equal to. If the type is a number or range then it will give the options is greater than and is less than.


####caseInsensitive
Default: true

Optional

Accepts: boolean

Requirements: none

Whether or not string searches should be case sensitive or not.


####server
Default: ```null```

Optional

Accepts: string

Requirements: dataTables serverSide is set to true

If the dataTables serverSide option is set to true this plugin will automatically send the request. All fields will be added to the request using their id in the associative array customsearch. If you want a custom key in the array for the field then specify this field.


####options
Default: The distinct values in the column

Optional

Accepts: an array of strings or objects

Requirements: ```type == 'select'```

This will specify the options available in the select field. If the array item is an object then you need to specify the value and the text of the option. If it is a string then it counts for both. An 'All' option will always be put first with a value of ''.


###Events

####after
Default: ```null```

Optional

Accepts: function

Requirements: none

Parameters: An array of the filtered data