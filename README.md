# Pipe Tools Diameter Library

This repository stores a JSON configuration file with links to pipe diameter
tables used by the Pipe Tools Blender add-on.

The repository does not contain the Pipe Tools add-on source code. It only
contains configuration data that tells the add-on where to load pipe diameter
libraries from.

## Purpose

Pipe Tools can load pipe diameter data from external CSV tables. This allows
users to maintain pipe diameter libraries separately from the Blender add-on
itself.

This repository is intended to be used as a remote configuration source for
Pipe Tools.

Typical use cases:

* storing links to Google Sheets CSV tables
* separating diameter libraries by building, object, project, or standard
* updating pipe diameter data without reinstalling the add-on
* sharing one common diameter library between multiple users

## Repository Structure

```text
.
├── README.md
└── tables.json
```

The main file is:

```text
tables.json
```

It contains a list of named pipe diameter tables.

## JSON Format

The JSON file must use the following structure:

```json
{
  "Building 1": "https://example.com/table_1.csv",
  "Building 2": "https://example.com/table_2.csv",
  "Building 3": "https://example.com/table_3.csv"
}
```

Each key is the name that will be shown in Pipe Tools as a building, object,
project, or library group.

Each value must be a direct CSV link to a pipe diameter table.

Example:

```json
{
  "Demo Building": "https://docs.google.com/spreadsheets/d/e/.../pub?gid=0&single=true&output=csv",
  "Workshop Area": "https://docs.google.com/spreadsheets/d/e/.../pub?gid=123456789&single=true&output=csv"
}
```

## CSV Table Format

Each linked CSV table must contain at least the following columns:

```text
Diameter,type
```

Example:

```csv
Diameter,type
57,DN 50
76,DN 65
89,DN 80
108,DN 100
159,DN 150
219,DN 200
```

Column requirements:

* `Diameter` — pipe outer diameter in millimeters
* `type` — pipe type, label, standard, or description

Both columns must be present and filled in.

## Google Sheets Setup

To use Google Sheets as a pipe diameter source:

1. Create a Google Sheet with the required columns:

```text
Diameter,type
```

2. Fill the table with pipe diameter data.

3. Open:

```text
File → Share → Publish to web
```

4. Select the required sheet.

5. Choose:

```text
Comma-separated values (.csv)
```

6. Publish the table.

7. Copy the generated CSV link.

8. Add the link to `tables.json`.

The final Google Sheets link should usually end with:

```text
output=csv
```

## Using This Repository in Pipe Tools

To use this repository as a remote Pipe Tools library configuration:

1. Open the `tables.json` file in this repository.

2. Open the raw version of the file.

3. Copy the raw URL.

4. In Blender, open:

```text
Edit → Preferences → Add-ons → Pipe Tools
```

5. Find the Pipe Library Config settings.

6. Set the config source to:

```text
URL
```

7. Paste the raw `tables.json` URL.

8. Click:

```text
Reload Pipe Library
```

After successful loading, the Building and Diameter drop-down lists in Pipe Tools
will be populated from the linked CSV tables.

## Important Notes

* Use direct raw links for JSON and CSV files.
* Do not use normal GitHub or GitLab web page links instead of raw file links.
* JSON must use straight double quotes.
* Do not use trailing commas in JSON.
* Each CSV link must be publicly accessible if the add-on needs to load it
  without authentication.
* Do not store confidential, client-related, or internal production data in a
  public repository.
* If the Google Sheet is private, Pipe Tools may not be able to access it.
* If a linked table is renamed, moved, unpublished, or deleted, Pipe Tools will
  not be able to load it.

## Updating the Library

To update the pipe diameter library:

1. Edit the corresponding Google Sheet or CSV table.
2. Save or publish the updated table.
3. In Blender, click:

```text
Reload Pipe Library
```

If you need to add a new building, object, or project:

1. Create or publish a new CSV table.
2. Add a new entry to `tables.json`.
3. Commit and push the updated JSON file.
4. Reload the library in Pipe Tools.

## Example `tables.json`

```json
{
  "Demo Building": "https://docs.google.com/spreadsheets/d/e/EXAMPLE_ID/pub?gid=0&single=true&output=csv",
  "Production Area": "https://docs.google.com/spreadsheets/d/e/EXAMPLE_ID/pub?gid=111111111&single=true&output=csv",
  "Workshop": "https://docs.google.com/spreadsheets/d/e/EXAMPLE_ID/pub?gid=222222222&single=true&output=csv"
}
```

## Troubleshooting

If the diameter library does not load in Pipe Tools, check the following:

* the JSON file is valid
* the JSON URL is a raw file link
* all CSV links are direct and publicly accessible
* each CSV table contains the `Diameter` and `type` columns
* the `Diameter` column contains numeric values
* the `type` column is not empty
* there are no extra commas or invalid quotes in the JSON file
* Blender has internet access
* the Google Sheet is still published to the web

## Related Project

Pipe Tools is a Blender add-on for procedural pipe modeling based on Curve
objects and Geometry Nodes.

The add-on supports:

* pipe diameter selection from external libraries
* custom pipe diameters
* procedural pipe fillets
* pipe adapters
* pipe ends
* warnings and validation tools
* applying and splitting generated pipe geometry

This repository is only a remote diameter library configuration source for the
add-on.

## License

This repository contains configuration files and sample data only.

If you use this repository as a public example, make sure that all linked tables
and data are allowed to be shared publicly.

Pipe Tools itself is distributed separately and is not included in this
repository.
