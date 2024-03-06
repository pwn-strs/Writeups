# Smoke Out the Rat

Directly searching the raw binary file for the number `789-012-3456`, gave the name of the traitor - `Matthew Miller`

Then parsed the file using `mysqlbinlog`

The employees table was changing at `15:31:29` and 2 names in the binary there were `John Darwin` & `John Smith`

Checking both the names gave the flag

# Flag: `VishwaCTF{Matthew_Darwin_15:31:29}`