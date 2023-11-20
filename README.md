- 👋 Hi, I’m @shiyasnisar
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
shiyasnisar/shiyasnisar is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
Feedback Type:
Frown (Error)

Timestamp:
2023-11-20T07:38:22.0085646Z

Local Time:
2023-11-20T13:08:22.0085646+05:30

Session ID:
d7ba2ef8-1d67-4918-84ac-2f853beff393

Release:
October 2023

Product Version:
2.122.746.0 (23.10) (x64)

OS Version:
Microsoft Windows NT 10.0.19045.0 (x64 en-US)

CLR Version:
4.8 or later [Release Number = 533325]

Peak Virtual Memory:
102 GB

Private Memory:
579 MB

Peak Working Set:
1 GB

IE Version:
11.3570.19041.0

User ID:
f55f054c-d1a0-4b7d-9942-275ac63c82eb

Workbook Package Info:
1* - en-IN, Query Groups: 0, fastCombine: Disabled, runBackgroundAnalysis: False.

Telemetry Enabled:
True

Snapshot Trace Logs:
C:\Users\WINDOWS\AppData\Local\Microsoft\Power BI Desktop\FrownSnapShotd15e706a-2ac2-41d9-b4a7-adaf59b245b4.zip

Model Default Mode:
Import

Model Version:
PowerBI_V3

Performance Trace Logs:
C:\Users\WINDOWS\AppData\Local\Microsoft\Power BI Desktop\PerformanceTraces.zip

Enabled Preview Features:
PBI_sparklines
PBI_scorecardVisual
PBI_NlToDax
PBI_fieldParametersSuperSwitch
PBI_setLabelOnExportPdf
PBI_dynamicFormatString
PBI_oneDriveSave
PBI_oneDriveShare
PBI_newCard

Disabled Preview Features:
PBI_shapeMapVisualEnabled
PBI_SpanishLinguisticsEnabled
PBI_qnaLiveConnect
PBI_b2bExternalDatasetSharing
PBI_enhancedTooltips
PBI_angularRls
PBI_onObject
PBI_backstageUI
PBI_gitIntegration
PBI_modelExplorer

Disabled DirectQuery Options:
TreatHanaAsRelationalSource

Cloud:
GlobalCloud

DPI Scale:
100%

Supported Services:
Power BI

Formulas:


section Section1;

shared covid_vaccine_statewise = let
    Source = Csv.Document(File.Contents("C:\Users\WINDOWS\Downloads\Task 2 Power BI Dashboard Creation - COVID-19 Daily Cases\covid_vaccine_statewise.csv"),[Delimiter=",", Columns=24, Encoding=1252, QuoteStyle=QuoteStyle.None]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"Updated On", type date}, {"State", type text}, {"Total Doses Administered", Int64.Type}, {"Sessions", Int64.Type}, {" Sites ", Int64.Type}, {"First Dose Administered", Int64.Type}, {"Second Dose Administered", Int64.Type}, {"Male (Doses Administered)", Int64.Type}, {"Female (Doses Administered)", Int64.Type}, {"Transgender (Doses Administered)", Int64.Type}, {" Covaxin (Doses Administered)", Int64.Type}, {"CoviShield (Doses Administered)", Int64.Type}, {"Sputnik V (Doses Administered)", Int64.Type}, {"AEFI", Int64.Type}, {"18-44 Years (Doses Administered)", Int64.Type}, {"45-60 Years (Doses Administered)", Int64.Type}, {"60+ Years (Doses Administered)", Int64.Type}, {"18-44 Years(Individuals Vaccinated)", Int64.Type}, {"45-60 Years(Individuals Vaccinated)", Int64.Type}, {"60+ Years(Individuals Vaccinated)", Int64.Type}, {"Male(Individuals Vaccinated)", Int64.Type}, {"Female(Individuals Vaccinated)", Int64.Type}, {"Transgender(Individuals Vaccinated)", Int64.Type}, {"Total Individuals Vaccinated", Int64.Type}}),
    #"Split Column by Delimiter" = Table.SplitColumn(Table.TransformColumnTypes(#"Changed Type", {{"Updated On", type text}}, "en-IN"), "Updated On", Splitter.SplitTextByEachDelimiter({"-"}, QuoteStyle.Csv, true), {"Updated On.1", "Updated On.2"}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Split Column by Delimiter",{{"Updated On.1", type date}, {"Updated On.2", Int64.Type}}),
    #"Extracted Month Name" = Table.TransformColumns(#"Changed Type1", {{"Updated On.1", each Date.MonthName(_), type text}}),
    #"Renamed Columns" = Table.RenameColumns(#"Extracted Month Name",{{"Updated On.1", "Month"}}),
    #"Merged Columns" = Table.CombineColumns(Table.TransformColumnTypes(#"Renamed Columns", {{"Updated On.2", type text}}, "en-IN"),{"Month", "Updated On.2"},Combiner.CombineTextByDelimiter("-", QuoteStyle.None),"Merged"),
    #"Renamed Columns1" = Table.RenameColumns(#"Merged Columns",{{"Merged", "MM-YY"}}),
    #"Filtered Rows" = Table.SelectRows(#"Renamed Columns1", each ([Total Doses Administered] <> null)),
    #"Filtered Rows1" = Table.SelectRows(#"Filtered Rows", each [#" Sites "] <> null and [#" Sites "] <> ""),
    #"Filtered Rows2" = Table.SelectRows(#"Filtered Rows1", each ([Sessions] <> null and [Sessions] <> "") and ([#"Male (Doses Administered)"] <> null)),
    #"Filtered Rows3" = Table.SelectRows(#"Filtered Rows2", each [#"Male (Doses Administered)"] <> null and [#"Male (Doses Administered)"] <> ""),
    #"Filtered Rows4" = Table.SelectRows(#"Filtered Rows3", each [#"Sputnik V (Doses Administered)"] <> null and [#"Sputnik V (Doses Administered)"] <> ""),
    #"Filtered Rows5" = Table.SelectRows(#"Filtered Rows4", each [#"18-44 Years (Doses Administered)"] <> null and [#"18-44 Years (Doses Administered)"] <> ""),
    #"Removed Columns" = Table.RemoveColumns(#"Filtered Rows5",{"18-44 Years(Individuals Vaccinated)", "45-60 Years(Individuals Vaccinated)", "60+ Years(Individuals Vaccinated)", "Male(Individuals Vaccinated)", "Female(Individuals Vaccinated)", "Transgender(Individuals Vaccinated)", "Total Individuals Vaccinated"}),
    #"Renamed Columns2" = Table.RenameColumns(#"Removed Columns",{{" Covaxin (Doses Administered)", "Covaxin"}, {"CoviShield (Doses Administered)", "CoviShield"}, {"Transgender (Doses Administered)", "Transgender"}, {"45-60 Years (Doses Administered)", "45-60 Years"}, {"60+ Years (Doses Administered)", "60+ Years"}, {"18-44 Years (Doses Administered)", "18-44 Years"}, {"Sputnik V (Doses Administered)", "Sputnik V"}, {"Female (Doses Administered)", "Female"}, {"Male (Doses Administered)", "Male"}}),
    #"Filtered Rows6" = Table.SelectRows(#"Renamed Columns2", each ([State] <> "India")),
    #"Removed Columns1" = Table.RemoveColumns(#"Filtered Rows6",{"Sessions", " Sites "}),
    #"Renamed Columns3" = Table.RenameColumns(#"Removed Columns1",{{"Total Doses Administered", "Total Doses "}})
in
    #"Renamed Columns3";
