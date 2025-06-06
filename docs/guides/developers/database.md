---
title: Database
after: permissions
---

# Database

The Oxide database extensions<sup><a href="/glossary#extensions">[2]</a></sup> implement a generalized database abstraction layer for both MySQL and SQLite.
[MySQL](https://dev.mysql.com/downloads/installer/) and [MariaDB](https://mariadb.org/download/?t=mariadb&p=mariadb&r=11.7.2&os=windows&cpu=x86_64&pkg=msi&mirror=osuosl) are probably the most commonly used server, but other products also be used.

Database functionality is essential for plugins<sup><a href="/glossary#plugins">[3]</a></sup> that need to store large amounts of data or perform complex queries that would be inefficient with traditional data files<sup><a href="/glossary#data-files">[10]</a></sup>.

## Open a connection

Create a new `MYSQL` connection to a database by providing the database file location or an address (URI and port), a database name, and authentication credentials.

```csharp
Core.MySql.Libraries.MySql sqlLibrary = Interface.Oxide.GetLibrary<Core.MySql.Libraries.MySql>();
Connection sqlConnection = sqlLibrary.OpenDb("localhost", 3306, "umod", "username", "password", this);
```

In the case of SQLite, the database is local, in `./oxide/data/` folder

```csharp
Oxide.Core.SQLite.Libraries.SQLite sqlLibrary = Interface.Oxide.GetLibrary<Oxide.Core.SQLite.Libraries.SQLite>();
Connection sqlConnection = sqlLibrary.OpenDb(_databaseName, this);
```

## Close the connection

Close an existing connection to the database.

```csharp
sqlLibrary.CloseDb(sqlConnection);
```

## Query the database

Retrieve data from the database, typically using a SELECT statement.

```csharp
string sqlQuery = "SELECT `id`, `field1`, `field2` FROM example_table";
Sql selectCommand = Oxide.Core.Database.Sql.Builder.Append(sqlQuery);

sqlLibrary.Query(selectCommand, sqlConnection, list =>
{
    if (list == null)
    {
        return; // Empty result or no records found
    }

    StringBuilder newString = new StringBuilder();
    newString.AppendLine(" id\tfield1\tfield2");

    // Iterate through resulting records
    foreach (Dictionary<string, object> entry in list)
    {
        newString.AppendFormat(" {0}\t{1}\t{2}\n", entry["id"], entry["field1"], entry["field2"]);
    }

    Puts(newString.ToString());
});
```

## Insert query

Insert records into the database using an INSERT statement.

```csharp
string sqlQuery = "INSERT INTO example_table (`field1`, `field2`) VALUES (@0, @1);";
Sql insertCommand = Oxide.Core.Database.Sql.Builder.Append(sqlQuery, "field1 value", "field2 value");

sqlLibrary.Insert(insertCommand, sqlConnection, rowsAffected =>
{
    if (rowsAffected > 0)
    {
        Puts("New record inserted with ID: {0}", sqlConnection.LastInsertRowId);
    }
});
```

## Update query

Update existing records in the database using an UPDATE statement.

```csharp
int exampleId = 2;
string sqlQuery = "UPDATE example_table SET `field1` = @0, `field2` = @1  WHERE `id` = @2;";
Sql updateCommand = Oxide.Core.Database.Sql.Builder.Append(sqlQuery, "field1 value", "field2 value", exampleId);

sqlLibrary.Update(updateCommand, sqlConnection, rowsAffected =>
{
    if (rowsAffected > 0)
    {
        Puts("Record successfully updated!");
    }
});
```

## Delete query

Delete existing records from a database using a DELETE statement.

```csharp
int exampleId = 2;
string sqlQuery = "DELETE FROM example_table WHERE `id` = @0;";
Sql deleteCommand = Oxide.Core.Database.Sql.Builder.Append(sqlQuery, exampleId);

sqlLibrary.Delete(deleteCommand, sqlConnection, rowsAffected =>
{
    if (rowsAffected > 0)
    {
        Puts("Record successfully deleted!");
    }
});
```

## Non-query

By definition a non-query is a query which modifies data and does not retrieve data. Insert, Update, and Delete queries are all considered non-queries.

```csharp
int exampleId = 2;
string sqlQuery = "UPDATE example_table SET `field1` = @0, `field2` = @1  WHERE `id` = @3;";
Sql sqlCommand = Oxide.Core.Database.Sql.Builder.Append(sqlQuery, "field1 value", "field2 value", exampleId);

sqlLibrary.ExecuteNonQuery(sqlCommand, sqlConnection);
```
