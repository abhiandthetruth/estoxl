# estoxl
This project aims to provide people a tool to export the data in their elastic search indexes to csv and even to ggogle sheets!. There are two scripts involved. First is the `estocsv.py`, which exports the data based on the specification given in `config.ini` to a csv file. The second is `csvtoxlsheet.py` exports the data generated in the csv to either an xlsx file or a Google sheet directly into your account!. Please read the documentation below thoroughly before using.  

# Procedure (All the examples provided were used by me) 

Following are the descriptions:
* estocsv.py
  * exports the index documents with only the selected fields.
  * Define a `config.ini` in the following format
  ```
  [elastic_search]
  url = http://localhost:9200
  index = groupsio_enriched
  fields = uuid, project, project_1, origin, grimoirelab_creation_date, body_extract, Subject_analyzed
  ```
  * command line parameter `--cfg` to specify path of `config.ini`. You are free to keep your config files anywhere as long as you specify it's path.
* csvtoxlsheet.py
  * Support to export the csv to xlsx and google sheets using the api.
  * Various command line arguments are now supported: 
 ```
--csv : Path to the csv file, required
--gen-xlsx: If specified,  generates the xlsx file
--new-sheet: Name of google sheet to be created, if a new one is to be created
--spreadsheet-id: Id of the spreadsheet the data is to be inserted, if an existing one is going to be used
--coordinates: Co-ordinates on sheet where to add data. If not specified 0, 0 is used.
```
  Clearly either of `--new-sheet` or `--spreadsheet-id` is required. If both are specified `--spreadsheet-id` gets a preference over `--new-sheet`. If neither of them is specified no interaction will take with google sheets api. The spreadsheet id of a spreadsheet can be extracted from the url of the spreadsheet. Maybe I will allow users to specify spreadsheet url in future versions.

Example commands 
```
python3 estocsv.py --cfg ./config.ini
python3 csvtoxlsheet.py --csv ./groupsio_enriched.csv --gen-xlsx --new-sheet groupsio --coordinates 0 5
python3 csvtoxlsheet.py --csv ./groupsio_enriched.csv --spreadsheet-id <spreadsheet-id>
```

Note that you need a `credentials.json` containing the client id and client secret for the api in the working directory for the script to work. You can obtain one from [here](https://developers.google.com/sheets/api/quickstart/python). Click on `enable sheets api` button there. Download the file and paste in the working directory. For the first time, it will attempt to open a new window or tab in your default browser. If this fails, copy the URL from the console and manually open it in your browser. If you are not already logged into your Google account, you will be prompted to log in. If you are logged into multiple Google accounts, you will be asked to select one account to use for the authorization. Click the Accept button. The sample will proceed automatically, and you may close the window/tab.
* You can check the exported data in the `{index_name}.csv` which here is, [`groupsio_enriched.csv`](/Microtask-8/groupsio_enriched.csv).
* You have all you wanted.

# Result
You have created raw, enriched indices, exported the selected fields into a csv and converted it into an excel sheet.

# Attachments

![Image](/Microtask-8/image.png)
![Image](/Microtask-8/kibiter.png)
![Image](/Microtask-8/csv.png)
![Image](/Microtask-8/xlsheet.png)
